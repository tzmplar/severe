# Color3

A data type representing a color with red, green, and blue components.

## Constructors

### Color3.new

### Definition

```luau
function Color3.new(r: number, g: number, b: number): Color3
```

### Parameters

| Name | Type   | Description                      |
| ---- | ------ | -------------------------------- |
| r    | number | Red component (0 to 1)           |
| g    | number | Green component (0 to 1)         |
| b    | number | Blue component (0 to 1)          |

### Returns

| Type   |
| ------ |
| Color3 |

### Description

Creates a new Color3 from RGB values in the range 0 to 1.

### Code Samples

```luau
-- Pure red
local red = Color3.new(1, 0, 0)

-- Pure green
local green = Color3.new(0, 1, 0)

-- Pure blue
local blue = Color3.new(0, 0, 1)

-- White
local white = Color3.new(1, 1, 1)

-- Gray (50%)
local gray = Color3.new(0.5, 0.5, 0.5)
```

***

### Color3.fromRGB

### Definition

```luau
function Color3.fromRGB(r: number, g: number, b: number): Color3
```

### Parameters

| Name | Type   | Description                      |
| ---- | ------ | -------------------------------- |
| r    | number | Red component (0 to 255)         |
| g    | number | Green component (0 to 255)       |
| b    | number | Blue component (0 to 255)        |

### Returns

| Type   |
| ------ |
| Color3 |

### Description

Creates a new Color3 from RGB values in the range 0 to 255.

### Code Samples

```luau
-- Pure red
local red = Color3.fromRGB(255, 0, 0)

-- Orange
local orange = Color3.fromRGB(255, 165, 0)

-- Sky blue
local skyBlue = Color3.fromRGB(135, 206, 235)
```

***

### Color3.fromHSV

### Definition

```luau
function Color3.fromHSV(h: number, s: number, v: number): Color3
```

### Parameters

| Name | Type   | Description                           |
| ---- | ------ | ------------------------------------- |
| h    | number | Hue component (0 to 1)                |
| s    | number | Saturation component (0 to 1)         |
| v    | number | Value/brightness component (0 to 1)   |

### Returns

| Type   |
| ------ |
| Color3 |

### Description

Creates a new Color3 from HSV (Hue, Saturation, Value) color space values.

### Code Samples

```luau
-- Pure red (hue = 0)
local red = Color3.fromHSV(0, 1, 1)

-- Pure green (hue = 1/3)
local green = Color3.fromHSV(1/3, 1, 1)

-- Pure blue (hue = 2/3)
local blue = Color3.fromHSV(2/3, 1, 1)

-- Desaturated red (pink)
local pink = Color3.fromHSV(0, 0.5, 1)
```

***

### Color3.fromHex

### Definition

```luau
function Color3.fromHex(hex: string): Color3
```

### Parameters

| Name | Type   | Description                                    |
| ---- | ------ | ---------------------------------------------- |
| hex  | string | Hexadecimal color string (e.g., "#FF5733")     |

### Returns

| Type   |
| ------ |
| Color3 |

### Description

Creates a new Color3 from a hexadecimal color string. The string can optionally start with "#".

### Code Samples

```luau
-- With hash
local orange = Color3.fromHex("#FF5733")

-- Without hash
local blue = Color3.fromHex("0000FF")

-- Cyan
local cyan = Color3.fromHex("#00FFFF")
```

***

## Methods

### ToHSV

### Definition

```luau
function Color3:ToHSV(): (number, number, number)
```

### Returns

| Type                        |
| --------------------------- |
| (number, number, number)    |

### Description

Converts the Color3 to HSV (Hue, Saturation, Value) format and returns the three components.

### Code Samples

```luau
local color = Color3.fromRGB(255, 128, 0)
local h, s, v = color:ToHSV()
print(h, s, v)
```

***

### Lerp

### Definition

```luau
function Color3:Lerp(goal: Color3, alpha: number): Color3
```

### Parameters

| Name  | Type   | Description                              |
| ----- | ------ | ---------------------------------------- |
| goal  | Color3 | The target color to interpolate towards  |
| alpha | number | The interpolation factor (0 to 1)        |

### Returns

| Type   |
| ------ |
| Color3 |

### Description

Returns a Color3 interpolated between this color and the goal color by the alpha amount.

### Code Samples

```luau
local red = Color3.fromRGB(255, 0, 0)
local blue = Color3.fromRGB(0, 0, 255)
local purple = red:Lerp(blue, 0.5)
```

***

## Metatables

### __index

Allows property access on Color3 values.

```luau
local color = Color3.fromRGB(255, 128, 64)
local r = color.R -- 1
local g = color.G -- 0.502
local b = color.B -- 0.251
```

***

### __tostring

Returns a string representation of the Color3.

```luau
local color = Color3.fromRGB(255, 128, 0)
print(color) -- "Color3(1, 0.502, 0)"
```

***

### __eq

Compares two Color3 values for equality.

```luau
local color1 = Color3.fromRGB(255, 0, 0)
local color2 = Color3.fromRGB(255, 0, 0)
local color3 = Color3.fromRGB(0, 255, 0)

print(color1 == color2) -- true
print(color1 == color3) -- false
```

***

### __type

Returns the type name "Color3".

```luau
local color = Color3.new(1, 0, 0)
print(typeof(color)) -- "Color3"
```

***

## Properties

### R

```luau
Color3.R: number
```

The red component of the color (0 to 1).

***

### G

```luau
Color3.G: number
```

The green component of the color (0 to 1).

***

### B

```luau
Color3.B: number
```

The blue component of the color (0 to 1).
