# Definition
```luau
local Text = Text.new() -- Or, Drawing.new("Text")
```
# Properties

## Visible
```luau
Text.Visible: boolean
```

---
## Color
```luau
Text.Color: Color3
```

---
## ZIndex
```luau
Text.ZIndex: number
```
Range `[-2147483647, 2147483647]`.

---
## Opacity
```luau
Text.Opacity: number
```

---
## Text
```luau
Text.Text: string
```

---

## Size
```luau
Text.Size: number
```

---
## Center
```luau
Text.Center: boolean
```

---
## Outline
```luau
Text.Outline: boolean
```

---
## OutlineColor
```luau
Text.OutlineColor: Vector3
```

---
## Position
```luau
Text.Position: Vector2
```

---
## TextBounds
```luau
Text.TextBounds: Vector2
```

---
## Font
```luau
Text.Font: number
```
Range `[0, 31]`.

---
# Methods

## Remove
```luau
Text:Remove(): ()
```
Permanently removes the drawing object.
