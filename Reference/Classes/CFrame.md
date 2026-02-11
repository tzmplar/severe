# CFrame

A coordinate frame representing position and rotation in 3D space.

## Constructors

### CFrame.new

#### Definition

```luau
function CFrame.new(): CFrame
function CFrame.new(x: number, y: number, z: number): CFrame
function CFrame.new(position: Vector3): CFrame
function CFrame.new(position: Vector3, lookAt: Vector3): CFrame
function CFrame.new(x: number, y: number, z: number, qx: number, qy: number, qz: number, qw: number): CFrame
function CFrame.new(x: number, y: number, z: number, R00: number, R01: number, R02: number, R10: number, R11: number, R12: number, R20: number, R21: number, R22: number): CFrame
```

#### Description

Creates a new CFrame. Can be constructed in several ways:
- Empty constructor creates an identity CFrame at (0, 0, 0)
- Position-only creates a CFrame at the specified position with no rotation
- Position and lookAt creates a CFrame positioned at the first argument, looking at the second
- Position with quaternion values for rotation
- Position with full rotation matrix components

#### Code Samples

```luau
-- Identity CFrame
local cf1 = CFrame.new()

-- Position only
local cf2 = CFrame.new(10, 20, 30)

-- Position from Vector3
local cf3 = CFrame.new(Vector3.new(5, 10, 15))

-- Position looking at another position
local cf4 = CFrame.new(Vector3.new(0, 5, 0), Vector3.new(10, 5, 10))
```

***

### CFrame.fromEulerAnglesXYZ

#### Definition

```luau
function CFrame.fromEulerAnglesXYZ(rx: number, ry: number, rz: number): CFrame
function CFrame.fromEulerAnglesXYZ(rotation: Vector3): CFrame
```

#### Parameters

| Name     | Type    | Description                           |
| -------- | ------- | ------------------------------------- |
| rx       | number  | Rotation around X-axis in radians     |
| ry       | number  | Rotation around Y-axis in radians     |
| rz       | number  | Rotation around Z-axis in radians     |
| rotation | Vector3 | Vector containing rotation angles     |

#### Returns

| Type   |
| ------ |
| CFrame |

#### Description

Creates a rotated CFrame using Euler angles in X, Y, Z order (roll, pitch, yaw).

#### Code Samples

```luau
-- Rotate 90 degrees (π/2 radians) around Y-axis
local cf = CFrame.fromEulerAnglesXYZ(0, math.pi/2, 0)

-- Using Vector3
local rotation = Vector3.new(0, math.pi/2, 0)
local cf2 = CFrame.fromEulerAnglesXYZ(rotation)
```

***

### CFrame.fromEulerAnglesYXZ

#### Definition

```luau
function CFrame.fromEulerAnglesYXZ(rx: number, ry: number, rz: number): CFrame
function CFrame.fromEulerAnglesYXZ(rotation: Vector3): CFrame
```

#### Parameters

| Name     | Type    | Description                           |
| -------- | ------- | ------------------------------------- |
| rx       | number  | Rotation around X-axis in radians     |
| ry       | number  | Rotation around Y-axis in radians     |
| rz       | number  | Rotation around Z-axis in radians     |
| rotation | Vector3 | Vector containing rotation angles     |

#### Returns

| Type   |
| ------ |
| CFrame |

#### Description

Creates a rotated CFrame using Euler angles in Y, X, Z order.

***

### CFrame.fromOrientation

#### Definition

```luau
function CFrame.fromOrientation(rx: number, ry: number, rz: number): CFrame
```

#### Parameters

| Name | Type   | Description                       |
| ---- | ------ | --------------------------------- |
| rx   | number | Rotation around X-axis in radians |
| ry   | number | Rotation around Y-axis in radians |
| rz   | number | Rotation around Z-axis in radians |

#### Returns

| Type   |
| ------ |
| CFrame |

#### Description

Creates a rotated CFrame from orientation angles (equivalent to fromEulerAnglesYXZ).

***

### CFrame.fromAxisAngle

#### Definition

```luau
function CFrame.fromAxisAngle(axis: Vector3, rotation: number): CFrame
```

#### Parameters

| Name     | Type    | Description                        |
| -------- | ------- | ---------------------------------- |
| axis     | Vector3 | The axis of rotation (unit vector) |
| rotation | number  | The angle of rotation in radians   |

#### Returns

| Type   |
| ------ |
| CFrame |

#### Description

Creates a CFrame rotated around the specified axis by the given angle.

#### Code Samples

```luau
-- Rotate 45 degrees around the Y-axis
local axis = Vector3.new(0, 1, 0)
local cf = CFrame.fromAxisAngle(axis, math.pi/4)
```

***

### CFrame.fromMatrix

#### Definition

```luau
function CFrame.fromMatrix(position: Vector3, vX: Vector3, vY: Vector3, vZ: Vector3): CFrame
```

#### Parameters

| Name     | Type    | Description                          |
| -------- | ------- | ------------------------------------ |
| position | Vector3 | The position of the CFrame           |
| vX       | Vector3 | The right vector                     |
| vY       | Vector3 | The up vector                        |
| vZ       | Vector3 | The negative look vector             |

