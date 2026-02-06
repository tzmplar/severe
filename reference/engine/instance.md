# Instance

Documentation for these functions and properties can be found [here](https://create.roblox.com/docs/reference/engine/classes/Instance).\
This object serves as the base class for everything.

## Properties

### Name

```lua
Instance.Name: string
```

### ClassName

```lua
Instance.ClassName: string
```

### Parent

```lua
Instance.Parent: Instance
```

### Data

```lua
Instance.Data: string
```

Hexadecimal representation of the Instance's address, note that this is a string, you can use `tonumber` to convert it into Lua's number representation.

## Methods

### GetTags

```lua
function Instance:GetTags(): { string }
```

### HasTag

```lua
function Instance:HasTag(name: string): boolean
```

### AddTag

```lua
function Instance:AddTag(name: string): ()
```

### RemoveTag

```lua
function Instance:RemoveTag(name: string): ()
```

### ClearTags

```lua
function Instance:ClearTags(): ()
```

### GetAttribute

```lua
function Instance:GetAttribute(name: string): ()
```

### GetAttributes

```lua
function Instance:GetAttributes(): { string }
```

### SetAttribute

```lua
function Instance:SetAttribute(name: string, value: any): ()
```

### FindFirstChildOfClass

```lua
function Instance:FindFirstChildOfClass(name: string): Instance?
```

### FindFirstChild

```lua
function Instance:FindFirstChild(name: string): Instance?
```

### FindFirstAncestorOfClass

```lua
function Instance:FindFirstAncestorOfClass(name: string): Instance?
```

### FindFirstAncestor

```lua
function Instance:FindFirstAncestor(name: string): Instance?
```

### GetChildren

```lua
function Instance:GetChildren(): { Instance }
```

### GetDescendants

```lua
function Instance:GetDescendants(): { Instance }
```

### WaitForChild

```lua
function Instance:WaitForChild(name: string): Instance?
```

### FindFirstDescendant

```lua
function Instance:FindFirstDescendant(name: string): Instance?
```

### IsAncestorOf

```lua
function Instance:IsAncestorOf(Object: Instance): boolean
```

### IsDescendantOf

```lua
function Instance:IsDescendantOf(Object: Instance): boolean
```

### Destroy

```lua
function Instance:Destroy(): ()
```
