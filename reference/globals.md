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

Whitelisted extensions are: `.lua`, `.txt`, `.md`, `.png`, `.dds`, `.bin`, `.gif`, `.jpg`.

### isfile

```lua
function isfile(path: string): boolean
```

### loadfile

```lua
function loadfile(path: string): (... any) -> (... any)?
```

Reads the file contents, and interprets it as Luau source-code. This is directly similar to:\


```lua
loadstring(readfile("my_file.lua"))
```

### dofile

```lua
function dofile(path: string): ()
```

Similar to `loadfile`, however instead of returning a callback, it directly calls it.

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

### isrightpressed

```lua
function isrightpressed(): boolean
```

### isleftpressed

```lua
function isleftpressed(): boolean
```

### smoothmouse\_exponential

```lua
function smoothmouse_exponential(origin: vector, target: vector, speed: number): ()
```

### smoothmouse\_linear

```lua
function smoothmouse_linear(origin: vector, target: vector, speed: number): ()
```

### mouse1press

```lua
function mouse1press(): ()
```

### mouse2press

```lua
function mouse2press(): ()
```

### mouse2click

```lua
function mouse2click(): ()
```

### mouse1click

```lua
function mouse1click(): ()
```

### keypress

```lua
function keypress(code: number): ()
```

### keyrelease

```lua
function keyrelease(code: number): ()
```

### getpressedkeys

```lua
function getpressedkeys(): { number }
```

### getpressedkey

```lua
function getpressedkey(): number
```

### setclipboard

```lua
function setclipboard(payload: string): ()
```

### getmouseposition

```lua
function getmouseposition(): vector
```

### send\_notification

```lua
function send_notification(content: string): ()
```

### queue\_on\_teleport

```lua
function queue_on_teleport(code: string): ()
```

### block\_roblox\_window

```lua
function block_roblox_window(state: boolean): ()
```

## References

### game [datamodel.md](engine/datamodel.md "mention")

### workspace [workspace.md](engine/workspace.md "mention")

### taskscheduler

A reference to Roblox's `TaskScheduler`  pointer.
