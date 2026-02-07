# Types
| Type    | Description     | Range / Format                 |
| :------ | :-------------- | :----------------------------- |
| **i8**  | Signed 8-bit    | \[-128, 127]                   |
| **u8**  | Unsigned 8-bit  | \[0, 255]                      |
| **i16** | Signed 16-bit   | \[-32,768, 32,767]             |
| **u16** | Unsigned 16-bit | \[0, 65,535]                   |
| **i32** | Signed 32-bit   | \[-2.1B, 2.1B]                 |
| **u32** | Unsigned 32-bit | \[0, 4.2B]                     |
| **i64** | Signed 64-bit   | Approximate (Casted to Double) |
| **u64** | Unsigned 64-bit | Approximate (Casted to Double) |
| **f32** | 32-bit Float    | IEEE 754 Single                |
| **f64** | 64-bit Float    | IEEE 754 Double                |
> **Note:** Luau does not natively support 64-bit integers. As a result, **i64** and **u64** operations are **approximations**; these values are cast to a double-precision float, which may lead to precision loss or rounding for extremely large integers.
# Functions

## read[type]
### Definition
```luau
function memory.read[type](address: number): number
function memory.read[type](source: userdata, offset: number): number
```
### Description
Reads data of a specific type from a raw memory address or an offset from a `userdata`.
Note that [type] has to be replaced with a valid type that can be found above. Valid example is: `memory.readu32(workspace, 0x50)`.

---

## memory.write[type]
### Definition
```luau
function memory.write[type](address: number, value: number): ()
function memory.write[type](destination: userdata, offset: number, value: number): ()
```
### Description
Writes a value of a specific type to a memory address or `userdata` offset. 
Note that [type] has to be replaced with a valid type that can be found above. Valid example is: `memory.writeu32(workspace, 0x50)`.

---

## memory.readbits
### Definition
```luau
function memory.readbits(address: number, bitOffset: number, bitSize: number): number
function memory.readbits(source: userdata, offset: number, bitOffset: number, bitSize: number): number
```
### Description
Reads a range of bits (up to 32) from the target, starting at `bitOffset`.

---

## memory.writebits
### Definition
```luau
function memory.writebits(address: number, bitOffset: number, bitSize: number, value: number): ()
function memory.writebits(destination: userdata, offset: number, bitOffset: number, bitSize: number, value: number): ()
```
### Description
Writes a range of bits (up to 32) from `value` to the destination at `bitOffset`.

---

## memory.readstring
### Definition
```luau
function memory.readstring(address: number): string
function memory.readstring(source: userdata, offset: number): string
```
### Description
Reads a raw null-terminated string or byte sequence from the target location.

---

## memory.writestring
### Definition
```luau
function memory.writestring(address: number, value: string): ()
function memory.writestring(destination: userdata, offset: number, value: string): ()
```
### Description
Writes the raw bytes of a string to the specified memory location.

---

## memory.readvector
### Definition
```luau
function memory.readvector(address: number): vector
function memory.readvector(source: userdata, offset: number): vector
```
### Description
Reads a 3-dimensional vector from memory.

---

## memory.writevector
### Definition
```luau
function memory.writevector(address: number, value: vector): ()
function memory.writevector(destination: userdata, offset: number, value: vector): ()
```
### Description
Writes a 3-dimensional vector to the target memory location.

---

## memory.readbuffer
### Definition
```luau
function memory.readbuffer(address: number, size: number): buffer
function memory.readbuffer(source: userdata, offset: number, size: number): buffer
```
### Description
Reads `size` bytes into a new Luau `buffer`. Highly efficient for bulk data extraction.

---

## memory.writebuffer
### Definition
```luau
function memory.writebuffer(address: number, value: buffer): ()
function memory.writebuffer(destination: userdata, offset: number, value: buffer): ()
```
### Description
Writes the contents of a Luau `buffer` directly to the specified memory location.

---

## memory.rtti
### Definition
```luau
function memory.rtti(address: number): string?
function memory.rtti(source: userdata, offset: number): string?
```
### Description
Retrieves the **Run-Time Type Information** name from the target address. Returns `nil` if no type info is available.

---

## memory.changed
### Definition
```luau
function memory.changed(address: number, type: string, callback: (self: userdata, new: any, old: any) -> (), iterations: number?): userdata
function memory.changed(source: userdata, offset: number, type: string, callback: (self: userdata, new: any, old: any) -> (), iterations: number?): userdata
```
### Description
Establishes a listener on a memory location that triggers the `callback` whenever the value changes. 
Available types: `i8`, `u8`, `i16`, `u16`, `i32`, `u32`, `i64`, `u64`, `f32`, `f64`, `string`.

# Properties
## memory.base
### Definition
```luau
memory.base: number
```
### Description
This is the base address for Roblox.
