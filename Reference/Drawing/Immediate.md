# Immediate

## Overview

Traditional drawing uses **retained mode**—objects persist until removed. **DrawingImmediate** is **immediate mode**; objects exist only during `RunService.Render` calls.

## Examples

```luau
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

```luau
function DrawingImmediate.Line(a: Vector2, b: Vector2, color: Color3, opacity: number, segments: number, thickness: number): ()
```

| Name      | Type    | Description    |
| --------- | ------- | -------------- |
| a         | Vector2 | Start position |
| b         | Vector2 | End position   |
| color     | Color3  | Line color     |
| opacity   | number  | Opacity (0-1)  |
| segments  | number  | Line segments  |
| thickness | number  | Line thickness |

***

### Circle

```luau
function DrawingImmediate.Circle(position: Vector2, radius: number, color: Color3, opacity: number, thickness: number): ()
```

| Name      | Type    | Description       |
| --------- | ------- | ----------------- |
| position  | Vector2 | Center position   |
| radius    | number  | Circle radius     |
| color     | Color3  | Outline color     |
| opacity   | number  | Opacity (0-1)     |
| thickness | number  | Outline thickness |

***

### FilledCircle

```luau
function DrawingImmediate.FilledCircle(position: Vector2, radius: number, color: Color3, opacity: number): ()
```

| Name     | Type    | Description     |
| -------- | ------- | --------------- |
| position | Vector2 | Center position |
| radius   | number  | Circle radius   |
| color    | Color3  | Fill color      |
| opacity  | number  | Opacity (0-1)   |

***

### Triangle

```luau
function DrawingImmediate.Triangle(a: Vector2, b: Vector2, c: Vector2, color: Color3, opacity: number, thickness: number): ()
```

| Name      | Type    | Description       |
| --------- | ------- | ----------------- |
| a         | Vector2 | Vertex A          |
| b         | Vector2 | Vertex B          |
| c         | Vector2 | Vertex C          |
| color     | Color3  | Outline color     |
| opacity   | number  | Opacity (0-1)     |
| thickness | number  | Outline thickness |

***

### FilledTriangle

```luau
function DrawingImmediate.FilledTriangle(a: Vector2, b: Vector2, c: Vector2, color: Color3, opacity: number): ()
```

| Name    | Type    | Description   |
| ------- | ------- | ------------- |
| a       | Vector2 | Vertex A      |
| b       | Vector2 | Vertex B      |
| c       | Vector2 | Vertex C      |
| color   | Color3  | Fill color    |
| opacity | number  | Opacity (0-1) |

***

### Rectangle

```luau
function DrawingImmediate.Rectangle(position: Vector2, size: Vector2, color: Color3, opacity: number, thickness: number): ()
```

| Name      | Type    | Description       |
| --------- | ------- | ----------------- |
| position  | Vector2 | Top-left position |
| size      | Vector2 | Width/height      |
| color     | Color3  | Outline color     |
| opacity   | number  | Opacity (0-1)     |
| thickness | number  | Outline thickness |

***

### FilledRectangle

```luau
function DrawingImmediate.FilledRectangle(position: Vector2, size: Vector2, color: Color3, opacity: number): ()
```

| Name     | Type    | Description       |
| -------- | ------- | ----------------- |
| position | Vector2 | Top-left position |
| size     | Vector2 | Width/height      |
| color    | Color3  | Fill color        |
| opacity  | number  | Opacity (0-1)     |

***

### Quad

```luau
function DrawingImmediate.Quad(a: Vector2, b: Vector2, c: Vector2, d: Vector2, color: Color3, opacity: number, thickness: number): ()
```

| Name      | Type    | Description       |
| --------- | ------- | ----------------- |
| a         | Vector2 | Vertex A          |
| b         | Vector2 | Vertex B          |
| c         | Vector2 | Vertex C          |
| d         | Vector2 | Vertex D          |
| color     | Color3  | Outline color     |
| opacity   | number  | Opacity (0-1)     |
| thickness | number  | Outline thickness |

***

### FilledQuad

```luau
function DrawingImmediate.FilledQuad(a: Vector2, b: Vector2, c: Vector2, d: Vector2, color: Color3, opacity: number): ()
```

| Name    | Type    | Description   |
| ------- | ------- | ------------- |
| a       | Vector2 | Vertex A      |
| b       | Vector2 | Vertex B      |
| c       | Vector2 | Vertex C      |
| d       | Vector2 | Vertex D      |
| color   | Color3  | Fill color    |
| opacity | number  | Opacity (0-1) |

***

### Polyline

```luau
function DrawingImmediate.Polyline(points: { Vector2 }, color: Color3, opacity: number, thickness: number): ()
```

| Name      | Type       | Description     |
| --------- | ---------- | --------------- |
| points    | { Vector2} | Array of points |
| color     | Color3     | Line color      |
| opacity   | number     | Opacity (0-1)   |
| thickness | number     | Line thickness  |

***

### Text

```luau
function DrawingImmediate.Text(position: Vector2, size: number, color: Color3, opacity: number, text: string, center: boolean, font: string?): ()
```

| Name     | Type    | Description          |
| -------- | ------- | -------------------- |
| position | Vector2 | Text position        |
| size     | number  | Text size            |
| color    | Color3  | Text color           |
| opacity  | number  | Opacity (0-1)        |
| text     | string  | Text content         |
| center   | boolean | Center align         |
| font     | string? | Font name (optional) |

***

### OutlinedText

```luau
function DrawingImmediate.OutlinedText(position: Vector2, size: number, color: Color3, opacity: number, text: string, center: boolean, font: string?): ()
```

| Name     | Type    | Description          |
| -------- | ------- | -------------------- |
| position | Vector2 | Text position        |
| size     | number  | Text size            |
| color    | Color3  | Text color           |
| opacity  | number  | Opacity (0-1)        |
| text     | string  | Text content         |
| center   | boolean | Center align         |
| font     | string? | Font name (optional) |

***

### Image

```luau
function DrawingImmediate.Image(source: string, position: Vector2, size: Vector2, color: Color3, opacity: number, is_gif: boolean, rounding: number): ()
```

| Name     | Type    | Description      |
| -------- | ------- | ---------------- |
| source   | string  | Image URL/source |
| position | Vector2 | Image position   |
| size     | Vector2 | Image size       |
| color    | Color3  | Tint color       |
| opacity  | number  | Opacity (0-1)    |
| is\_gif  | boolean | GIF animation    |
| rounding | number  | Corner rounding  |

***

### GetTextBounds

```luau
function DrawingImmediate.GetTextBounds(font: string, size: number, text: string): Vector2
```

| Name | Type   | Description  |
| ---- | ------ | ------------ |
| font | string | Font name    |
| size | number | Text size    |
| text | string | Text content |

<table data-header-hidden data-full-width="false"><thead><tr><th valign="middle">Type</th></tr></thead><tbody><tr><td valign="middle"><pre class="language-luau"><code class="lang-luau">Vector2
</code></pre></td></tr></tbody></table>

Calculates text boundaries. Returns `(width, height)`.
