# table

## concat

```lua
function table.concat(a: {string}, sep: string?, f: number?, t: number?): string
```

Concatenate all elements of `a` with indices in range `[f..t]` together, using `sep` as a separator if present. `f` defaults to 1 and `t` defaults to `#a`.

## foreach

```lua
function table.foreach<K, V, R>(t: { [K]: V }, f: (K, V) -> R?): R?
```

Iterates over all elements of the table in unspecified order; for each key-value pair, calls `f` and returns the result of `f` if it's non-nil. If all invocations of `f` returned `nil`, returns no values. This function has been deprecated and is not recommended for use in new code; use `for` loop instead.

## foreachi

```lua
function table.foreachi<V, R>(t: {V}, f: (number, V) -> R?): R?
```

Iterates over numeric keys of the table in `[1..#t]` range in order; for each key-value pair, calls `f` and returns the result of `f` if it's non-nil. If all invocations of `f` returned `nil`, returns no values. This function has been deprecated and is not recommended for use in new code; use `for` loop instead.

## getn

```lua
function table.getn<V>(t: {V}): number
```

Returns the length of table `t`. This function has been deprecated and is not recommended for use in new code; use `#t` instead.

## maxn

```lua
function table.maxn<V>(t: {V}): number
```

Returns the maximum numeric key of table `t`, or zero if the table doesn't have numeric keys.

## insert

```lua
function table.insert<V>(t: {V}, v: V)
function table.insert<V>(t: {V}, i: number, v: V)
```

When using a two-argument version, appends the value to the array portion of the table (equivalent to `t[#t+1] = v`). When using a three-argument version, inserts the value at index `i` and shifts values at indices after that by 1. `i` should be in `[1..#t]` range.

## remove

```lua
function table.remove<V>(t: {V}, i: number?): V?
```

Removes element `i` from the table and shifts values at indices after that by 1. If `i` is not specified, removes the last element of the table. `i` should be in `[1..#t]` range. Returns the value of the removed element, or `nil` if no element was removed (e.g. table was empty).

## sort

```lua
function table.sort<V>(t: {V}, f: ((V, V) -> boolean)?)
```

Sorts the table `t` in ascending order, using `f` as a comparison predicate: `f` should return `true` iff the first parameter should be before the second parameter in the resulting table. When `f` is not specified, builtin less-than comparison is used instead. The comparison predicate must establish a strict weak ordering - sort results are undefined otherwise.

## pack

```lua
function table.pack<V>(args: ...V): { [number]: V, n: number }
```

Returns a table that consists of all input arguments as array elements, and `n` field that is set to the number of inputs.

## unpack

```lua
function table.unpack<V>(a: {V}, f: number?, t: number?): ...V
```

Returns all values of `a` with indices in `[f..t]` range. `f` defaults to 1 and `t` defaults to `#a`. Note that if you want to unpack varargs packed with `table.pack` you have to specify the index fields because `table.unpack` doesn't automatically use the `n` field that `table.pack` creates. Example usage for packed varargs: `table.unpack(args, 1, args.n)`

## move

```lua
function table.move<V>(a: {V}, f: number, t: number, d: number, tt: {V}?)
```

Copies elements in range `[f..t]` from table `a` to table `tt` if specified and `a` otherwise, starting from the index `d`.

## create

```lua
function table.create<V>(n: number, v: V?): {V}
```

Creates a table with `n` elements; all of them (range `[1..n]`) are set to `v`. When `v` is nil or omitted, the returned table is empty but has preallocated space for `n` elements which can make subsequent insertions faster. Note that preallocation is only performed for the array portion of the table - using `table.create` on dictionaries is counter-productive.

## find

```lua
function table.find<V>(t: {V}, v: V, init: number?): number?
```

Find the first element in the table that is equal to `v` and returns its index; the traversal stops at the first `nil`. If the element is not found, `nil` is returned instead. The traversal starts at index `init` if specified, otherwise 1.

## clear

```lua
function table.clear(t: table)
```

Removes all elements from the table while preserving the table capacity, so future assignments don't need to reallocate space.

## freeze

```lua
function table.freeze(t: table): table
```

Given a non-frozen table, freezes it such that all subsequent attempts to modify the table or assign its metatable raise an error. If the input table is already frozen or has a protected metatable, the function raises an error; otherwise it returns the input table. Note that the table is frozen in-place and is not being copied. Additionally, only `t` is frozen, and keys/values/metatable of `t` don't change their state and need to be frozen separately if desired.

## isfrozen

```lua
function table.isfrozen(t: table): boolean
```

Returns `true` iff the input table is frozen.

## clone

```lua
function table.clone(t: table): table
```

Returns a copy of the input table that has the same metatable, same keys and values, and is not frozen even if `t` was. The copy is shallow: implementing a deep recursive copy automatically is challenging, and often only certain keys need to be cloned recursively which can be done after the initial clone by modifying the resulting table.
