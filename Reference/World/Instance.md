# Instance

The base class for all objects in the game world.

## GetTags

### Definition

```luau
function Instance:GetTags(): { string }
```

### Returns

| Type       |
| ---------- |
| { string } |

### Description

Returns an array of all tags assigned to this instance.

***

## HasTag

### Definition

```luau
function Instance:HasTag(tag: string): boolean
```

### Parameters

| Name | Type   | Description          |
| ---- | ------ | -------------------- |
| tag  | string | The tag to check for |

### Returns

| Type    |
| ------- |
| boolean |

### Description

Returns `true` if the instance has the specified tag, otherwise `false`.

***

## AddTag

### Definition

```luau
function Instance:AddTag(tag: string): ()
```

### Parameters

| Name | Type   | Description    |
| ---- | ------ | -------------- |
| tag  | string | The tag to add |

### Description

Adds a tag to this instance.

***

## RemoveTag

### Definition

```luau
function Instance:RemoveTag(tag: string): ()
```

### Parameters

| Name | Type   | Description       |
| ---- | ------ | ----------------- |
| tag  | string | The tag to remove |

### Description

Removes a tag from this instance.

***

## ClearTags

### Definition

```luau
function Instance:ClearTags(): ()
```

### Description

Removes all tags from this instance.

***

## GetAttributes

### Definition

```luau
function Instance:GetAttributes(): { [string]: any }
```

### Returns

| Type               |
| ------------------ |
| { [string]: any }  |

### Description

Returns a dictionary of all attributes assigned to this instance.

***

## GetAttribute

### Definition

```luau
function Instance:GetAttribute(name: string): any
```

### Parameters

| Name | Type   | Description        |
| ---- | ------ | ------------------ |
| name | string | The attribute name |

### Returns

| Type |
| ---- |
| any  |

### Description

Returns the value of the specified attribute, or `nil` if it doesn't exist.

***

## SetAttribute

### Definition

```luau
function Instance:SetAttribute(name: string, value: any): ()
```

### Parameters

| Name  | Type   | Description        |
| ----- | ------ | ------------------ |
| name  | string | The attribute name |
| value | any    | The attribute value|

### Description

Sets the value of an attribute on this instance. Setting to `nil` removes the attribute.

***

## FindFirstChild

### Definition

```luau
function Instance:FindFirstChild(name: string): Instance?
```

### Parameters

| Name | Type   | Description            |
| ---- | ------ | ---------------------- |
| name | string | The name of the child  |

### Returns

| Type      |
| --------- |
| Instance? |

### Description

Returns the first child with the specified name, or `nil` if not found.

***

## FindFirstChildOfClass

### Definition

```luau
function Instance:FindFirstChildOfClass(className: string): Instance?
```

### Parameters

| Name      | Type   | Description      |
| --------- | ------ | ---------------- |
| className | string | The class name   |

### Returns

| Type      |
| --------- |
| Instance? |

### Description

Returns the first child of the specified class, or `nil` if not found.

***

## FindFirstDescendant

### Definition

```luau
function Instance:FindFirstDescendant(name: string): Instance?
```

### Parameters

| Name | Type   | Description                |
| ---- | ------ | -------------------------- |
| name | string | The name of the descendant |

### Returns

| Type      |
| --------- |
| Instance? |

### Description

Returns the first descendant with the specified name, or `nil` if not found.

***

## FindFirstAncestor

### Definition

```luau
function Instance:FindFirstAncestor(name: string): Instance?
```

### Parameters

| Name | Type   | Description              |
| ---- | ------ | ------------------------ |
| name | string | The name of the ancestor |

### Returns

| Type      |
| --------- |
| Instance? |

### Description

Returns the first ancestor with the specified name, or `nil` if not found.

***

## FindFirstAncestorOfClass

### Definition

```luau
function Instance:FindFirstAncestorOfClass(className: string): Instance?
```

### Parameters

| Name      | Type   | Description    |
| --------- | ------ | -------------- |
| className | string | The class name |

### Returns

| Type      |
| --------- |
| Instance? |

### Description

Returns the first ancestor of the specified class, or `nil` if not found.

***

## GetChildren

### Definition

```luau
function Instance:GetChildren(): { Instance }
```

### Returns

| Type        |
| ----------- |
| { Instance }|

### Description

Returns an array of all direct children of this instance.

***

## GetDescendants

### Definition

```luau
function Instance:GetDescendants(): { Instance }
```

### Returns

| Type        |
| ----------- |
| { Instance }|

### Description

Returns an array of all descendants of this instance.

***

## WaitForChild

### Definition

```luau
function Instance:WaitForChild(name: string, timeout: number?): Instance?
```

### Parameters

| Name    | Type    | Description                       |
| ------- | ------- | --------------------------------- |
| name    | string  | The name of the child to wait for |
| timeout | number? | Optional timeout in seconds       |

### Returns

| Type      |
| --------- |
| Instance? |

### Description

Waits for a child with the specified name to be added. Returns the child when found, or `nil` if timeout is reached.

***

## IsAncestorOf

### Definition

```luau
function Instance:IsAncestorOf(instance: Instance): boolean
```

### Parameters

| Name     | Type     | Description           |
| -------- | -------- | --------------------- |
| instance | Instance | The instance to check |

### Returns

| Type    |
| ------- |
| boolean |

### Description

Returns `true` if this instance is an ancestor of the specified instance.

***

## IsDescendantOf

### Definition

```luau
function Instance:IsDescendantOf(instance: Instance): boolean
```

### Parameters

| Name     | Type     | Description           |
| -------- | -------- | --------------------- |
| instance | Instance | The instance to check |

### Returns

| Type    |
| ------- |
| boolean |

### Description

Returns `true` if this instance is a descendant of the specified instance.

***

## Destroy

### Definition

```luau
function Instance:Destroy(): ()
```

### Description

Destroys the instance and removes it from the game. All descendants are also destroyed.

***

## Name

### Definition

```luau
Instance.Name: string
```

### Description

The name of the instance.

***

## ClassName

### Definition

```luau
Instance.ClassName: string
```

### Description

The class name of the instance (read-only).

***

## Parent

### Definition

```luau
Instance.Parent: Instance?
```

### Description

The parent instance. Can be set to `nil` or another instance.

***

## Data

### Definition

```luau
Instance.Data: any
```

### Description

Custom data storage for the instance.
