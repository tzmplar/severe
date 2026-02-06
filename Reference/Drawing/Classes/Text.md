# Definition
```lua
local Text = Text.new() -- Or, Drawing.new("Text")
```
# Properties

## Visible
```lua
Text.Visible: boolean
```

---
## Color
```lua
Text.Color: Color3
```

---
## ZIndex
```lua
Text.ZIndex: number
```
Range `[-2147483647, 2147483647]`.

---
## Opacity
```lua
Text.Opacity: number
```

---
## Text
```lua
Text.Text: string
```

---

## Size
```lua
Text.Size: number
```

---
## Center
```lua
Text.Center: boolean
```

---
## Outline
```lua
Text.Outline: boolean
```

---
## OutlineColor
```lua
Text.OutlineColor: Vector3
```

---
## Position
```lua
Text.Position: Vector2
```

---
## TextBounds
```lua
Text.TextBounds: Vector2
```

---
## Font
```lua
Text.Font: number
```
Range `[0, 31]`.

---
# Methods
#### Remove
```lua
Text:Remove(): ()
```
Permanently removes the drawing object.