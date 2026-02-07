# Camera

The Camera object controls the player's view in the game.

## ViewportSize

### Definition

```luau
Camera.ViewportSize: Vector2
```

### Description

The size of the camera's viewport in pixels (read-only).

***

## FieldOfView

### Definition

```luau
Camera.FieldOfView: number
```

### Description

The field of view of the camera in degrees (read-only).

***

## Position

### Definition

```luau
Camera.Position: Vector3
```

### Description

The position of the camera in world space. Can be read and written.

***

## CFrame

### Definition

```luau
Camera.CFrame: CFrame
```

### Description

The position and orientation of the camera in world space. Can be read and written.

***

## Velocity

### Definition

```luau
Camera.Velocity: Vector3
```

### Description

The current velocity of the camera. Can be read and written.

***

## RightVector

### Definition

```luau
Camera.RightVector: Vector3
```

### Description

The right vector of the camera's orientation. Can be read and written.

***

## UpVector

### Definition

```luau
Camera.UpVector: Vector3
```

### Description

The up vector of the camera's orientation. Can be read and written.

***

## LookVector

### Definition

```luau
Camera.LookVector: Vector3
```

### Description

The forward/look vector of the camera's orientation. Can be read and written.

***

## CameraSubject

### Definition

```luau
Camera.CameraSubject: Instance?
```

### Description

The instance that the camera is focused on. Can be set to change the camera's subject.

***

## WorldToScreenPoint

### Definition

```luau
function Camera:WorldToScreenPoint(worldPosition: Vector3): (Vector3, boolean)
```

### Parameters

| Name          | Type    | Description                 |
| ------------- | ------- | --------------------------- |
| worldPosition | Vector3 | The position in world space |

### Returns

| Type               |
| ------------------ |
| (Vector3, boolean) |

### Description

Converts a world position to screen coordinates. Returns a Vector3 with X and Y as screen coordinates (Z is depth), and a boolean indicating if the point is visible on screen.
