# Static

## Functions

### Drawing.new

**Definition**

```luau
function Drawing.new(class: string): userdata
```

**Parameters**

| Name  | Type   | Description                                                |
| ----- | ------ | ---------------------------------------------------------- |
| class | string | Valid classes can be found under the "Classes" sub-folder. |

**Description**

Will create a new static drawing on the screen, it's retained, meaning you will have to manually describe it (set it's color, position, size), and manually clean-up.

***

### Drawing.clear

**Definition**

```luau
function Drawing.clear(): ()
```

**Description**

Will clear all the static objects created, this will also include static objects that were created by other scripts.

***

> **Note:** Not removing static drawings can result in degraded performance and memory leaks. Creating a lot of static drawings may result in render thread error, this is a known issue.
