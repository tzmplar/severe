# Definition
```luau
local Polyline = Polyline.new() -- Or, Drawing.new("Polyline")
```
# Properties

## Visible
```luau
Polyline.Visible: boolean
```

---

## Color
```luau
Polyline.Color: Color3
```

---

## ZIndex
```luau
Polyline.ZIndex: number
```
Range `[-2147483647, 2147483647]`.

---

## Opacity
```luau
Polyline.Opacity: number
```

---

## Points
```luau
Polyline.Points: { Vector2 }
```
An array of Vector2 points that make up the polyline.

---

## Thickness
```luau
Polyline.Thickness: number
```

---

## Filled
```luau
Polyline.Filled: boolean
```

---

# Methods

## Remove
```luau
Polyline:Remove(): ()
```
Permanently removes the drawing object.
