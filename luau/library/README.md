# Library

## Globals

While most library functions are provided as part of a library like `table`, a few global functions are exposed without extra namespacing.

### assert

```lua
function assert<T>(value: T, message: string?): T
```

`assert` checks if the value is truthy; if it's not (which means it's `false` or `nil`), it raises an error. The error message can be customized with an optional parameter. Upon success the function returns the `value` argument.

### error

```lua
function error(obj: any, level: number?)
```

`error` raises an error with the specified object. Note that errors don't have to be strings, although they often are by convention; various error handling mechanisms like `pcall` preserve the error type. When `level` is specified, the error raised is turned into a string that contains call frame information for the caller at level `level`, where `1` refers to the function that called `error`. This can be useful to attribute the errors to callers, for example `error("Expected a valid object", 2)` highlights the caller of the function that called `error` instead of the function itself in the callstack.

### gcinfo

```lua
function gcinfo(): number
```

`gcinfo` returns the total heap size in kilobytes, which includes bytecode objects, global tables as well as the script-allocated objects. Note that Luau uses an incremental garbage collector, and as such at any given point in time the heap may contain both reachable and unreachable objects. The number returned by `gcinfo` reflects the current heap consumption from the operating system perspective and can fluctuate over time as garbage collector frees objects.

### getfenv

```lua
function getfenv(target: (function | number)?): table
```

Returns the environment table for target function; when `target` is not a function, it must be a number corresponding to the caller stack index, where 1 means the function that calls `getfenv`, and the environment table is returned for the corresponding function from the call stack. When `target` is omitted it defaults to `1`, so `getfenv()` returns the environment table for the calling function.

### getmetatable

```lua
function getmetatable(obj: any): table?
```

Returns the metatable for the specified object; when object is not a table or a userdata, the returned metatable is shared between all objects of the same type. Note that when metatable is protected (has a `__metatable` key), the value corresponding to that key is returned instead and may not be a table.

### next

```lua
function next<K, V>(t: { [K]: V }, i: K?): (K, V)?
```

Given the table `t`, returns the next key-value pair after `i` in the table traversal order, or nothing if `i` is the last key. When `i` is `nil`, returns the first key-value pair instead.

### newproxy

```lua
function newproxy(mt: boolean?): userdata
```

Creates a new untyped userdata object; when `mt` is true, the new object has an empty metatable that can be modified using `getmetatable`.

### print

```lua
function print(args: ...any)
```

Prints all arguments to the standard output, using Tab as a separator.

### rawequal

```lua
function rawequal(a: any, b: any): boolean
```

Returns true iff `a` and `b` have the same type and point to the same object (for garbage collected types) or are equal (for value types).

### rawget

```lua
function rawget<K, V>(t: { [K]: V }, k: K): V?
```

Performs a table lookup with index `k` and returns the resulting value, if present in the table, or nil. This operation bypasses metatables/`__index`.

### rawset

```lua
function rawset<K, V>(t: { [K] : V }, k: K, v: V)
```

Assigns table field `k` to the value `v`. This operation bypasses metatables/`__newindex`.

### select

```lua
function select<T>(i: string, args: ...T): number
function select<T>(i: number, args: ...T): ...T
```

When called with `'#'` as the first argument, returns the number of remaining parameters passed. Otherwise, returns the subset of parameters starting with the specified index. Index can be specified from the start of the arguments (using 1 as the first argument), or from the end (using -1 as the last argument).

### setfenv

```lua
function setfenv(target: function | number, env: table)
```

Changes the environment table for target function to `env`; when `target` is not a function, it must be a number corresponding to the caller stack index, where 1 means the function that calls `setfenv`, and the environment table is returned for the corresponding function from the call stack.

### setmetatable

```lua
function setmetatable(t: table, mt: table?)
```

Changes metatable for the given table. Note that unlike `getmetatable`, this function only works on tables. If the table already has a protected metatable (has a `__metatable` field), this function errors.

### tonumber

```lua
function tonumber(s: string, base: number?): number?
```

Converts the input string to the number in base `base` (default 10) and returns the resulting number. If the conversion fails (that is, if the input string doesn't represent a valid number in the specified base), returns `nil` instead.

### tostring

```lua
function tostring(obj: any): string
```

Converts the input object to string and returns the result. If the object has a metatable with `__tostring` field, that method is called to perform the conversion.

### type

```lua
function type(obj: any): string
```

Returns the type of the object, which is one of `"nil"`, `"boolean"`, `"number"`, `"vector"`, `"string"`, `"table"`, `"function"`, `"userdata"`, `"thread"`, or `"buffer"`.

### typeof

```lua
function typeof(obj: any): string
```

Returns the type of the object; for userdata objects that have a metatable with the `__type` field _and_ are defined by the host (not `newproxy`), returns the value for that key. For custom userdata objects, such as ones returned by `newproxy`, this function returns `"userdata"` to make sure host-defined types can not be spoofed.

### ipairs

```lua
function ipairs(t: table): <iterator>
```

Returns the triple (generator, state, nil) that can be used to traverse the table using a `for` loop. The traversal results in key-value pairs for the numeric portion of the table; key starts from 1 and increases by 1 on each iteration. The traversal terminates when reaching the first `nil` value (so `ipairs` can't be used to traverse array-like tables with holes).

### pairs

```lua
function pairs(t: table): <iterator>
```

Returns the triple (generator, state, nil) that can be used to traverse the table using a `for` loop. The traversal results in key-value pairs for all keys in the table, numeric and otherwise, but doesn't have a defined order.

### pcall

```lua
function pcall(f: function, args: ...any): (boolean, ...any)
```

Calls function `f` with parameters `args`. If the function succeeds, returns `true` followed by all return values of `f`. If the function raises an error, returns `false` followed by the error object. Note that `f` can yield, which results in the entire coroutine yielding as well.

### xpcall

```lua
function xpcall(f: function, e: function, args: ...any): (boolean, ...any)
```

Calls function `f` with parameters `args`. If the function succeeds, returns `true` followed by all return values of `f`. If the function raises an error, calls `e` with the error object as an argument, and returns `false` followed by the first return value of `e`. Note that `f` can yield, which results in the entire coroutine yielding as well. `e` can neither yield nor error - if it does raise an error, `xpcall` returns with `false` followed by a special error message.

### unpack

```lua
function unpack<V>(a: {V}, f: number?, t: number?): ...V
```

Returns all values of `a` with indices in `[f..t]` range. `f` defaults to 1 and `t` defaults to `#a`. Note that this is equivalent to `table.unpack`.

## Libraries

* bit32
* buffer
* coroutine
* debug
* math
* string
* table
* utf8
* vector
* os
