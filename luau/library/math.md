# math

## abs

```lua
function math.abs(n: number): number
```

Returns the absolute value of `n`. Returns NaN if the input is NaN.

## acos

```lua
function math.acos(n: number): number
```

Returns the arc cosine of `n`, expressed in radians. Returns a value in `[0, pi]` range. Returns NaN if the input is not in `[-1, +1]` range.

## asin

```lua
function math.asin(n: number): number
```

Returns the arc sine of `n`, expressed in radians. Returns a value in `[-pi/2, +pi/2]` range. Returns NaN if the input is not in `[-1, +1]` range.

## atan2

```lua
function math.atan2(y: number, x: number): number
```

Returns the arc tangent of `y/x`, expressed in radians. The function takes into account the sign of both arguments in order to determine the quadrant. Returns a value in `[-pi, pi]` range.

## atan

```lua
function math.atan(n: number): number
```

Returns the arc tangent of `n`, expressed in radians. Returns a value in `[-pi/2, pi-2]` range.

## ceil

```lua
function math.ceil(n: number): number
```

Rounds `n` upwards to the next integer boundary.

## cosh

```lua
function math.cosh(n: number): number
```

Returns the hyperbolic cosine of `n`.

## cos

```lua
function math.cos(n: number): number
```

Returns the cosine of `n`, which is an angle in radians. Returns a value in `[0, 1]` range.

## deg

```lua
function math.deg(n: number): number
```

Converts `n` from radians to degrees and returns the result.

## exp

```lua
function math.exp(n: number): number
```

Returns the base-e exponent of `n`, that is `e^n`.

## floor

```lua
function math.floor(n: number): number
```

Rounds `n` downwards to previous integer boundary.

## fmod

```lua
function math.fmod(x: number, y: number): number
```

Returns the remainder of `x` modulo `y`, rounded towards zero. Returns NaN if `y` is zero.

## frexp

```lua
function math.frexp(n: number): (number, number)
```

Splits the number into a significand (a number in `[-1, +1]` range) and binary exponent such that `n = s * 2^e`, and returns `s, e`.

## ldexp

```lua
function math.ldexp(s: number, e: number): number
```

Given the significand and a binary exponent, returns a number `s * 2^e`.

## lerp

```lua
function math.lerp(a: number, b: number, t: number): number
```

Linearly interpolated between number value `a` and `b` using factor `t`, generally returning the result of `a + (b - a) * t`. When `t` is exactly `1`, the value of `b` will be returned instead to ensure that when `t` is on the interval `[0, 1]`, the result of `lerp` will be on the interval `[a, b]`.

## map

```lua
math.map(x: number, inmin: number, inmax: number, outmin: number, outmax: number): number
```

Returns a value that represents `x` mapped linearly from the input range (`inmin` to `inmax`) to the output range (`outmin` to `outmax`).

## log10

```lua
function math.log10(n: number): number
```

Returns base-10 logarithm of the input number. Returns NaN if the input is negative, and negative infinity if the input is 0. Equivalent to `math.log(n, 10)`.

## log

```lua
function math.log(n: number, base: number?): number
```

Returns logarithm of the input number in the specified base; base defaults to `e`. Returns NaN if the input is negative, and negative infinity if the input is 0.

## max

```lua
function math.max(list: ...number): number
```

Returns the maximum number of the input arguments. The function requires at least one input and will error if zero parameters are passed. If one of the inputs is a NaN, the result may or may not be a NaN.

## min

```lua
function math.min(list: ...number): number
```

Returns the minimum number of the input arguments. The function requires at least one input and will error if zero parameters are passed. If one of the inputs is a NaN, the result may or may not be a NaN.

## modf

```lua
function math.modf(n: number): (number, number)
```

Returns the integer and fractional part of the input number. Both the integer and fractional part have the same sign as the input number, e.g. `math.modf(-1.5)` returns `-1, -0.5`.

## pow

```lua
function math.pow(x: number, y: number): number
```

Returns `x` raised to the power of `y`.

## rad

```lua
function math.rad(n: number): number
```

Converts `n` from degrees to radians and returns the result.

## random

```lua
function math.random(): number
function math.random(n: number): number
function math.random(min: number, max: number): number
```

Returns a random number using the global random number generator. A zero-argument version returns a number in `[0, 1]` range. A one-argument version returns a number in `[1, n]` range. A two-argument version returns a number in `[min, max]` range. The input arguments are truncated to integers, so `math.random(1.5)` always returns 1.

## randomseed

```lua
function math.randomseed(seed: number)
```

Reseeds the global random number generator; subsequent calls to `math.random` will generate a deterministic sequence of numbers that only depends on `seed`.

## sinh

```lua
function math.sinh(n: number): number
```

Returns a hyperbolic sine of `n`.

## sin

```lua
function math.sin(n: number): number
```

Returns the sine of `n`, which is an angle in radians. Returns a value in `[0, 1]` range.

## sqrt

```lua
function math.sqrt(n: number): number
```

Returns the square root of `n`. Returns NaN if the input is negative.

## tanh

```lua
function math.tanh(n: number): number
```

Returns the hyperbolic tangent of `n`.

## tan

```lua
function math.tan(n: number): number
```

Returns the tangent of `n`, which is an angle in radians.

## noise

```lua
function math.noise(x: number, y: number?, z: number?): number
```

Returns 3D Perlin noise value for the point `(x, y, z)` (`y` and `z` default to zero if absent). Returns a value in `[-1, 1]` range.

## clamp

```lua
function math.clamp(n: number, min: number, max: number): number
```

Returns `n` if the number is in `[min, max]` range; otherwise, returns `min` when `n < min`, and `max` otherwise. If `n` is NaN, may or may not return NaN. The function errors if `min > max`.

## sign

```lua
function math.sign(n: number): number
```

Returns `-1` if `n` is negative, `1` if `n` is positive, and `0` if `n` is zero or NaN.

## round

```lua
function math.round(n: number): number
```

Rounds `n` to the nearest integer boundary. If `n` is exactly halfway between two integers, rounds `n` away from 0.