#### Returns

| Type   |
| ------ |
| CFrame |

#### Description

Creates a CFrame from a position and three directional vectors representing the rotation matrix.

***

### CFrame.lookAt

#### Definition

```luau
function CFrame.lookAt(from: Vector3, to: Vector3, up: Vector3?): CFrame
```

#### Parameters

| Name | Type     | Description                                     |
| ---- | -------- | ----------------------------------------------- |
| from | Vector3  | The position to look from                       |
| to   | Vector3  | The position to look at                         |
| up   | Vector3? | Optional up vector (defaults to world up)       |

#### Returns

| Type   |
| ------ |
| CFrame |

#### Description

Creates a CFrame positioned at 'from' and oriented to look at 'to'.

#### Code Samples

```luau
-- Create a CFrame looking from origin to a point
local cf = CFrame.lookAt(Vector3.new(0, 5, 0), Vector3.new(10, 5, 10))

-- With custom up vector
local cf2 = CFrame.lookAt(Vector3.new(0, 0, 0), Vector3.new(5, 5, 5), Vector3.new(0, 1, 0))
```

***

### CFrame.Angles

#### Definition

```luau
function CFrame.Angles(rx: number, ry: number, rz: number): CFrame
```

#### Parameters

| Name | Type   | Description                       |
| ---- | ------ | --------------------------------- |
| rx   | number | Rotation around X-axis in radians |
| ry   | number | Rotation around Y-axis in radians |
| rz   | number | Rotation around Z-axis in radians |

#### Returns

| Type   |
| ------ |
| CFrame |

#### Description

Creates a rotated CFrame from Euler angles (equivalent to fromOrientation).

***

## Methods

### Inverse

#### Definition

```luau
function CFrame:Inverse(): CFrame
```

#### Returns

| Type   |
| ------ |
| CFrame |

#### Description

Returns the inverse of this CFrame. When multiplied with the original, produces an identity CFrame.

#### Code Samples

```luau
local cf = CFrame.new(10, 20, 30)
local inverse = cf:Inverse()
local identity = cf * inverse -- Results in CFrame at origin
```

***

### Lerp

#### Definition

```luau
function CFrame:Lerp(goal: CFrame, alpha: number): CFrame
```

#### Parameters

| Name  | Type   | Description                              |
| ----- | ------ | ---------------------------------------- |
| goal  | CFrame | The target CFrame to interpolate towards |
| alpha | number | The interpolation factor (0 to 1)        |

#### Returns

| Type   |
| ------ |
| CFrame |

#### Description

Returns a CFrame interpolated between this CFrame and the goal CFrame by the alpha amount.

#### Code Samples

```luau
local start = CFrame.new(0, 0, 0)
local goal = CFrame.new(10, 10, 10)
local halfway = start:Lerp(goal, 0.5) -- CFrame at (5, 5, 5)
```

***

### ToWorldSpace

#### Definition

```luau
function CFrame:ToWorldSpace(cf: CFrame): CFrame
```

#### Parameters

| Name | Type   | Description                         |
| ---- | ------ | ----------------------------------- |
| cf   | CFrame | The CFrame in object space          |

#### Returns

| Type   |
| ------ |
| CFrame |

#### Description

Transforms a CFrame from object space to world space. Equivalent to `self * cf`.

***

### ToObjectSpace

#### Definition

```luau
function CFrame:ToObjectSpace(cf: CFrame): CFrame
```

#### Parameters

| Name | Type   | Description                    |
| ---- | ------ | ------------------------------ |
| cf   | CFrame | The CFrame in world space      |

#### Returns

| Type   |
| ------ |
| CFrame |

#### Description

Transforms a CFrame from world space to object space. Equivalent to `self:Inverse() * cf`.

***

### PointToWorldSpace

#### Definition

```luau
function CFrame:PointToWorldSpace(point: Vector3): Vector3
```

#### Parameters

| Name  | Type    | Description                  |
| ----- | ------- | ---------------------------- |
| point | Vector3 | The point in object space    |

#### Returns

| Type    |
| ------- |
| Vector3 |

#### Description

Transforms a point from object space to world space.

#### Code Samples

```luau
local cf = CFrame.new(10, 0, 0)
local localPoint = Vector3.new(5, 0, 0)
local worldPoint = cf:PointToWorldSpace(localPoint) -- Vector3(15, 0, 0)
```

***

### PointToObjectSpace

#### Definition

```luau
function CFrame:PointToObjectSpace(point: Vector3): Vector3
```

#### Parameters

| Name  | Type    | Description               |
| ----- | ------- | ------------------------- |
| point | Vector3 | The point in world space  |

#### Returns

| Type    |
| ------- |
| Vector3 |

#### Description

Transforms a point from world space to object space.

***

### VectorToWorldSpace

#### Definition

```luau
function CFrame:VectorToWorldSpace(vector: Vector3): Vector3
```

#### Parameters

| Name   | Type    | Description                   |
| ------ | ------- | ----------------------------- |
| vector | Vector3 | The vector in object space    |

#### Returns

| Type    |
| ------- |
| Vector3 |

