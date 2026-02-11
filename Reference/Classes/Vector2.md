# Vector2

A 2D vector with X and Y components.

## Constructors

### Vector2.new

#### Definition

```luau
function Vector2.new(x: number, y: number): Vector2
function Vector2.new(): Vector2
```

#### Parameters

| Name | Type   | Description                 |
| ---- | ------ | --------------------------- |
| x    | number | The X component             |
| y    | number | The Y component             |

#### Returns

| Type    |
| ------- |
| Vector2 |

#### Description

Creates a new Vector2. If no parameters are provided, creates a zero vector (0, 0).

#### Code Samples

```luau
-- Create a vector
local vec = Vector2.new(100, 200)

-- Zero vector
local zero = Vector2.new()
print(zero) -- Vector2(0, 0)

-- Unit vectors
local right = Vector2.new(1, 0)
local up = Vector2.new(0, 1)
```

***

## Properties

### X

```luau
Vector2.X: number
```

The X component of the vector.

***

### Y

```luau
Vector2.Y: number
```

The Y component of the vector.

***

### Magnitude

```luau
Vector2.Magnitude: number
```

The length of the vector.

***

### Unit

```luau
Vector2.Unit: Vector2
```

A normalized version of the vector (length of 1).

***

## Methods

### Dot

#### Definition

```luau
function Vector2:Dot(other: Vector2): number
```

#### Parameters

| Name  | Type    | Description              |
| ----- | ------- | ------------------------ |
| other | Vector2 | The other vector         |

#### Returns

| Type   |
| ------ |
| number |

#### Description

Returns the dot product of this vector and another vector.

***

### Cross

#### Definition

```luau
function Vector2:Cross(other: Vector2): number
```

#### Parameters

| Name  | Type    | Description              |
| ----- | ------- | ------------------------ |
| other | Vector2 | The other vector         |

#### Returns

| Type   |
| ------ |
| number |

#### Description

Returns the 2D cross product (scalar) of this vector and another vector.

***

### Lerp

#### Definition

```luau
function Vector2:Lerp(goal: Vector2, alpha: number): Vector2
```

#### Parameters

| Name  | Type    | Description                              |
| ----- | ------- | ---------------------------------------- |
| goal  | Vector2 | The target vector to interpolate towards |
| alpha | number  | The interpolation factor (0 to 1)        |

#### Returns

| Type    |
| ------- |
| Vector2 |

#### Description

Returns a Vector2 interpolated between this vector and the goal vector by the alpha amount.

***

## Metatables

### __add

Adds two vectors.

```luau
local v1 = Vector2.new(10, 20)
local v2 = Vector2.new(5, 15)
local result = v1 + v2 -- Vector2(15, 35)
```

***

### __sub

Subtracts one vector from another.

```luau
local v1 = Vector2.new(10, 20)
local v2 = Vector2.new(5, 15)
local result = v1 - v2 -- Vector2(5, 5)
```

***

### __mul

Multiplies a vector by a scalar or another vector.

```luau
local vec = Vector2.new(10, 20)
local scaled = vec * 2 -- Vector2(20, 40)

-- Component-wise multiplication
local v1 = Vector2.new(2, 3)
local v2 = Vector2.new(4, 5)
local result = v1 * v2 -- Vector2(8, 15)
```

***

### __div

Divides a vector by a scalar or another vector.

```luau
local vec = Vector2.new(100, 200)
local scaled = vec / 2 -- Vector2(50, 100)

-- Component-wise division
local v1 = Vector2.new(100, 200)
local v2 = Vector2.new(10, 20)
local result = v1 / v2 -- Vector2(10, 10)
```

***

### __unm

Negates a vector.

```luau
local vec = Vector2.new(10, 20)
local negated = -vec -- Vector2(-10, -20)
```

***

### __eq

Compares two vectors for equality.

```luau
local v1 = Vector2.new(10, 20)
local v2 = Vector2.new(10, 20)
local v3 = Vector2.new(5, 15)

print(v1 == v2) -- true
print(v1 == v3) -- false
```

***

### __tostring

Returns a string representation of the vector.

```luau
local vec = Vector2.new(100, 200)
print(vec) -- "Vector2(100, 200)"
```

***

## Constants

### Vector2.zero

```luau
Vector2.zero: Vector2
```

A Vector2 with all components set to 0 (0, 0).

***

### Vector2.one

```luau
Vector2.one: Vector2
```

A Vector2 with all components set to 1 (1, 1).

***

### Vector2.xAxis

```luau
Vector2.xAxis: Vector2
```

A unit vector along the X-axis (1, 0).

***

### Vector2.yAxis

```luau
Vector2.yAxis: Vector2
```

A unit vector along the Y-axis (0, 1).
