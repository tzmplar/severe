# buffer

Buffer is an object that represents a fixed-size mutable block of memory.

All operations on a buffer are provided using the 'buffer' library functions.

Many of the functions accept an offset in bytes from the start of the buffer.

Offset of 0 from the start of the buffer memory block accesses the first byte.

All offsets, counts and sizes should be non-negative integer numbers.

If the bytes that are accessed by any read or write operation are outside the buffer memory, an error is thrown.

## create

```lua
function buffer.create(size: number): buffer
```

Creates a buffer of the requested size with all bytes initialized to 0.

Size limit is 1GB or 1,073,741,824 bytes.

## fromstring

```lua
function buffer.fromstring(str: string): buffer
```

Creates a buffer initialized to the contents of the string.

The size of the buffer equals to the length of the string.

## tostring

```lua
function buffer.tostring(b: buffer): string
```

Returns the buffer data as a string.

## len

```lua
function buffer.len(b: buffer): number
```

Returns the size of the buffer in bytes.

## read

```lua
function buffer.readi8(b: buffer, offset: number): number
function buffer.readu8(b: buffer, offset: number): number

function buffer.readi16(b: buffer, offset: number): number
function buffer.readu16(b: buffer, offset: number): number

function buffer.readi32(b: buffer, offset: number): number
function buffer.readu32(b: buffer, offset: number): number

function buffer.readf32(b: buffer, offset: number): number
function buffer.readf64(b: buffer, offset: number): number
```

Used to read the data from the buffer by reinterpreting bytes at the offset as the type in the argument and converting it into a number.

Available types:

| Function | Type                         | Range                            |
| -------- | ---------------------------- | -------------------------------- |
| readi8   | signed 8-bit integer         | \[-128, 127]                     |
| readu8   | unsigned 8-bit integer       | \[0, 255]                        |
| readi16  | signed 16-bit integer        | \[-32,768, 32,767]               |
| readu16  | unsigned 16-bit integer      | \[0, 65,535]                     |
| readi32  | signed 32-bit integer        | \[-2,147,483,648, 2,147,483,647] |
| readu32  | unsigned 32-bit integer      | \[0, 4,294,967,295]              |
| readf32  | 32-bit floating-point number | Single-precision IEEE 754 number |
| readf64  | 64-bit floating-point number | Double-precision IEEE 754 number |

* Floating-point numbers are read and written using a format specified by IEEE 754.
* If a floating-point value matches any of bit patterns that represent a NaN (not a number), returned value might be converted to a different quiet NaN representation.
* Read and write operations use the little endian byte order.
* Integer numbers are read and written using two's complement representation.

## write

```lua
function buffer.writei8(b: buffer, offset: number, value: number): ()
function buffer.writeu8(b: buffer, offset: number, value: number): ()

function buffer.writei16(b: buffer, offset: number, value: number): ()
function buffer.writeu16(b: buffer, offset: number, value: number): ()

function buffer.writei32(b: buffer, offset: number, value: number): ()
function buffer.writeu32(b: buffer, offset: number, value: number): ()

function buffer.writef32(b: buffer, offset: number, value: number): ()
function buffer.writef64(b: buffer, offset: number, value: number): ()
```

Used to write data to the buffer by converting the number into the type in the argument and reinterpreting it as individual bytes.

* Ranges of acceptable values can be seen in the table above.
* When writing integers, the number is converted using `bit32` library rules.
* Values that are out-of-range will take less significant bits of the full number.
* For example, writing 43,981 (0xabcd) using writei8 function will take 0xcd and interpret it as an 8-bit signed number -51.
* It is still recommended to keep all numbers in range of the target type.
* Results of converting special number values (inf/nan) to integers are platform-specific.

## readstring

```lua
function buffer.readstring(b: buffer, offset: number, count: number): string
```

Used to read a string of length 'count' from the buffer at specified offset.

## writestring

```lua
function buffer.writestring(b: buffer, offset: number, value: string, count: number?): ()
```

Used to write data from a string into the buffer at a specified offset.

If an optional 'count' is specified, only 'count' bytes are taken from the string.

Count cannot be larger than the string length.

## readbits

```lua
buffer.readbits(b: buffer, bitOffset: number, bitCount: number): number
```

Used to read a range of `bitCount` bits from the buffer, at specified offset `bitOffset`, into an unsigned integer.

`bitCount` must be in `[0, 32]` range.

## writebits

```lua
buffer.writebits(b: buffer, bitOffset: number, bitCount: number, value: number): ()
```

Used to write `bitCount` bits from `value` into the buffer at specified offset `bitOffset`.

`bitCount` must be in `[0, 32]` range.

## copy

```lua
function buffer.copy(target: buffer, targetOffset: number, source: buffer, sourceOffset: number?, count: number?): ()
```

Copy 'count' bytes from 'source' starting at offset 'sourceOffset' into the 'target' at 'targetOffset'.

It is possible for 'source' and 'target' to be the same. Copying an overlapping region inside the same buffer acts as if the source region is copied into a temporary buffer and then that buffer is copied over to the target.

If 'sourceOffset' is nil or is omitted, it defaults to 0.

If 'count' is 'nil' or is omitted, the whole 'source' data starting from 'sourceOffset' is copied.

## fill

```lua
function buffer.fill(b: buffer, offset: number, value: number, count: number?): ()
```

Sets the 'count' bytes in the buffer starting at the specified 'offset' to the 'value'.

If 'count' is 'nil' or is omitted, all bytes from the specified offset until the end of the buffer are set.