#### Description

Transforms a vector from object space to world space (rotation only, no translation).

***

### VectorToObjectSpace

#### Definition

```luau
function CFrame:VectorToObjectSpace(vector: Vector3): Vector3
```

#### Parameters

| Name   | Type    | Description                |
| ------ | ------- | -------------------------- |
| vector | Vector3 | The vector in world space  |

#### Returns

| Type    |
| ------- |
| Vector3 |

#### Description

Transforms a vector from world space to object space (rotation only, no translation).

***

### GetComponents

#### Definition

```luau
function CFrame:GetComponents(): (number, number, number, number, number, number, number, number, number, number, number, number)
```

#### Returns

| Type                                                                                              |
| ------------------------------------------------------------------------------------------------- |
| (number, number, number, number, number, number, number, number, number, number, number, number) |

#### Description

Returns the 12 components of the CFrame: position (x, y, z) and rotation matrix (R00, R01, R02, R10, R11, R12, R20, R21, R22).

#### Code Samples

```luau
local cf = CFrame.new(10, 20, 30)
local x, y, z, R00, R01, R02, R10, R11, R12, R20, R21, R22 = cf:GetComponents()
print(x, y, z) -- 10, 20, 30
```

***

### ToOrientation

#### Definition

```luau
function CFrame:ToOrientation(): (number, number, number)
```

#### Returns

| Type                        |
| --------------------------- |
| (number, number, number)    |

#### Description

Returns the orientation of the CFrame as three Euler angles in radians (rx, ry, rz) in Y, X, Z order.

***

### ToEulerAnglesXYZ

#### Definition

```luau
function CFrame:ToEulerAnglesXYZ(): (number, number, number)
```

#### Returns

| Type                        |
| --------------------------- |
| (number, number, number)    |

#### Description

Returns the orientation of the CFrame as three Euler angles in radians (rx, ry, rz) in X, Y, Z order.

#### Code Samples

```luau
local cf = CFrame.Angles(0, math.pi/2, 0)
local rx, ry, rz = cf:ToEulerAnglesXYZ()
print(rx, ry, rz)
```

***

### ToEulerAnglesYXZ

#### Definition

```luau
function CFrame:ToEulerAnglesYXZ(): (number, number, number)
```

#### Returns

| Type                        |
| --------------------------- |
| (number, number, number)    |

#### Description

Returns the orientation of the CFrame as three Euler angles in radians (rx, ry, rz) in Y, X, Z order.

***

### ToAxisAngle

#### Definition

```luau
function CFrame:ToAxisAngle(): (Vector3, number)
```

#### Returns

| Type               |
| ------------------ |
| (Vector3, number)  |

#### Description

Returns the axis-angle representation of the CFrame's rotation as a unit vector and rotation angle in radians.

#### Code Samples

```luau
local cf = CFrame.fromAxisAngle(Vector3.new(0, 1, 0), math.pi/4)
local axis, angle = cf:ToAxisAngle()
print(axis, angle)
```

***

## Metatables

### __index

Allows property access on CFrame values.

```luau
local cf = CFrame.new(10, 20, 30)
local pos = cf.Position -- Vector3(10, 20, 30)
local rightVector = cf.RightVector
local upVector = cf.UpVector
local lookVector = cf.LookVector
```

***

### __mul

Multiplies two CFrames or transforms a Vector3.

```luau
-- CFrame multiplication
local cf1 = CFrame.new(10, 0, 0)
local cf2 = CFrame.new(5, 0, 0)
local result = cf1 * cf2 -- CFrame at (15, 0, 0)

-- Transform a Vector3
local cf = CFrame.new(10, 20, 30)
local point = Vector3.new(1, 1, 1)
local transformed = cf * point
```

***

### __add

Translates a CFrame by a Vector3.

```luau
local cf = CFrame.new(10, 20, 30)
local offset = Vector3.new(5, 5, 5)
local result = cf + offset -- CFrame at (15, 25, 35)
```

***

### __sub

Translates a CFrame by the negative of a Vector3.

```luau
local cf = CFrame.new(10, 20, 30)
local offset = Vector3.new(5, 5, 5)
local result = cf - offset -- CFrame at (5, 15, 25)
```

***

### __tostring

Returns a string representation of the CFrame.

```luau
local cf = CFrame.new(10, 20, 30)
print(cf) -- "CFrame(10, 20, 30, 1, 0, 0, 0, 1, 0, 0, 0, 1)"
```

***

## Properties

### Position

```luau
CFrame.Position: Vector3
```

The position component of the CFrame.

***

### RightVector

```luau
CFrame.RightVector: Vector3
```

The right direction vector of the CFrame (X-axis).

***

### UpVector

```luau
CFrame.UpVector: Vector3
```

The up direction vector of the CFrame (Y-axis).

***

### LookVector

```luau
CFrame.LookVector: Vector3
```

The look direction vector of the CFrame (negative Z-axis).

***

### X

```luau
CFrame.X: number
```

The X position component.

***

### Y

```luau
CFrame.Y: number
```

The Y position component.

***

### Z

```luau
CFrame.Z: number
```

The Z position component.
