# UserInputService

Service for handling user input such as mouse and keyboard.

## GetMouseLocation

### Definition

```luau
function UserInputService:GetMouseLocation(): Vector2
```

### Returns

| Type    |
| ------- |
| Vector2 |

### Description

Returns the current mouse position as a Vector2.

***

## SetMouseLocation

### Definition

```luau
function UserInputService:SetMouseLocation(x: number, y: number): ()
```

### Parameters

| Name | Type   | Description           |
| ---- | ------ | --------------------- |
| x    | number | The X coordinate      |
| y    | number | The Y coordinate      |

### Description

Sets the mouse position to the specified X and Y coordinates.

***

## MouseBehavior

### Type

```luau
Enum.MouseBehavior
```

### Description

Controls how the mouse behaves (e.g., locked, default). Can be read and written.

***

## MouseDeltaSensitivity

### Type

```luau
number
```

### Description

The sensitivity of mouse movement delta. Can be read and written.

***

## MouseIconEnabled

### Type

```luau
boolean
```

### Description

Determines whether the mouse icon is visible. Can be read and written.
