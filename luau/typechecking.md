# Typechecking

Luau supports a gradual type system through the use of type annotations and type inference.

### Type inference modes <a href="#type-inference-modes" id="type-inference-modes"></a>

There are three modes currently available. They must be annotated on the top few lines among the comments.

* `--!nocheck`,
* `--!nonstrict` (default), and
* `--!strict`

`nocheck` mode will simply not start the type inference engine whatsoever.

As for the other two, they are largely similar but with one important difference: in nonstrict mode, we infer `any` for most of the types if we couldn’t figure it out early enough. This means that given this snippet:

```
local foo = 1
```

We can infer `foo` to be of type `number`, whereas the `foo` in the snippet below is inferred `any`:

```
local foo
foo = 1
```

However, given the second snippet in strict mode, the type checker would be able to infer `number` for `foo`.

### Structural type system <a href="#structural-type-system" id="structural-type-system"></a>

Luau’s type system is structural by default, which is to say that we inspect the shape of two tables to see if they are similar enough. This was the obvious choice because Lua 5.1 is inherently structural.

```
type A = {x: number, y: number, z: number?}
type B = {x: number, y: number, z: number}

local a1: A = {x = 1, y = 2}        -- ok
local b1: B = {x = 1, y = 2, z = 3} -- ok

local a2: A = b1 -- ok
local b2: B = a1 -- not ok
```

### Builtin types <a href="#builtin-types" id="builtin-types"></a>

