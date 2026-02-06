# Engine

## Overview

This article, and its sub-pages document how to utilize the DataModel (aka `game` global) to interact with the game state, and hierarchy.

## Instance

### declare

```lua
function Instance.declare(settings: {
    class: string | { string },
    name: string,
    callback: {
        get: (self) -> any,
        set: (self, value: any) -> (),
        Method: (...any) -> any
    }
}): ()
```

This function is used to declare new properties, or methods to all active instances that match the specified class.
