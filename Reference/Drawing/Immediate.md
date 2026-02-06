# DrawingImmediate

## Overview

Traditional drawing uses **retained mode**—objects persist until removed. **DrawingImmediate** is **immediate mode**; objects exist only during `RunService.Render` calls.
## Examples
```lua
local Players = game:GetService("Players")
local CurrentCamera = workspace.CurrentCamera
local RunService = game:GetService("RunService")

RunService.Render:Connect(function()
    for Index, Player in Players:GetChildren() do
        local Character = Player.Character
        if not Character then continue end
        
        local Head = Character:FindFirstChild("Head")
        if not Head then continue end
        
        local Screen, Visible = CurrentCamera:WorldToScreenPoint(Head.Position)
        
        if Visible then
            DrawingImmediate.OutlinedText(Screen, 14, Color3.fromRGB(125, 165, 255), 1, Player.Name, true, "Tamzen")
        end
    end
end)
```

## Functions

Call inside `RunService.Render` to avoid flickering. No return values.
### Line
### Definition
```lua
function DrawingImmediate.Line(a: Vector2, b: Vector2, color: Color3, opacity: number, segments: number, thickness: number): ()
```
### Parameters

| Name     | Type    | Description          |
|----------|---------|----------------------|
| a        | Vector2 | Start position       |
| b        | Vector2 | End position         |
| color    | Color3  | Line color           |
| opacity  | number  | Opacity (0-1)        |
| segments | number  | Line segments        |
| thickness| number  | Line thickness       |

---

### Circle
### Definition
```lua
function DrawingImmediate.Circle(position: Vector2, radius: number, color: Color3, opacity: number, thickness: number): ()
```
### Parameters

| Name     | Type    | Description          |
|----------|---------|----------------------|
| position | Vector2 | Center position      |
| radius   | number  | Circle radius        |
| color    | Color3  | Outline color        |
| opacity  | number  | Opacity (0-1)        |
| thickness| number  | Outline thickness    |

---

### FilledCircle
### Definition
```lua
function DrawingImmediate.FilledCircle(position: Vector2, radius: number, color: Color3, opacity: number): ()
```
### Parameters

| Name     | Type    | Description          |
|----------|---------|----------------------|
| position | Vector2 | Center position      |
| radius   | number  | Circle radius        |
| color    | Color3  | Fill color           |
| opacity  | number  | Opacity (0-1)        |

---

### Triangle
### Definition
```lua
function DrawingImmediate.Triangle(a: Vector2, b: Vector2, c: Vector2, color: Color3, opacity: number, thickness: number): ()
```
### Parameters

| Name     | Type    | Description          |
|----------|---------|----------------------|
| a        | Vector2 | Vertex A             |
| b        | Vector2 | Vertex B             |
| c        | Vector2 | Vertex C             |
| color    | Color3  | Outline color        |
| opacity  | number  | Opacity (0-1)        |
| thickness| number  | Outline thickness    |

---

### FilledTriangle
### Definition
```lua
function DrawingImmediate.FilledTriangle(a: Vector2, b: Vector2, c: Vector2, color: Color3, opacity: number): ()
```
### Parameters

| Name     | Type    | Description          |
|----------|---------|----------------------|
| a        | Vector2 | Vertex A             |
| b        | Vector2 | Vertex B             |
| c        | Vector2 | Vertex C             |
| color    | Color3  | Fill color           |
| opacity  | number  | Opacity (0-1)        |

---

### Rectangle
### Definition
```lua
function DrawingImmediate.Rectangle(position: Vector2, size: Vector2, color: Color3, opacity: number, thickness: number): ()
```
### Parameters

| Name     | Type    | Description          |
|----------|---------|----------------------|
| position | Vector2 | Top-left position    |
| size     | Vector2 | Width/height         |
| color    | Color3  | Outline color        |
| opacity  | number  | Opacity (0-1)        |
| thickness| number  | Outline thickness    |

---

