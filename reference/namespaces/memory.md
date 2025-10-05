# memory

## Overview

Functions in the `memory` library allow direct low-level access to the client's memory.

These functions are unsafe, and if used incorrectly can lead to corruption / crashes, you should also be careful and always strictly type-check the read & writes

## Functions

### read

```lua
function memory.readi8(address: number): number
function memory.readi8(source: userdata, offset: number): number

function memory.readu8(address: number): number
function memory.readu8(source: userdata, offset: number): number

function memory.readi16(address: number): number
function memory.readi16(source: userdata, offset: number): number

function memory.readu16(address: number): number
function memory.readu16(source: userdata, offset: number): number

function memory.readi32(address: number): number
function memory.readi32(source: userdata, offset: number): number

function memory.readu32(address: number): number
function memory.readu32(source: userdata, offset: number): number

function memory.readi64(address: number): number
function memory.readi64(source: userdata, offset: number): number

function memory.readu64(address: number): number
function memory.readu64(source: userdata, offset: number): number

function memory.readf32(address: number): number
function memory.readf32(source: userdata, offset: number): number

function memory.readf64(address: number): number
function memory.readf64(source: userdata, offset: number): number
```

Used to read the data from the specified memory address or from the specified offset in the `userdata`.

Available types:

| Function | Type                         | Range                                                    |
| -------- | ---------------------------- | -------------------------------------------------------- |
| readi8   | signed 8-bit integer         | \[-128, 127]                                             |
| readu8   | unsigned 8-bit integer       | \[0, 255]                                                |
| readi16  | signed 16-bit integer        | \[-32,768, 32,767]                                       |
| readu16  | unsigned 16-bit integer      | \[0, 65,535]                                             |
| readi32  | signed 32-bit integer        | \[-2,147,483,648, 2,147,483,647]                         |
| readu32  | unsigned 32-bit integer      | \[0, 4,294,967,295]                                      |
| readi64  | signed 64-bit integer        | \[-9,223,372,036,854,775,808, 9,223,372,036,854,775,807] |
| readu64  | unsigned 64-bit integer      | \[0, 18,446,744,073,709,551,615]                         |
| readf32  | 32-bit floating-point number | Single-precision IEEE 754 number                         |
| readf64  | 64-bit floating-point number | Double-precision IEEE 754 number                         |

* Floating-point numbers are read and written using a format specified by IEEE 754.

### write

```lua
function memory.writei8(address: number, value: number): ()
function memory.writei8(destination: userdata, offset: number, value: number): ()

function memory.writeu8(address: number, value: number): ()
function memory.writeu8(destination: userdata, offset: number, value: number): ()

function memory.writei16(address: number, value: number): ()
function memory.writei16(destination: userdata, offset: number, value: number): ()

function memory.writeu16(address: number, value: number): ()
function memory.writeu16(destination: userdata, offset: number, value: number): ()

function memory.writei32(address: number, value: number): ()
function memory.writei32(destination: userdata, offset: number, value: number): ()

function memory.writeu32(address: number, value: number): ()
function memory.writeu32(destination: userdata, offset: number, value: number): ()

function memory.writei64(address: number, value: number): ()
function memory.writei64(destination: userdata, offset: number, value: number): ()

function memory.writeu64(address: number, value: number): ()
function memory.writeu64(destination: userdata, offset: number, value: number): ()

function memory.writef32(address: number, value: number): ()
function memory.writef32(destination: userdata, offset: number, value: number): ()

function memory.writef64(address: number, value: number): ()
function memory.writef64(destination: userdata, offset: number, value: number): ()
```

Used to write the data to the specified memory address or to the specified offset in the `userdata`.

* Ranges of acceptable values can be seen in the table above.

### readbits

```lua
function memory.readbits(address: number, bitOffset: number, bitSize: number): number
function memory.readbits(source: userdata, offset: number, bitOffset: number, bitSize: number): number
```

Used to read a range of `bitCount` bits from the source, at specified offset `bitOffset`, into an unsigned integer.

`bitCount` must be in `[0, 32]` range.

### writebits

```lua
function memory.writebits(address: number, bitOffset: number, bitSize: number, value: number): ()
function memory.writebits(destination: userdata, offset: number, bitOffset: number, bitSize: number, value: number): ()
```

Used to write a range of `bitCount` bits from the unsigned integer `value` to the destination, at specified offset `bitOffset`.

`bitCount` must be in `[0, 32]` range.

### readstring

```lua
function memory.readstring(address: number): string
function memory.readstring(source: userdata, offset: number): string
```

### writestring

```lua
function memory.writestring(address: number, value: string): ()
function memory.writestring(destination: userdata, offset: number, value: string): ()
```

Writes the bytes of the specified string to the specified memory address or to the specified offset in the `userdata`.

### readvector

```lua
function memory.readvector(address: number): vector
function memory.readvector(source: userdata, offset: number): vector
```

### writevector

```lua
function memory.writevector(address: number, value: vector): ()
function memory.writevector(destination: userdata, offset: number, value: vector): ()
```

Writes the bytes of the specified vector to the specified memory address or to the specified offset in the `userdata`.

### readbuffer

```lua
function memory.readbuffer(address: number, size: number): buffer
function memory.readbuffer(source: userdata, offset: number, size: number): buffer
```

Reads `size` bytes from the specified memory address or from the specified offset in the `userdata`, and returns a new `buffer` object containing those bytes.

{% hint style="info" %}
Note, that this function is extremely useful if you need to read multiple values at once, refer to [buffer.md](../../luau/library/buffer.md "mention")documentation to learn how to take advantage of this.
{% endhint %}

### writebuffer

```lua
function memory.writebuffer(address: number, value: buffer): ()
function memory.writebuffer(destination: userdata, offset: number, value: buffer): ()
```

Writes the bytes from the specified `buffer` object to the specified memory address or to the specified offset in the `userdata`.

{% hint style="info" %}
Note, that this function is extremely useful if you need to write multiple values at once, refer to [buffer.md](../../luau/library/buffer.md "mention")documentation to learn how to take advantage of this.
{% endhint %}

### rtti

```lua
function memory.rtti(address: number): string?
function memory.rtti(source: userdata, offset: number): string?
```

Given an address or a `userdata` and an offset, returns the RTTI type name if available, or nil otherwise.

* RTTI (Run-Time Type Information) is a mechanism that exposes type information at runtime. Not all objects have RTTI information.

### changed

```lua
function memory.changed(address: number, type: string, callback: (self: userdata, change: number | string, old: number | string) -> (), iterations: number?): userdata
function memory.changed(source: userdata, offset: number, type: string, callback: (self: userdata, change: number | string, old: number | string) -> (), iterations: number?): userdata
```

Watches the specified memory address or the specified offset in the `userdata` for changes. When a change is detected, the provided callback function is called with three arguments: the `userdata` itself, the new value, and the old value. `iterations` specifies how many times the callback should be invoked before the watch is automatically removed; if omitted, the watch remains active until manually removed.

Available types:

* `i8`, `u8`, `i16`, `u16`, `i32`, `u32`, `i64`, `u64`, `f32`, `f64`, `string`

### at

```lua
function memory.at(address: number): userdata
function memory.at(source: userdata, offset: number): userdata
```

Given an address or a `userdata` and an offset, returns a new `userdata` that points to the specified memory location.

* The returned `userdata` can be used with other `memory` functions to read from or write to that memory location.
