# Definition
```lua
local Triangle = Triangle.new() -- Or, Drawing.new("Triangle")
```

# Properties

## Visible
```lua
Triangle.Visible: boolean
```

---

## Color
```lua
Triangle.Color: Color3
```

---

## ZIndex
```lua
Triangle.ZIndex: number
```
Range `[-2147483647, 2147483647]`.

---

## Opacity
```lua
Triangle.Opacity: number
```

---

## Transparency
```lua
Triangle.Transparency: number
```

---

## Thickness
```lua
Triangle.Thickness: number
```

---

## PointA
```lua
Triangle.PointA: Vector2
```

---

## PointB
```lua
Triangle.PointB: Vector2
```

---

## PointC
```lua
Triangle.PointC: Vector2
```

---

## Filled
```lua
Triangle.Filled: boolean
```

---

# Methods

## Remove
```lua
Triangle:Remove(): ()
```
Permanently removes the drawing object.