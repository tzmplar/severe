# utf8

Strings in Luau can contain arbitrary bytes; however, in many applications strings representing text contain UTF8 encoded data by convention, that can be inspected and manipulated using `utf8` library.

## offset

```lua
function utf8.offset(s: string, n: number, i: number?): number?
```

Returns the byte offset of the Unicode codepoint number `n` in the string, starting from the byte position `i`. When the character is not found, returns `nil` instead.

## codepoint

```lua
function utf8.codepoint(s: string, i: number?, j: number?): ...number
```

Returns a number for each Unicode codepoint in the string with the starting byte offset in `[i..j]` range. `i` defaults to 1 and `j` defaults to `i`, so a two-argument version of this function returns the Unicode codepoint that starts at byte offset `i`.

## char

```lua
function utf8.char(args: ...number): string
```

Creates a string by concatenating Unicode codepoints for each input number.

## len

```lua
function utf8.len(s: string, i: number?, j: number?): number?
```

Returns the number of Unicode codepoints with the starting byte offset in `[i..j]` range, or `nil` followed by the first invalid byte position if the input string is malformed. `i` defaults to 1 and `j` defaults to `#s`, so `utf8.len(s)` returns the number of Unicode codepoints in string `s` or `nil` if the string is malformed.

## codes

```lua
function utf8.codes(s: string): <iterator>
```

Returns an iterator that, when used in `for` loop, produces the byte offset and the codepoint for each Unicode codepoints that `s` consists of.
