# Camera

Documentation for these functions and properties can be found [here](https://create.roblox.com/docs/reference/engine/classes/Camera).

## Properties

### ViewportSize

```lua
Camera.ViewportSize: vector
```

### FieldOfView

```lua
Camera.FieldOfView: number?
```

### CameraSubject

```lua
Camera.CameraSubject: Instance?
```

### Position

```lua
Camera.Position: vector
```

### UpVector

```lua
Camera.UpVector: vector
```

### LookVector

```lua
Camera.LookVector: vector
```

### RightVector

```lua
Camera.RightVector: vector
```

### CFrame

```lua
Camera.CFrame: {
    Position: vector,
    
    UpVector: vector,
    RightVector: vector,
    LookVector: vector
}
```

## Methods

### WorldToScreenPoint

```lua
function Camera:WorldToScreenPoint(world: vector): (vector, boolean)
```
