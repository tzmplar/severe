# Functions

## keypress
### Definition
```lua
function keypress(keycode: number): ()
```
### Parameters

| Name    | Type   | Description                  |
|---------|--------|------------------------------|
| keycode | number | Virtual keycode to press     |

### Description
Simulates a key press for the given virtual keycode.

> **Note:** Virtual key codes: [Microsoft Docs](https://docs.microsoft.com/en-us/windows/desktop/inputdev/virtual-key-codes)

---

## keyrelease
### Definition
```lua
function keyrelease(keycode: number): ()
```
### Parameters

| Name    | Type   | Description                     |
|---------|--------|---------------------------------|
| keycode | number | Virtual keycode to release      |

### Description
Simulates a key release for the given virtual keycode.

---

## getpressedkey
### Definition
```lua
function getpressedkey(): string
```
### Returns
```horizontal
### string
```
### Description
Returns the name of the last pressed key.

---

## getpressedkeys
### Definition
```lua
function getpressedkeys(): { string }
```
### Returns
```horizontal
### { string }
```
### Description
Returns an array of currently pressed key names.

---

## isleftclicked
### Definition
```lua
function isleftclicked(): boolean
```
### Returns
```horizontal
### boolean
```
### Description
Returns `true` if left mouse button was clicked.

---

## isrightclicked
### Definition
```lua
function isrightclicked(): boolean
```
### Returns
```horizontal
### boolean
```
### Description
Returns `true` if right mouse button was clicked.

---

## isleftpressed
### Definition
```lua
function isleftpressed(): boolean
```
### Returns
```horizontal
### boolean
```
### Description
Returns `true` if left mouse button is held down.

---

## isrightpressed
### Definition
```lua
function isrightpressed(): boolean
```
### Returns
```horizontal
### boolean
```
### Description
Returns `true` if right mouse button is held down.

---

## mousemoverel
### Definition
```lua
function mousemoverel(x: number, y: number): ()
```
### Parameters

| Name | Type   | Description             |
|------|--------|-------------------------|
| x    | number | Relative X offset       |
| y    | number | Relative Y offset       |

### Description
Moves mouse by relative X/Y coordinates.

---

## mousemoveabs
### Definition
```lua
function mousemoveabs(x: number, y: number): ()
```
### Parameters

| Name | Type   | Description           |
|------|--------|-----------------------|
| x    | number | Absolute X position   |
| y    | number | Absolute Y position   |

### Description
Moves mouse to absolute X/Y screen coordinates.

---

## mousescroll
### Definition
```lua
function mousescroll(pixels: number): ()
```
### Parameters

| Name   | Type   | Description              |
| ------ | ------ | ------------------------ |
| pixels | number | Scroll distance (pixels) |

### Description
Scrolls mouse wheel by specified pixels.

---

## mouse1click
### Definition
```lua
function mouse1click(): ()
```
### Description
Simulates a left mouse button click.

---

## mouse1press
### Definition
```lua
function mouse1press(): ()
```
### Description
Simulates a left mouse button press (hold).

---

## mouse1release
### Definition
```lua
function mouse1release(): ()
```
### Description
Simulates a left mouse button release.

---

## mouse2click
### Definition
```lua
function mouse2click(): ()
```
### Description
Simulates a right mouse button click.

---

## mouse2press
### Definition
```lua
function mouse2press(): ()
```
### Description
Simulates a right mouse button press (hold).

---

## mouse2release
### Definition
```lua
function mouse2release(): ()
```
### Description
Simulates a right mouse button release.