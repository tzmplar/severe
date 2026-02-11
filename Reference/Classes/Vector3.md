# Vector3

A 3D vector with X, Y, and Z components.

## Constructors

### Vector3.new

#### Definition

```luau
function Vector3.new(x: number, y: number, z: number): Vector3
function Vector3.new(): Vector3
```

#### Parameters

| Name | Type   | Description                 |
| ---- | ------ | --------------------------- |
| x    | number | The X component             |
| y    | number | The Y component             |
| z    | number | The Z component             |

#### Returns

| Type    |
| ------- |
| Vector3 |

#### Description

Creates a new Vector3. If no parameters are provided, creates a zero vector (0, 0, 0).

#### Code Samples

```luau
-- Create a vector
local vec = Vector3.new(10, 20, 30)

-- Zero vector
local zero = Vector3.new()
print(zero) -- Vector3(0, 0, 0)

-- Unit vectors
local right = Vector3.new(1, 0, 0)
local up = Vector3.new(0, 1, 0)
local forward = Vector3.new(0, 0, 1)
```

***

## Properties

### X

```luau
Vector3.X: number
```

The X component of the vector.

***

### Y

```luau
Vector3.Y: number
```

The Y component of the vector.

***

### Z

```luau
Vector3.Z: number
```

The Z component of the vector.

***

### Magnitude

```luau
Vector3.Magnitude: number
```

The length of the vector.

***

### Unit

```luau
Vector3.Unit: Vector3
```

A normalized version of the vector (length of 1).

***

## Methods

### Dot

#### Definition

```luau
function Vector3:Dot(other: Vector3): number
```

#### Parameters

| Name  | Type    | Description              |
| ----- | ------- | ------------------------ |
| other | Vector3 | The other vector         |

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
function Vector3:Cross(other: Vector3): Vector3
```

#### Parameters

| Name  | Type    | Description              |
| ----- | ------- | ------------------------ |
| other | Vector3 | The other vector         |

#### Returns

| Type    |
| ------- |
| Vector3 |

#### Description

Returns the cross product of this vector and another vector.

***

### Lerp

#### Definition

```luau
function Vector3:Lerp(goal: Vector3, alpha: number): Vector3
```

#### Parameters

| Name  | Type    | Description                              |
| ----- | ------- | ---------------------------------------- |
| goal  | Vector3 | The target vector to interpolate towards |
| alpha | number  | The interpolation factor (0 to 1)        |

#### Returns

| Type    |
| ------- |
| Vector3 |

#### Description

Returns a Vector3 interpolated between this vector and the goal vector by the alpha amount.

***

## Metatables

### __add

Adds two vectors.

```luau
local v1 = Vector3.new(1, 2, 3)
local v2 = Vector3.new(4, 5, 6)
local result = v1 + v2 -- Vector3(5, 7, 9)
```

***

### __sub

Subtracts one vector from another.

```luau
local v1 = Vector3.new(5, 7, 9)
local v2 = Vector3.new(1, 2, 3)
local result = v1 - v2 -- Vector3(4, 5, 6)
```

***

### __mul

Multiplies a vector by a scalar or another vector.

```luau
local vec = Vector3.new(1, 2, 3)
local scaled = vec * 2 -- Vector3(2, 4, 6)

-- Component-wise multiplication
local v1 = Vector3.new(2, 3, 4)
local v2 = Vector3.new(1, 2, 3)
local result = v1 * v2 -- Vector3(2, 6, 12)
```

***

### __div

Divides a vector by a scalar or another vector.

```luau
local vec = Vector3.new(10, 20, 30)
local scaled = vec / 2 -- Vector3(5, 10, 15)

-- Component-wise division
local v1 = Vector3.new(10, 20, 30)
local v2 = Vector3.new(2, 4, 5)
local result = v1 / v2 -- Vector3(5, 5, 6)
```

***

### __unm

Negates a vector.

```luau
local vec = Vector3.new(1, 2, 3)
local negated = -vec -- Vector3(-1, -2, -3)
```

***

### __eq

Compares two vectors for equality.

```luau
local v1 = Vector3.new(1, 2, 3)
local v2 = Vector3.new(1, 2, 3)
local v3 = Vector3.new(4, 5, 6)

print(v1 == v2) -- true
print(v1 == v3) -- false
```

***

### __tostring

Returns a string representation of the vector.

```luau
local vec = Vector3.new(10, 20, 30)
print(vec) -- "Vector3(10, 20, 30)"
```

***

## Constants

### Vector3.zero

```luau
Vector3.zero: Vector3
```

A Vector3 with all components set to 0 (0, 0, 0).

***

### Vector3.one

```luau
Vector3.one: Vector3
```

A Vector3 with all components set to 1 (1, 1, 1).

***

### Vector3.xAxis

```luau
Vector3.xAxis: Vector3
```

A unit vector along the X-axis (1, 0, 0).

***

### Vector3.yAxis

```luau
Vector3.yAxis: Vector3
```

A unit vector along the Y-axis (0, 1, 0).

***

### Vector3.zAxis

```luau
Vector3.zAxis: Vector3
```

A unit vector along the Z-axis (0, 0, 1).