### FilledRectangle
### Definition
```lua
function DrawingImmediate.FilledRectangle(position: Vector2, size: Vector2, color: Color3, opacity: number): ()
```
### Parameters

| Name     | Type    | Description          |
|----------|---------|----------------------|
| position | Vector2 | Top-left position    |
| size     | Vector2 | Width/height         |
| color    | Color3  | Fill color           |
| opacity  | number  | Opacity (0-1)        |

---

### Quad
### Definition
```lua
function DrawingImmediate.Quad(a: Vector2, b: Vector2, c: Vector2, d: Vector2, color: Color3, opacity: number, thickness: number): ()
```
### Parameters

| Name     | Type    | Description          |
|----------|---------|----------------------|
| a        | Vector2 | Vertex A             |
| b        | Vector2 | Vertex B             |
| c        | Vector2 | Vertex C             |
| d        | Vector2 | Vertex D             |
| color    | Color3  | Outline color        |
| opacity  | number  | Opacity (0-1)        |
| thickness| number  | Outline thickness    |

---

### FilledQuad
### Definition
```lua
function DrawingImmediate.FilledQuad(a: Vector2, b: Vector2, c: Vector2, d: Vector2, color: Color3, opacity: number): ()
```
### Parameters

| Name     | Type    | Description          |
|----------|---------|----------------------|
| a        | Vector2 | Vertex A             |
| b        | Vector2 | Vertex B             |
| c        | Vector2 | Vertex C             |
| d        | Vector2 | Vertex D             |
| color    | Color3  | Fill color           |
| opacity  | number  | Opacity (0-1)        |

---

### Polyline
### Definition
```lua
function DrawingImmediate.Polyline(points: { Vector2 }, color: Color3, opacity: number, thickness: number): ()
```
### Parameters

| Name    | Type     | Description          |
|---------|----------|----------------------|
| points  | { Vector2} | Array of points    |
| color   | Color3   | Line color           |
| opacity | number   | Opacity (0-1)        |
| thickness| number | Line thickness     |

---

### Text
### Definition
```lua
function DrawingImmediate.Text(position: Vector2, size: number, color: Color3, opacity: number, text: string, center: boolean, font: string?): ()
```
### Parameters

| Name    | Type    | Description          |
|---------|---------|----------------------|
| position| Vector2 | Text position        |
| size    | number  | Text size            |
| color   | Color3  | Text color           |
| opacity | number  | Opacity (0-1)        |
| text    | string  | Text content         |
| center  | boolean | Center align         |
| font    | string? | Font name (optional) |

---

### OutlinedText
### Definition
```lua
function DrawingImmediate.OutlinedText(position: Vector2, size: number, color: Color3, opacity: number, text: string, center: boolean, font: string?): ()
```
### Parameters

| Name    | Type    | Description          |
|---------|---------|----------------------|
| position| Vector2 | Text position        |
| size    | number  | Text size            |
| color   | Color3  | Text color           |
| opacity | number  | Opacity (0-1)        |
| text    | string  | Text content         |
| center  | boolean | Center align         |
| font    | string? | Font name (optional) |

---

### Image
### Definition
```lua
function DrawingImmediate.Image(source: string, position: Vector2, size: Vector2, color: Color3, opacity: number, is_gif: boolean, rounding: number): ()
```
### Parameters

| Name    | Type    | Description          |
|---------|---------|----------------------|
| source  | string  | Image URL/source     |
| position| Vector2 | Image position       |
| size    | Vector2 | Image size           |
| color   | Color3  | Tint color           |
| opacity | number  | Opacity (0-1)        |
| is_gif  | boolean | GIF animation        |
| rounding| number  | Corner rounding      |

---

### GetTextBounds
### Definition
```lua
function DrawingImmediate.GetTextBounds(font: string, size: number, text: string): Vector2
```
### Parameters

| Name | Type   | Description          |
|------|--------|----------------------|
| font | string | Font name            |
| size | number | Text size            |
| text | string | Text content         |

### Returns
```horizontal
### Vector2
```
### Description
Calculates text boundaries. Returns `(width, height)`.