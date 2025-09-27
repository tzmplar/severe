# Globals

## Functions

### loadstring

```lua
function loadstring(code: string, chunk: string): (...) -> (... any)?
```

{% hint style="warning" %}
This function is deprecated, use [#compile](namespaces/luau.md#compile "mention") and [#load](namespaces/luau.md#load "mention") instead.
{% endhint %}

### pointer\_to\_userdata

```lua
function pointer_to_userdata(address: number): userdata
```

Converts the `address` into a `userdata` for usage with memory functions, if the address is a valid instance, it is converted to match the specified class.

### delfile

```lua
function delfile(path: string): ()
```

### writefile

```lua
function writefile(path: string, content: string): ()
```

### isfile

```lua
function isfile(path: string): boolean
```

### readfile

```lua
function readfile(path: string): string
```

### delfolder

```lua
function delfolder(path: string): ()
```

### makefolder

```lua
function makefolder(path: string): ()
```

### isfolder

```lua
function isfolder(path: string): boolean
```

### isrbxactive

```lua
function isrbxactive(): boolean
```

## References

### game [datamodel.md](engine/datamodel.md "mention")

### workspace [workspace.md](engine/workspace.md "mention")

### taskscheduler

A reference to Roblox's `TaskScheduler`  pointer.
