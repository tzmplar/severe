# DrawingImmediate

## Overview

The traditional way of [.](./ "mention") is [**retained mode**](https://en.wikipedia.org/wiki/Retained_mode), thus the objects that are made through it stay on the screen until removed. However, **DrawingImmediate** as the name implies, is [**immediate mode**](https://en.wikipedia.org/wiki/Immediate_mode_\(computer_graphics\)), where the lifecycle of the objects are directly influenced by [#render](../../engine/runservice.md#render "mention").\
\
This is similar to something, like **Serotonin/Melatonin** way of "painting" objects, with the exception that the API design is heavily inspired by **Synapse V3** and **Roblox**'s RunService.

## Examples

```lua
local Players = game:GetService("Players")
local CurrentCamera = workspace.CurrentCamera

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

These functions construct an object with the respective parameters, they don't return anything, and they should be called inside `RunService.OnRender`.

### Line

```lua
function DrawingImmediate.Line(a: vector, b: vector, color: Color3, opacity: number, segments: number, thickness: number): ()
```

### Circle

```lua
function DrawingImmediate.Circle(position: vector, radius: number, color: Color3, opacity: number, thickness: number): ()
```

### FilledCircle

```lua
function DrawingImmediate.FilledCircle(position: vector, radius: number, color: Color3, opacity: number): ()
```

### Triangle

```lua
function DrawingImmediate.Triangle(a: vector, b: vector, c: vector, color: Color3, opacity: number, thickness: number): ()
```

### FilledTriangle

```lua
function DrawingImmediate.FilledTriangle(a: vector, b: vector, c: vector, color: Color3, opacity: number): ()
```

### Rectangle

```lua
function DrawingImmediate.Rectangle(position: vector, size: vector, color: Color3, opacity: number, thickness: number): ()
```

### FilledRectangle

```lua
function DrawingImmediate.FilledRectangle(position: vector, size: vector, color: Color3, opacity: number): ()
```

### Quad

```lua
function DrawingImmediate.Quad(a: vector, b: vector, c: vector, d: vector, color: Color3, opacity: number, thickness: number): ()
```

### FilledQuad

```lua
function DrawingImmediate.FilledQuad(a: vector, b: vector, c: vector, d: vector, color: Color3, opacity: number): ()
```

### Polyline

```lua
function DrawingImmediate.Polyline(points: { vector }, color: Color3, opacity: number, thickness: number): ()
```

### Text

```lua
function DrawingImmediate.Text(position: vector, size: number, color: Color3, opacity: number, text: string, center: boolean, font: string?): ()
```

### OutlinedText

```lua
function DrawingImmediate.OutlinedText(position: vector, size: number, color: Color3, opacity: number, text: string, center: boolean, font: string?): ()
```

### Image

```lua
function DrawingImmediate.Image(source: string, position: vector, size: vector, color: Color3, opacity: number, is_gif: boolean, rounding: number): ()
```

### GetTextBounds

```lua
function DrawingImmediate.GetTextBounds(font: string, size: number, text: string): vector
```

Calculates the text boundaries based on the provided `font`, `size`, and `text`. Returns a 2-dimensional vector.
