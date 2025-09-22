# Drawing

The `Drawing` library provides functions to create and manage graphical drawing objects.

## Functions

### clear

```lua
function Drawing.clear(): ()
```

Removes all existing drawing objects.

### new

```lua
function Drawing.new(type: string): Object
```

Creates a new drawing object of the specified type and returns it. Valid types are: "Text", "Line", "Quad", "Triangle", "Circle", "Square", "Image", "Polyline".

## Methods

### Remove

```lua
function Object:Remove(): ()
```

Permanently removes the drawing object.

## Properties

### Base

#### Visible

```lua
Object.Visible: boolean
```

#### Color

```lua
Object.Color: Color3
```

#### ZIndex

```lua
Object.ZIndex: number
```

The sort-order of the object, the higher it is, the more priority the object holds, range \[-2147483647, 2147483647].

#### Opacity

```lua
Object.Opacity: number
```

### Text

#### Text

```lua
Object.Text: string
```

#### Size

```lua
Object.Size: number
```

#### Center

```lua
Object.Center: boolean
```

#### Outline

```lua
Object.Outline: boolean
```

#### OutlineColor

```lua
Object.OutlineColor: Vector3
```

#### Position

```lua
Object.Position: Vector2
```

#### TextBounds

```lua
Object.TextBounds: Vector2
```

#### Font

```lua
Object.Font: number
```

Range \[0, 31].

### Line

#### Thickness

```lua
Object.Thickness: number
```

#### From

```lua
Object.From: Vector2
```

#### To

```lua
Object.To: Vector2
```

### Circle

#### Thickness

```lua
Object.Thickness: number
```

#### NumSides

```lua
Object.NumSides: number
```

#### Radius

```lua
Object.Radius: number
```

#### Filled

```lua
Object.Filled: boolean
```

#### Position

```lua
Object.Position: Vector2
```

### Square

#### Thickness

```lua
Object.Thickness: number
```

#### Size

```lua
Object.Size: Vector2
```

#### Position

```lua
Object.Position: Vector2
```

#### Filled

```lua
Object.Filled: boolean
```

#### Rounding

```lua
Object.Rounding: number
```

### Triangle

#### Transparency

```lua
Object.Transparency: number
```

#### Thickness

```lua
Object.Thickness: number
```

#### PointA

```lua
Object.PointA: Vector2
```

#### PointB

```lua
Object.PointB: Vector2
```

#### PointC

```lua
Object.PointC: Vector2
```

#### Filled

```lua
Object.Filled: boolean
```

### Image

#### Url

```lua
Object.Url: string
```

#### Data

```lua
Object.Data: string
```

#### Gif

```lua
Object.Gif: boolean
```

#### Delay

```lua
Object.Delay: number
```

#### Position

```lua
Object.Position: Vector2
```

#### Size

```lua
Object.Size: Vector2
```

#### Rounding

```lua
Object.Rounding: number
```

#### ImageSize

```lua
Object.ImageSize: Vector2
```

### Quad

#### PointA

```lua
Object.PointA: Vector2
```

#### PointB

```lua
Object.PointB: Vector2
```

#### PointC

```lua
Object.PointC: Vector2
```

#### PointD

```lua
Object.PointD: Vector2
```

#### Thickness

```lua
Object.Thickness: number
```

#### Filled

```lua
Object.Filled: boolean
```

### Polyline

#### Points

```lua
Object.Points: { Vector2 }
```

An array of Vector2 points that make up the polyline.

#### Thickness

```lua
Object.Thickness: number
```

The thickness of the polyline.

#### Filled

```lua
Object.Filled: boolean
```

Whether the polyline is filled or not.
