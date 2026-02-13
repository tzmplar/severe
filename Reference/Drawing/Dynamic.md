# Dynamic

## Overview

Dynamic drawing allows you to automatically attach drawing objects to 3D world positions or instances. Drawing objects automatically update their screen position based on the camera's view of the linked points.

## Functions

### Drawing.attach

**Definition**

```luau
function Drawing.attach(config: { [Drawing]: AttachmentConfig }): Cluster
```

**Parameters**

| Name   | Type                              | Description                                                            |
| ------ | --------------------------------- | ---------------------------------------------------------------------- |
| config | { [Drawing]: AttachmentConfig } | A table mapping drawing objects to their attachment configurations |

**Returns**

| Type    | Description                                                      |
| ------- | ---------------------------------------------------------------- |
| Cluster | A cluster object that can be destroyed, paused, or resumed |

**Description**

Attaches drawing objects to 3D points in the world. The drawing objects will automatically update their screen positions based on the camera's view of the linked points. Each drawing object can be configured with different attachment properties depending on its type.

**Attachment Configurations**

For positional drawings (Square, Circle, Image, Text):

| Property    | Type         | Description                                   |
| ----------- | ------------ | --------------------------------------------- |
| Link        | Point        | The point to attach the drawing to           |
| Size        | UDim2        | Size of the drawing (Scale/Offset)           |
| AnchorPoint | Vector2      | Anchor point for positioning (0-1 range)     |

For line-based drawings (Line, Polyline):

| Property | Type  | Description                    |
| -------- | ----- | ------------------------------ |
| From     | Point | Starting point of the line    |
| To       | Point | Ending point of the line      |

**Code Samples**

```luau
local Head = PointInstance.new(game.Players.LocalPlayer.Character.Head :: BasePart)
local Mesh = PointInstance.new(workspace.SpawnLocation :: BasePart)

local Square = Drawing.new 'Square'
Square.Visible = true
Square.Filled = true
Square.Color = Color3.fromRGB(255, 255, 125)

local Line = Drawing.new 'Line'
Line.Visible = true
Line.Color = Color3.fromRGB(255, 0, 0)
Line.Thickness = 2

local Cluster = Drawing.attach {
    [Square] = {
        Link = Head,
        Size = UDim2.fromScale(1, 1),
        AnchorPoint = Vector2.new(0.5, 0.5)
    },

    [Line] = {
        From = Head,
        To = Mesh,
    }
}

-- Later, when done:
Cluster:Destroy()
```

***

## Classes

### PointInstance

**Definition**

```luau
PointInstance.new(instance: BasePart): PointInstance
```

**Description**

Creates a point tracker for an instance with a CFrame property. The point automatically tracks the instance's position in the world. Only instances that have a CFrame property (e.g., BasePart) can be used.

**Properties**

| Property | Type    | Description                                           |
| -------- | ------- | ----------------------------------------------------- |
| CFrame   | CFrame  | The current CFrame of the tracked instance           |
| Size     | Vector3 | The current Size of the tracked instance             |
| Active   | boolean | Whether the point is actively tracking the instance  |

**Methods**

| Method  | Description                              |
| ------- | ---------------------------------------- |
| Destroy | Stops tracking and cleans up resources  |

**Code Samples**

```luau
local Head = PointInstance.new(game.Players.LocalPlayer.Character.Head :: BasePart)

-- Access properties
print(Head.CFrame)
print(Head.Size)
print(Head.Active)

-- Clean up when done
Head:Destroy()
```

***

### Point3D

**Definition**

```luau
Point3D.new(position: Vector3): Point3D
```

**Description**

Creates a point at a fixed world-space position. The point represents a static location in 3D space.

**Properties**

| Property | Type    | Description                                    |
| -------- | ------- | ---------------------------------------------- |
| Position | Vector3 | The world-space position of the point         |
| Active   | boolean | Whether the point is active                   |

**Methods**

| Method  | Description                             |
| ------- | --------------------------------------- |
| Destroy | Cleans up the point and its resources  |

**Code Samples**

```luau
local StaticPoint = Point3D.new(Vector3.new(0, 10, 0))

-- Access properties
print(StaticPoint.Position)
print(StaticPoint.Active)

-- Clean up when done
StaticPoint:Destroy()
```

***

### Cluster

**Description**

A cluster is returned by `Drawing.attach` and manages a group of attached drawing objects. It provides methods to control the lifecycle of all attached drawings.

**Methods**

| Method  | Description                                               |
| ------- | --------------------------------------------------------- |
| Destroy | Destroys the cluster and all attached drawing objects    |
| Pause   | Pauses automatic updates for all drawings in the cluster |
| Resume  | Resumes automatic updates for all drawings in the cluster|

**Code Samples**

```luau
local Head = PointInstance.new(game.Players.LocalPlayer.Character.Head :: BasePart)

local Square = Drawing.new 'Square'
Square.Visible = true

local Cluster = Drawing.attach {
    [Square] = {
        Link = Head,
        Size = UDim2.fromScale(1, 1),
        AnchorPoint = Vector2.new(0.5, 0.5)
    }
}

-- Pause updates
Cluster:Pause()

-- Resume updates
Cluster:Resume()

-- Clean up everything
Cluster:Destroy()
```