The Luau VM supports 10 primitive types: `nil`, `string`, `number`, `boolean`, `table`, `function`, `thread`, `userdata`, `vector`, and `buffer`. Of these, `table` and `function` are not represented by name, but have their dedicated syntax as covered in this syntax document, `userdata` is represented by [concrete types](typechecking.md#roblox-types), while `vector` is not representable by name at all; other types can be specified by their name.

The type checker also provides the builtin types [`unknown`](typechecking.md#unknown-type), [`never`](typechecking.md#never-type), and [`any`](typechecking.md#any-type).

```
local s = "foo"
local n = 1
local b = true
local t = coroutine.running()

local a: any = 1
print(a.x) -- Type checker believes this to be ok, but crashes at runtime.
```

There’s a special case where we intentionally avoid inferring `nil`. It’s a good thing because it’s never useful for a local variable to always be `nil`, thereby permitting you to assign things to it for Luau to infer that instead.

```
local a
local b = nil
```

#### `unknown` type <a href="#unknown-type" id="unknown-type"></a>

`unknown` is also said to be the _top_ type, that is it’s a union of all types.

```
local a: unknown = "hello world!"
local b: unknown = 5
local c: unknown = function() return 5 end
```

Unlike `any`, `unknown` will not allow itself to be used as a different type!

```
local function unknown(): unknown
    return if math.random() > 0.5 then "hello world!" else 5
end

local a: string = unknown() -- not ok
local b: number = unknown() -- not ok
local c: string | number = unknown() -- not ok
```

In order to turn a variable of type `unknown` into a different type, you must apply [type refinements](typechecking.md#type-refinements) on that variable.

```
local x = unknown()
if typeof(x) == "number" then
    -- x : number
end
```

#### `never` type <a href="#never-type" id="never-type"></a>

`never` is also said to be the _bottom_ type, meaning there doesn’t exist a value that inhabits the type `never`. In fact, it is the _dual_ of `unknown`. `never` is useful in many scenarios, and one such use case is when type refinements proves it impossible:

```
local x = unknown()
if typeof(x) == "number" and typeof(x) == "string" then
    -- x : never
end
```

#### `any` type <a href="#any-type" id="any-type"></a>

`any` is just like `unknown`, except that it allows itself to be used as an arbitrary type without further checks or annotations. Essentially, it’s an opt-out from the type system entirely.

```
local x: any = 5
local y: string = x -- no type errors here!
```

### Function types <a href="#function-types" id="function-types"></a>

Let’s start with something simple.

```
local function f(x) return x end

local a: number = f(1)     -- ok
local b: string = f("foo") -- ok
local c: string = f(true)  -- not ok
```

In strict mode, the inferred type of this function `f` is `<A>(A) -> A` (take a look at [generics](typechecking.md#generics)), whereas in nonstrict we infer `(any) -> any`. We know this is true because `f` can take anything and then return that. If we used `x` with another concrete type, then we would end up inferring that.

Similarly, we can infer the types of the parameters with ease. By passing a parameter into _anything_ that also has a type, we are saying “this and that has the same type.”

```
local function greetingsHelper(name: string)
    return "Hello, " .. name
end

local function greetings(name)
    return greetingsHelper(name)
end

print(greetings("Alexander"))          -- ok
print(greetings({name = "Alexander"})) -- not ok
```

### Table types <a href="#table-types" id="table-types"></a>

From the type checker perspective, each table can be in one of three states. They are: `unsealed table`, `sealed table`, and `generic table`. This is intended to represent how the table’s type is allowed to change.

#### Unsealed tables <a href="#unsealed-tables" id="unsealed-tables"></a>

An unsealed table is a table which supports adding new properties, which updates the tables type. Unsealed tables are created using table literals. This is one way to accumulate knowledge of the shape of this table.

```
local t = {x = 1} -- {x: number}
t.y = 2           -- {x: number, y: number}
t.z = 3           -- {x: number, y: number, z: number}
```

However, if this local were written as `local t: { x: number } = { x = 1 }`, it ends up sealing the table, so the two assignments henceforth will not be ok.

Furthermore, once we exit the scope where this unsealed table was created in, we seal it.

```
local function vec2(x, y)
    local t = {}
    t.x = x
    t.y = y
    return t
end

local v2 = vec2(1, 2)
v2.z = 3 -- not ok
```

Unsealed tables are _exact_ in that any property of the table must be named by the type. Since Luau treats missing properties as having value `nil`, this means that we can treat an unsealed table which does not mention a property as if it mentioned the property, as long as that property is optional.

```
local t = {x = 1}
local u : { x : number, y : number? } = t -- ok because y is optional
local v : { x : number, z : number } = t  -- not ok because z is not optional
```

#### Sealed tables <a href="#sealed-tables" id="sealed-tables"></a>

A sealed table is a table that is now locked down. This occurs when the table type is spelled out explicitly via a type annotation, or if it is returned from a function.

```
local t : { x: number } = {x = 1}
t.y = 2 -- not ok
```

Sealed tables are _inexact_ in that the table may have properties which are not mentioned in the type. As a result, sealed tables support _width subtyping_, which allows a table with more properties to be used as a table with fewer properties.

```
type Point1D = { x : number }
type Point2D = { x : number, y : number }
local p : Point2D = { x = 5, y = 37 }
local q : Point1D = p -- ok because Point2D has more properties than Point1D
```

#### Generic tables <a href="#generic-tables" id="generic-tables"></a>

This typically occurs when the symbol does not have any annotated types or were not inferred anything concrete. In this case, when you index on a parameter, you’re requesting that there is a table with a matching interface.

```
local function f(t)
    return t.x + t.y
           --^   --^ {x: _, y: _}
end

f({x = 1, y = 2})        -- ok
f({x = 1, y = 2, z = 3}) -- ok
f({x = 1})               -- not ok
```

### Table indexers <a href="#table-indexers" id="table-indexers"></a>

These are particularly useful for when your table is used similarly to an array.

```
local t = {"Hello", "world!"} -- {[number]: string}
print(table.concat(t, ", "))
```

Luau supports a concise declaration for array-like tables, `{T}` (for example, `{string}` is equivalent to `{[number]: string}`); the more explicit definition of an indexer is still useful when the key isn’t a number, or when the table has other fields like `{ [number]: string, n: number }`.

### Generics <a href="#generics" id="generics"></a>

The type inference engine was built from the ground up to recognize generics. A generic is simply a type parameter in which another type could be slotted in. It’s extremely useful because it allows the type inference engine to remember what the type actually is, unlike `any`.

```
type Pair<T> = {first: T, second: T }
-- generics can also have defaults!
type PairWithDefault<T = string> = Pair<T>

local strings: Pair<string> = { first="Hello", second="World" }
local numbers: Pair<number> = { first=1, second=2 }
-- can just treat PairWithDefault as a type that doesnt have generics because it has all of its generics assigned a default!
local more_strings: PairWithDefault = { first = "meow", second = "mrrp" }
```

### Generic functions <a href="#generic-functions" id="generic-functions"></a>

As well as generic type aliases like `Pair<T>`, Luau supports generic functions. These are functions that, as well as their regular data parameters, take type parameters. For example, a function which reverses an array is:

```
function reverse(a)
  local result = {}
  for i = #a, 1, -1 do
    table.insert(result, a[i])
  end
  return result
end
```

The type of this function is that it can reverse an array, and return an array of the same type. Luau can infer this type, but if you want to be explicit, you can declare the type parameter `T`, for example:

```
function reverse<T>(a: {T}): {T}
  local result: {T} = {}
  for i = #a, 1, -1 do
    table.insert(result, a[i])
  end
  return result
end
```

When a generic function is called, Luau infers type arguments, for example

```
local x: {number} = reverse({1, 2, 3})
local y: {string} = reverse({"a", "b", "c"})
```

Generic types are used for built-in functions as well as user functions, for example the type of two-argument `table.insert` is:

```
<T>({T}, T) -> ()
```

Note: Functions don’t support having defaults assigned to generics, meaning the following is invalid

```
function meow<T = string>(mrrp: T)
     print(mrrp .. " :3")
end
```

### Union types <a href="#union-types" id="union-types"></a>

A union type represents _one of_ the types in this set. If you try to pass a union onto another thing that expects a _more specific_ type, it will fail.

For example, what if this `string | number` was passed into something that expects `number`, but the passed in value was actually a `string`?

```
local stringOrNumber: string | number = "foo"

local onlyString: string = stringOrNumber -- not ok
local onlyNumber: number = stringOrNumber -- not ok
```

Note: it’s impossible to be able to call a function if there are two or more function types in this union.

### Intersection types <a href="#intersection-types" id="intersection-types"></a>

An intersection type represents _all of_ the types in this set. It’s useful for two main things: to join multiple tables together, or to specify overloadable functions.

```
type XCoord = {x: number}
type YCoord = {y: number}
type ZCoord = {z: number}

type Vector2 = XCoord & YCoord
type Vector3 = XCoord & YCoord & ZCoord

local vec2: Vector2 = {x = 1, y = 2}        -- ok
local vec3: Vector3 = {x = 1, y = 2, z = 3} -- ok
```

```
type SimpleOverloadedFunction = ((string) -> number) & ((number) -> string)

local f: SimpleOverloadedFunction

local r1: number = f("foo") -- ok
local r2: number = f(12345) -- not ok
local r3: string = f("foo") -- not ok
local r4: string = f(12345) -- ok
```

Note: it’s impossible to create an intersection type of some primitive types, e.g. `string & number`, or `string & boolean`, or other variations thereof.

Note: Luau still does not support user-defined overloaded functions. Some of Roblox and Lua 5.1 functions have different function signature, so inherently requires overloaded functions.

### Singleton types (aka literal types) <a href="#singleton-types-aka-literal-types" id="singleton-types-aka-literal-types"></a>

Luau’s type system also supports singleton types, which means it’s a type that represents one single value at runtime. At this time, both string and booleans are representable in types.

> We do not currently support numbers as types. For now, this is intentional.

```
local foo: "Foo" = "Foo" -- ok
local bar: "Bar" = foo   -- not ok
local baz: string = foo  -- ok

local t: true = true -- ok
local f: false = false -- ok
```

This happens all the time, especially through [type refinements](typechecking.md#type-refinements) and is also incredibly useful when you want to enforce program invariants in the type system! See [tagged unions](typechecking.md#tagged-unions) for more information.

### Variadic types <a href="#variadic-types" id="variadic-types"></a>

Luau permits assigning a type to the `...` variadic symbol like any other parameter:

```
local function f(...: number)
end

f(1, 2, 3)     -- ok
f(1, "string") -- not ok
```

`f` accepts any number of `number` values.

In type annotations, this is written as `...T`:

```
type F = (...number) -> ...string
```

### Type packs <a href="#type-packs" id="type-packs"></a>

Multiple function return values as well as the function variadic parameter use a type pack to represent a list of types.

When a type alias is defined, generic type pack parameters can be used after the type parameters:

```
type Signal<T, U...> = { f: (T, U...) -> (), data: T }
```

> Keep in mind that `...T` is a variadic type pack (many elements of the same type `T`), while `U...` is a generic type pack that can contain zero or more types and they don’t have to be the same.

It is also possible for a generic function to reference a generic type pack from the generics list:

```
local function call<T, U...>(s: Signal<T, U...>, ...: U...)
    s.f(s.data, ...)
end
```

Generic types with type packs can be instantiated by providing a type pack:

```
local signal: Signal<string, (number, number, boolean)> = --

call(signal, 1, 2, false)
```

There are also other ways to instantiate types with generic type pack parameters:

```
type A<T, U...> = (T) -> U...

type B = A<number, ...string> -- with a variadic type pack
type C<S...> = A<number, S...> -- with a generic type pack
type D = A<number, ()> -- with an empty type pack
```

Trailing type pack argument can also be provided without parentheses by specifying variadic type arguments:

```
type List<Head, Rest...> = (Head, Rest...) -> ()

type B = List<number> -- Rest... is ()
type C = List<number, string, boolean> -- Rest is (string, boolean)

type Returns<T...> = () -> T...

-- When there are no type parameters, the list can be left empty
type D = Returns<> -- T... is ()
```

Type pack parameters are not limited to a single one, as many as required can be specified:

```
type Callback<Args..., Rets...> = { f: (Args...) -> Rets... }

type A = Callback<(number, string), ...number>
```

### Adding types for faux object oriented programs <a href="#adding-types-for-faux-object-oriented-programs" id="adding-types-for-faux-object-oriented-programs"></a>

One common pattern we see with existing Lua/Luau code is the following object-oriented code. While Luau is capable of inferring a decent chunk of this code, it cannot pin down on the types of `self` when it spans multiple methods.

```
local Account = {}
Account.__index = Account

function Account.new(name, balance)
    local self = {}
    self.name = name
    self.balance = balance

    return setmetatable(self, Account)
end

-- The `self` type is different from the type returned by `Account.new`
function Account:deposit(credit)
    self.balance += credit
end

-- The `self` type is different from the type returned by `Account.new`
function Account:withdraw(debit)
    self.balance -= debit
end

local account = Account.new("Alexander", 500)
```

For example, the type of `Account.new` is `<a, b>(name: a, balance: b) -> { ..., name: a, balance: b, ... }` (snipping out the metatable). For better or worse, this means you are allowed to call `Account.new(5, "hello")` as well as `Account.new({}, {})`. In this case, this is quite unfortunate, so your first attempt may be to add type annotations to the parameters `name` and `balance`.

There’s the next problem: the type of `self` is not shared across methods of `Account`, this is because you are allowed to explicitly opt for a different value to pass as `self` by writing `account.deposit(another_account, 50)`. As a result, the type of `Account:deposit` is `<a, b>(self: { balance: a }, credit: b) -> ()`. Consequently, Luau cannot infer the result of the `+` operation from `a` and `b`, so a type error is reported.

We can see there’s a lot of problems happening here. This is a case where you’ll have to provide some guidance to Luau in the form of annotations today, but the process is straightforward and without repetition. You first specify the type of _data_ you want your class to have, and then you define the class type separately with `setmetatable` (either via `typeof`, or in the New Type Solver, the `setmetatable` type function). From then on, you can explicitly annotate the `self` type of each method with your class type! Note that while the definition is written e.g. `Account.deposit`, you can still call it as `account:deposit(...)`.

```
local Account = {}
Account.__index = Account

type AccountData = {
    name: string,
    balance: number,
}

export type Account = typeof(setmetatable({} :: AccountData, Account))
-- or alternatively, in the new type solver...
-- export type Account = setmetatable<AccountData, typeof(Account)>


-- this return annotation is not required, but ensures that you cannot
-- accidentally make the constructor incompatible with the methods
function Account.new(name, balance): Account
    local self = {}
    self.name = name
    self.balance = balance

    return setmetatable(self, Account)
end

-- this annotation on `self` is the only _required_ annotation.
function Account.deposit(self: Account, credit)
    -- autocomplete on `self` works here!
    self.balance += credit
end

-- this annotation on `self` is the only _required_ annotation.
function Account.withdraw(self: Account, debit)
    -- autocomplete on `self` works here!
    self.balance -= debit
end

local account = Account.new("Hina", 500)
account:deposit(20) -- this still works, and we had autocomplete after hitting `:`!
```

Based on feedback, we plan to restrict the types of all functions defined with `:` syntax to [share their self types](https://rfcs.luau.org/shared-self-types.html). This will enable future versions of this code to work without any explicit `self` annotations because it amounts to having type inference make precisely the assumptions we are encoding with annotations here — namely, that the type of the constructors and the method definitions is intended by the developer to be the same.

### Tagged unions <a href="#tagged-unions" id="tagged-unions"></a>

Tagged unions are just union types! In particular, they’re union types of tables where they have at least _some_ common properties but the structure of the tables are different enough. Here’s one example:

```
type Ok<T> = { type: "ok", value: T }
type Err<E> = { type: "err", error: E }
type Result<T, E> = Ok<T> | Err<E>
```

This `Result<T, E>` type can be discriminated by using type refinements on the property `type`, like so:

```
if result.type == "ok" then
    -- result is known to be Ok<T>
    -- and attempting to index for error here will fail
    print(result.value)
elseif result.type == "err" then
    -- result is known to be Err<E>
    -- and attempting to index for value here will fail
    print(result.error)
end
```

Which works out because `value: T` exists only when `type` is in actual fact `"ok"`, and `error: E` exists only when `type` is in actual fact `"err"`.

### Type refinements <a href="#type-refinements" id="type-refinements"></a>

When we check the type of any lvalue (a global, a local, or a property), what we’re doing is we’re refining the type, hence “type refinement.” The support for this is arbitrarily complex, so go at it!

Here are all the ways you can refine:

1. Truthy test: `if x then` will refine `x` to be truthy.
2. Type guards: `if type(x) == "number" then` will refine `x` to be `number`.
3. Equality: `if x == "hello" then` will refine `x` to be a singleton type `"hello"`.

And they can be composed with many of `and`/`or`/`not`. `not`, just like `~=`, will flip the resulting refinements, that is `not x` will refine `x` to be falsy.

The `assert(..)` function may also be used to refine types instead of `if/then`.

Using truthy test:

```
local maybeString: string? = nil

if maybeString then
    local onlyString: string = maybeString -- ok
    local onlyNil: nil = maybeString       -- not ok
end

if not maybeString then
    local onlyString: string = maybeString -- not ok
    local onlyNil: nil = maybeString       -- ok
end
```

Using `type` test:

```
local stringOrNumber: string | number = "foo"

if type(stringOrNumber) == "string" then
    local onlyString: string = stringOrNumber -- ok
    local onlyNumber: number = stringOrNumber -- not ok
end

if type(stringOrNumber) ~= "string" then
    local onlyString: string = stringOrNumber -- not ok
    local onlyNumber: number = stringOrNumber -- ok
end
```

Using equality test:

```
local myString: string = f()

if myString == "hello" then
    local hello: "hello" = myString -- ok because it is absolutely "hello"!
    local copy: string = myString   -- ok
end
```

And as said earlier, we can compose as many of `and`/`or`/`not` as we wish with these refinements:

```
local function f(x: any, y: any)
    if (x == "hello" or x == "bye") and type(y) == "string" then
        -- x is of type "hello" | "bye"
        -- y is of type string
    end

    if not (x ~= "hi") then
        -- x is of type "hi"
    end
end
```

`assert` can also be used to refine in all the same ways:

```
local stringOrNumber: string | number = "foo"

assert(type(stringOrNumber) == "string")

local onlyString: string = stringOrNumber -- ok
local onlyNumber: number = stringOrNumber -- not ok
```

### Type casts <a href="#type-casts" id="type-casts"></a>

Expressions may be typecast using `::`. Typecasting is useful for specifying the type of an expression when the automatically inferred type is too generic.

For example, consider the following table constructor where the intent is to store a table of names:

```
local myTable = {names = {}}
table.insert(myTable.names, 42)         -- Inserting a number ought to cause a type error, but doesn't
```

In order to specify the type of the `names` table a typecast may be used:

```
local myTable = {names = {} :: {string}}
table.insert(myTable.names, 42)         -- not ok, invalid 'number' to 'string' conversion
```

A typecast itself is also type checked to ensure that one of the conversion operands is the subtype of the other or `any`:

```
local numericValue = 1
local value = numericValue :: any             -- ok, all expressions may be cast to 'any'
local flag = numericValue :: boolean          -- not ok, invalid 'number' to 'boolean' conversion
```

When typecasting a variadic or the result of a function with multiple returns, only the first value will be preserved. The rest will be discarded.

```
function returnsMultiple(...): (number, number, number)
    print(... :: string) -- "x"
    return 1, 2, 3
end

print(returnsMultiple("x", "y", "z")) -- 1, 2, 3
print(returnsMultiple("x", "y", "z") :: number) -- 1
```

### Roblox types <a href="#roblox-types" id="roblox-types"></a>

Roblox supports a rich set of classes and data types, [documented here](https://developer.roblox.com/en-us/api-reference). All of them are readily available for the type checker to use by their name (e.g. `Part` or `RaycastResult`).

When one type inherits from another type, the type checker models this relationship and allows to cast a subclass to the parent class implicitly, so you can pass a `Part` to a function that expects an `Instance`.

All enums are also available to use by their name as part of the `Enum` type library, e.g. `local m: Enum.Material = part.Material`.

We can automatically deduce what calls like `Instance.new` and `game:GetService` are supposed to return:

```
local part = Instance.new("Part")
local basePart: BasePart = part
```

Finally, Roblox types can be refined using `IsA`:

```
local function getText(x : Instance) : string
    if x:IsA("TextLabel") or x:IsA("TextButton") or x:IsA("TextBox") then
        return child.Text
    end
    return ""
end
```

Note that many of these types provide some properties and methods in both lowerCase and UpperCase; the lowerCase variants are deprecated, and the type system will ask you to use the UpperCase variants instead.

### Module interactions <a href="#module-interactions" id="module-interactions"></a>

Let’s say that we have two modules, `Foo` and `Bar`. Luau will try to resolve the paths if it can find any `require` in any scripts. In this case, when you say `script.Parent.Bar`, Luau will resolve it as: relative to this script, go to my parent and get that script named Bar.

```
-- Module Foo
local Bar = require(script.Parent.Bar)

local baz1: Bar.Baz = 1     -- not ok
local baz2: Bar.Baz = "foo" -- ok

print(Bar.Quux)         -- ok
print(Bar.FakeProperty) -- not ok

Bar.NewProperty = true -- not ok
```

```
-- Module Bar
export type Baz = string

local module = {}

module.Quux = "Hello, world!"

return module
```

There are some caveats here though. For instance, the require path must be resolvable statically, otherwise Luau cannot accurately type check it.

#### Cyclic module dependencies <a href="#cyclic-module-dependencies" id="cyclic-module-dependencies"></a>

Cyclic module dependencies can cause problems for the type checker. In order to break a module dependency cycle a typecast of the module to `any` may be used:

```
local myModule = require(MyModule) :: any
```

### Type functions <a href="#type-functions" id="type-functions"></a>

Type functions are functions that run during analysis time and operate on types, instead of runtime values. They can use the [types](typechecking.md#types-library) library to transform existing types or create new ones.

Here’s a simplified implementation of the builtin type function `keyof`. It takes a table type and returns its property names as a [union](about:blank/typecheck#union-types) of [singletons](about:blank/typecheck#singleton-types-aka-literal-types).

```
type function simple_keyof(ty)
    -- Ignoring unions or intersections of tables for simplicity.
    if not ty:is("table") then
        error("Can only call keyof on tables.")
    end

    local union = nil

    for property in ty:properties() do
        union = if union then types.unionof(union, property) else property
    end

    return if union then union else types.singleton(nil)
end

type person = {
    name: string,
    age: number,
}
--- keys = "age" | "name"
type keys = simple_keyof<person>
```

#### Type function environment <a href="#type-function-environment" id="type-function-environment"></a>

In addition to the [types](typechecking.md#types-library) library, type functions have access to:

* `assert`, `error`, `print`
* `next`, `ipairs`, `pairs`
* `select`, `unpack`
* `getmetatable`, `setmetatable`
* `rawget`, `rawset`, `rawlen`, `raweq`
* `tonumber`, `tostring`
* `type`, `typeof`
* `math` library
* `table` library
* `string` library
* `bit32` library
* `utf8` library
* `buffer` library

### types library <a href="#types-library" id="types-library"></a>

The `types` library is used to create and transform types, and can only be used within [type functions](typechecking.md#type-functions).

#### `types` library properties <a href="#types-library-properties" id="types-library-properties"></a>

```
types.any
```

The [any](about:blank/typecheck#any-type) `type`.

```
types.unknown
```

The [unknown](about:blank/typecheck#unknown-type) `type`.

```
types.never
```

The [never](about:blank/typecheck#never-type) `type`.

```
types.boolean
```

The boolean `type`.

```
types.buffer
```

The [buffer](about:blank/library#buffer-library) `type`.

```
types.number
```

The number `type`.

```
types.string
```

The string `type`.

```
types.thread
```

The thread `type`.

### `types` library functions <a href="#types-library-functions" id="types-library-functions"></a>

```
types.singleton(arg: string | boolean | nil): type
```

Returns the [singleton](about:blank/typecheck#singleton-types-aka-literal-types) type of the argument.

```
types.negationof(arg: type): type
```

Returns an immutable negation of the argument type.

```
types.optional(arg: type): type
```

Returns a version of the given type that is now optional.

* If the given type is a [union type](about:blank/\(typecheck#union-types\)), `nil` will be added unconditionally as a component.
* Otherwise, the result will be a union of the given type and the `nil` type.

```
types.unionof(first: type, second: type, ...: type): type
```

Returns an immutable [union](about:blank/typecheck#union-types) of two or more arguments.

```
types.intersectionof(first: type, second: type, ...: type): type
```

Returns an immutable [intersection](about:blank/typecheck#intersection-types) of two or more arguments.

```
types.newtable(props: { [type]: type | { read: type?, write: type? } }?, indexer: { index: type, readresult: type, writeresult: type? }?, metatable: type?): type
```

Returns a fresh, mutable table `type`. Property keys must be string singleton `type`s. The table’s metatable is set if one is provided.

```
types.newfunction(parameters: { head: {type}?, tail: type? }, returns: { head: {type}?, tail: type? }?, generics: {type}?): type
```

Returns a fresh, mutable function `type`, using the ordered parameters of `head` and the variadic tail of `tail`.

```
types.copy(arg: type): type
```

Returns a deep copy of the argument type.

```
types.generic(name: string?, ispack: boolean?): type
```

Creates a [generic](about:blank/typecheck#generic-functions) named `name`. If `ispack` is `true`, the result is a [generic pack](about:blank/typecheck#type-packs).

#### `type` instance <a href="#type-instance" id="type-instance"></a>

`type` instances can have extra properties and methods described in subsections depending on its tag.

```
type.tag: "nil" | "unknown" | "never" | "any" | "boolean" | "number" | "string" | "singleton" | "negation" | "union" | "intersection" | "table" | "function" | "class" | "thread" | "buffer"
```

An immutable property holding the type’s tag.

```
__eq(arg: type): boolean
```

Overrides the `==` operator to return `true` if `self` is syntactically equal to `arg`. This excludes semantically equivalent types, `true | false` is unequal to `boolean`.

```
type:is(arg: "nil" | "unknown" | "never" | "any" | "boolean" | "number" | "string" | "singleton" | "negation" | "union" | "intersection" | "table" | "function" | "class" | "thread" | "buffer")
```

Returns `true` if `self` has the argument as its tag.

#### Singleton `type` instance <a href="#singleton-type-instance" id="singleton-type-instance"></a>

```
singletontype:value(): boolean | nil | "string"
```

Returns the singleton’s actual value, like `true` for `types.singleton(true)`.

#### Generic `type` instance <a href="#generic-type-instance" id="generic-type-instance"></a>

```
generictype:name(): string?
```

Returns the name of the [generic](about:blank/typecheck#generic-functions) or `nil` if it has no name.

```
generictype:ispack(): boolean
```

Returns `true` if the [generic](about:blank/typecheck#generic-functions) is a [pack](about:blank/typecheck#type-packs), or `false` otherwise.

#### Table `type` instance <a href="#table-type-instance" id="table-type-instance"></a>

```
tabletype:setproperty(key: type, value: type?)
```

Sets the type of the property for the given `key`, using the same type for both reading from and writing to the table.

* `key` is expected to be a string singleton type, naming the property.
* `value` will be set as both the `read type` and `write type` of the property.
* If `value` is `nil`, the property is removed.

```
tabletype:setreadproperty(key: type, value: type?)
```

Sets the type for reading from the property named by `key`, leaving the type for writing this property as-is.

* `key` is expected to be a string singleton type, naming the property.
* `value` will be set as the `read type`, the `write type` will be unchanged.
* If `key` is not already present, only a `read type` will be set, making the property read-only.
* If `value` is `nil`, the property is removed.

```
tabletype:setwriteproperty(key: type, value: type?)
```

Sets the type for writing to the property named by `key`, leaving the type for reading this property as-is.

* `key` is expected to be a string singleton type, naming the property.
* `value` will be set as the `write type`, the `read type` will be unchanged.
* If `key` is not already present, only a `write type` will be set, making the property write-only.
* If `value` is `nil`, the property is removed.

```
tabletype:readproperty(key: type): type?
```

Returns the type used for reading values from this property, or `nil` if the property doesn’t exist.

```
tabletype:writeproperty(key: type): type?
```

Returns the type used for writing values to this property, or `nil` if the property doesn’t exist.

```
tabletype:properties(): { [type]: { read: type?, write: type? } }
```

Returns a table mapping property keys to their read and write types.

```
tabletype:setindexer(index: type, result: type)
```

Sets the table’s indexer, using the same type for reads and writes.

```
tabletype:setreadindexer(index: type, result: type)
```

Sets the type resulting from reading from this table via indexing.

```
tabletype:setwriteindexer(index: type, result: type)
```

Sets the type for writing to this table via indexing.

```
tabletype:indexer(): { index: type, readresult: type, writeresult: type }
```

Returns the table’s indexer as a table, or `nil` if it doesn’t exist.

```
tabletype:readindexer(): { index: type, result: type }?
```

Returns the table’s indexer using the result’s read type, or `nil` if it doesn’t exist.

```
tabletype:writeindexer()
```

Returns the table’s indexer using the result’s write type, or `nil` if it doesn’t exist.

```
tabletype:setmetatable(arg: type)
```

Sets the table’s metatable.

```
tabletype:metatable(): type?
```

Gets the table’s metatable, or `nil` if it doesn’t exist.

#### Function `type` instance <a href="#function-type-instance" id="function-type-instance"></a>

```
functiontype:setparameters(head: {type}?, tail: type?)
```

Sets the function’s parameters, with the ordered parameters in `head` and the variadic tail in `tail`.

```
functiontype:parameters(): { head: {type}?, tail: type? }
```

Returns the function’s parameters, with the ordered parameters in `head` and the variadic tail in `tail`.

```
functiontype:setreturns(head: {type}?, tail: type?)
```

Sets the function’s return types, with the ordered parameters in `head` and the variadic tail in `tail`.

```
functiontype:returns(): { head: {type}?, tail: type? }
```

Returns the function’s return types, with the ordered parameters in `head` and the variadic tail in `tail`.

```
functiontype:generics(): {type}
```

Returns an array of the function’s [generic](about:blank/typecheck#generic-functions) `type`s.

```
functiontype:setgenerics(generics: {type}?)
```

Sets the function’s [generic](about:blank/typecheck#generic-functions) `type`s.

#### Negation `type` instance <a href="#negation-type-instance" id="negation-type-instance"></a>

```
type:inner(): type
```

Returns the `type` being negated.

#### Union `type` instance <a href="#union-type-instance" id="union-type-instance"></a>

```
uniontype:components(): {type}
```

Returns an array of the [unioned](about:blank/typecheck#union-types) types.

#### Intersection `type` instance <a href="#intersection-type-instance" id="intersection-type-instance"></a>

```
intersectiontype:components()
```

Returns an array of the [intersected](about:blank/typecheck#intersection-types) types.

#### Class `type` instance <a href="#class-type-instance" id="class-type-instance"></a>

```
classtype:properties(): { [type]: { read: type?, write: type? } }
```

Returns the properties of the class with their respective `read` and `write` types.

```
classtype:readparent(): type?
```

Returns the type of reading this class’ parent, or returns `nil` if the parent class doesn’t exist.

```
classtype:writeparent(): type?
```

Returns the type for writing to this class’ parent, or returns `nil` if the parent class doesn’t exist.

```
classtype:metatable(): type?
```

Returns the class’ metatable, or `nil` if it doesn’t exist.

```
classtype:indexer(): { index: type, readresult: type, writeresult: type }?
```

Returns the class’ indexer, or `nil` if it doesn’t exist.

```
classtype:readindexer(): { index: type, result: type }?
```

Returns result type of reading from the class via indexing, or `nil` if it doesn’t exist.

```
classtype:writeindexer(): { index: type, result: type }?
```

Returns the type for writing to the class via indexing, or `nil` if it doesn’t exist.
