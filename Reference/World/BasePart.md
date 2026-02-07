# BasePart

BasePart is the base class for all physical part objects in the game world.

## Applies To

- Part
- MeshPart
- UnionOperation
- SpawnLocation
- CornerWedgePart
- TrussPart
- WedgePart

## CanCollide

### Definition

```luau
BasePart.CanCollide: boolean
```

### Description

Determines whether the part can collide with other parts. Can be read and written.

***

## Transparency

### Definition

```luau
BasePart.Transparency: number
```

### Description

The transparency of the part, ranging from 0 (opaque) to 1 (fully transparent). Can be read and written.

***

## Size

### Definition

```luau
BasePart.Size: Vector3
```

### Description

The size of the part in studs. Can be read and written.

***

## Position

### Definition

```luau
BasePart.Position: Vector3
```

### Description

The position of the part in world space. Can be read and written.

***

## CFrame

### Definition

```luau
BasePart.CFrame: CFrame
```

### Description

The position and orientation of the part in world space. Can be read and written.

***

## Velocity

### Definition

```luau
BasePart.Velocity: Vector3
```

### Description

The current velocity of the part. Can be read and written.

***

## RightVector

### Definition

```luau
BasePart.RightVector: Vector3
```

### Description

The right vector of the part's orientation (read-only).

***

## UpVector

### Definition

```luau
BasePart.UpVector: Vector3
```

### Description

The up vector of the part's orientation (read-only).

***

## LookVector

### Definition

```luau
BasePart.LookVector: Vector3
```

### Description

The forward/look vector of the part's orientation (read-only).

***

## IsNetworkSleeping

### Definition

```luau
BasePart.IsNetworkSleeping: boolean
```

### Description

Indicates whether the part is currently network sleeping (read-only).

***

## Description

### Definition

```luau
BasePart.Description: string
```

### Description

A user-defined description for the part. Can be read and written.

***

## TextureId

**Applies to: MeshPart, SpecialMesh**

### Definition

```luau
MeshPart.TextureId: string
SpecialMesh.TextureId: string
```

### Description

The asset ID of the texture applied to the mesh. Can be read and written.

***

## MeshId

**Applies to: MeshPart, SpecialMesh**

### Definition

```luau
MeshPart.MeshId: string
SpecialMesh.MeshId: string
```

### Description

The asset ID of the mesh geometry. Can be read and written.
