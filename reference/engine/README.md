# Engine

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
