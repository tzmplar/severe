# Definition
```lua
local Polyline = Polyline.new() -- Or, Drawing.new("Polyline")
```
# Properties

## Visible
```lua
Polyline.Visible: boolean
```

---

## Color
```lua
Polyline.Color: Color3
```

---

## ZIndex
```lua
Polyline.ZIndex: number
```
Range `[-2147483647, 2147483647]`.

---

## Opacity
```lua
Polyline.Opacity: number
```

---

## Points
```lua
Polyline.Points: { Vector2 }
```
An array of Vector2 points that make up the polyline.

---

## Thickness
```lua
Polyline.Thickness: number
```

---

## Filled
```lua
Polyline.Filled: boolean
```

---

# Methods

## Remove
```lua
Polyline:Remove(): ()
```
Permanently removes the drawing object.