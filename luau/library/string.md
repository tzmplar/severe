# string

## byte

```lua
function string.byte(s: string, f: number?, t: number?): ...number
```

Returns the numeric code of every byte in the input string with indices in range `[f..t]`. `f` defaults to 1 and `t` defaults to `f`, so a two-argument version of this function returns a single number. If the function is called with a single argument and the argument is out of range, the function returns no values.

## char

```lua
function string.char(args: ...number): string
```

Returns the string that contains a byte for every input number; all inputs must be integers in `[0..255]` range.

## find

```lua
function string.find(s: string, p: string, init: number?, plain: boolean?): (number?, number?, ...string)
```

Tries to find an instance of pattern `p` in the string `s`, starting from position `init` (defaults to 1). When `plain` is true, the search is using raw (case-sensitive) string equality, otherwise `p` should be a [string pattern](https://www.lua.org/manual/5.3/manual.html#6.4.1). If a match is found, returns the position of the match and the length of the match, followed by the pattern captures; otherwise returns `nil`.

## format

```lua
function string.format(s: string, args: ...any): string
```

Returns a formatted version of the input arguments using a [printf-style format string](https://en.cppreference.com/w/c/io/fprintf) `s`. The following format characters are supported:

* `c`: expects an integer number and produces a character with the corresponding character code
* `d`, `i`, `u`: expects an integer number and produces the decimal representation of that number
* `o`: expects an integer number and produces the octal representation of that number
* `x`, `X`: expects an integer number and produces the hexadecimal representation of that number, using lower case or upper case hexadecimal characters
* `e`, `E`, `f`, `g`, `G`: expects a number and produces the floating point representation of that number, using scientific or decimal representation
* `q`: expects a string and produces the same string quoted using double quotation marks, with escaped special characters if necessary
* `s`: expects a string and produces the same string verbatim

The formats support modifiers `-`, `+`, space, `#` and `0`, as well as field width and precision modifiers - with the exception of `*`.

## gmatch

```lua
function string.gmatch(s: string, p: string): <iterator>
```

Produces an iterator function that, when called repeatedly explicitly or via `for` loop, produces matches of string `s` with [string pattern](https://www.lua.org/manual/5.3/manual.html#6.4.1) `p`. For every match, the captures within the pattern are returned if present (if a pattern has no captures, the entire matching substring is returned instead).

## gsub

```lua
function string.gsub(s: string, p: string, f: function | table | string, maxs: number?): (string, number)
```

For every match of [string pattern](https://www.lua.org/manual/5.3/manual.html#6.4.1) `p` in `s`, replace the match according to `f`. The substitutions stop after the limit of `maxs`, and the function returns the resulting string followed by the number of substitutions.

When `f` is a string, the substitution uses the string as a replacement. When `f` is a table, the substitution uses the table element with key corresponding to the first pattern capture, if present, and entire match otherwise. Finally, when `f` is a function, the substitution uses the result of calling `f` with call pattern captures, or entire matching substring if no captures are present.

## len

```lua
function string.len(s: string): number
```

Returns the number of bytes in the string (equivalent to `#s`).

## lower

```lua
function string.lower(s: string): string
```

Returns a string where each byte corresponds to the lower-case ASCII version of the input byte in the source string.

## match

```lua
function string.match(s: string, p: string, init: number?): ...string?
```

Tries to find an instance of pattern `p` in the string `s`, starting from position `init` (defaults to 1). `p` should be a [string pattern](https://www.lua.org/manual/5.3/manual.html#6.4.1). If a match is found, returns all pattern captures, or entire matching substring if no captures are present, otherwise returns `nil`.

## rep

```lua
function string.rep(s: string, n: number): string
```

Returns the input string `s` repeated `n` times. Returns an empty string if `n` is zero or negative.

## reverse

```lua
function string.reverse(s: string): string
```

Returns the string with the order of bytes reversed compared to the original. Note that this only works if the input is a binary or ASCII string.

## sub

```lua
function string.sub(s: string, f: number, t: number?): string
```

Returns a substring of the input string with the byte range `[f..t]`; `t` defaults to `#s`, so a two-argument version returns a string suffix.

## upper

```lua
function string.upper(s: string): string
```

Returns a string where each byte corresponds to the upper-case ASCII version of the input byte in the source string.

## split

```lua
function string.split(s: string, sep: string?): {string}
```

Splits the input string using `sep` as a separator (defaults to `","`) and returns the resulting substrings. If separator is empty, the input string is split into separate one-byte strings.

## pack

```lua
function string.pack(f: string, args: ...any): string
```

Given a [pack format string](https://www.lua.org/manual/5.3/manual.html#6.4.2), encodes all input parameters according to the packing format and returns the resulting string. Note that Luau uses fixed sizes for all types that have platform-dependent size in Lua 5.x: short is 16 bit, long is 64 bit, integer is 32-bit and size\_t is 32 bit for the purpose of string packing.

## packsize

```lua
function string.packsize(f: string): number
```

Given a [pack format string](https://www.lua.org/manual/5.3/manual.html#6.4.2), returns the size of the resulting packed representation. The pack format can't use variable-length format specifiers. Note that Luau uses fixed sizes for all types that have platform-dependent size in Lua 5.x: short is 16 bit, long is 64 bit, integer is 32-bit and size\_t is 32 bit for the purpose of string packing.

## unpack

```lua
function string.unpack(f: string, s: string): ...any
```

Given a [pack format string](https://www.lua.org/manual/5.3/manual.html#6.4.2), decodes the input string according to the packing format and returns all resulting values. Note that Luau uses fixed sizes for all types that have platform-dependent size in Lua 5.x: short is 16 bit, long is 64 bit, integer is 32-bit and size\_t is 32 bit for the purpose of string packing.
