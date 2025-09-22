# bit32

All functions in the `bit32` library treat input numbers as 32-bit unsigned integers in `[0..4294967295]` range. The bit positions start at 0 where 0 corresponds to the least significant bit.

## arshift

```lua
function bit32.arshift(n: number, i: number): number
```

Shifts `n` by `i` bits to the right (if `i` is negative, a left shift is performed instead). The most significant bit of `n` is propagated during the shift. When `i` is larger than 31, returns an integer with all bits set to the sign bit of `n`. When `i` is smaller than `-31`, 0 is returned.

## band

```lua
function bit32.band(args: ...number): number
```

Performs a bitwise `and` of all input numbers and returns the result. If the function is called with no arguments, an integer with all bits set to 1 is returned.

## bnot

```lua
function bit32.bnot(n: number): number
```

Returns a bitwise negation of the input number.

## bor

```lua
function bit32.bor(args: ...number): number
```

Performs a bitwise `or` of all input numbers and returns the result. If the function is called with no arguments, zero is returned.

## bxor

```lua
function bit32.bxor(args: ...number): number
```

Performs a bitwise `xor` (exclusive or) of all input numbers and returns the result. If the function is called with no arguments, zero is returned.

## btest

```lua
function bit32.btest(args: ...number): boolean
```

Perform a bitwise `and` of all input numbers, and return `true` iff the result is not 0. If the function is called with no arguments, `true` is returned.

## extract

```lua
function bit32.extract(n: number, f: number, w: number?): number
```

Extracts bits of `n` at position `f` with a width of `w`, and returns the resulting integer. `w` defaults to `1`, so a two-argument version of `extract` returns the bit value at position `f`. Bits are indexed starting at 0. Errors if `f` and `f+w-1` are not between 0 and 31.

## lrotate

```lua
function bit32.lrotate(n: number, i: number): number
```

Rotates `n` to the left by `i` bits (if `i` is negative, a right rotate is performed instead); the bits that are shifted past the bit width are shifted back from the right.

## lshift

```lua
function bit32.lshift(n: number, i: number): number
```

Shifts `n` to the left by `i` bits (if `i` is negative, a right shift is performed instead). When `i` is outside of `[-31..31]` range, returns 0.

## replace

```lua
function bit32.replace(n: number, r: number, f: number, w: number?): number
```

Replaces bits of `n` at position `f` and width `w` with `r`, and returns the resulting integer. `w` defaults to `1`, so a three-argument version of `replace` changes one bit at position `f` to `r` (which should be 0 or 1) and returns the result. Bits are indexed starting at 0. Errors if `f` and `f+w-1` are not between 0 and 31.

## rrotate

```lua
function bit32.rrotate(n: number, i: number): number
```

Rotates `n` to the right by `i` bits (if `i` is negative, a left rotate is performed instead); the bits that are shifted past the bit width are shifted back from the left.

## rshift

```lua
function bit32.rshift(n: number, i: number): number
```

Shifts `n` to the right by `i` bits (if `i` is negative, a left shift is performed instead). When `i` is outside of `[-31..31]` range, returns 0.

## countlz

```lua
function bit32.countlz(n: number): number
```

Returns the number of consecutive zero bits in the 32-bit representation of `n` starting from the left-most (most significant) bit. Returns 32 if `n` is zero.

## countrz

```lua
function bit32.countrz(n: number): number
```

Returns the number of consecutive zero bits in the 32-bit representation of `n` starting from the right-most (least significant) bit. Returns 32 if `n` is zero.

## byteswap

```lua
function bit32.byteswap(n: number): number
```

Returns `n` with the order of the bytes swapped.
