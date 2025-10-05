# Memory

## Requirements

Read through [buffer.md](../../luau/library/buffer.md "mention"), and [memory.md](../../reference/namespaces/memory.md "mention") first to understand key concepts in here.

## Overview

In this article, we will be covering our unique aspects, and how to properly (and also efficiently) use them.

## Buffers

Luau has powerful library named "buffer", which allows low-level manipulation with data (either manually created, or received via [#readbuffer](../../reference/namespaces/memory.md#readbuffer "mention")). You can use `readbuffer` to read chunks and/or pages of memory pretty much instantly. This is worth using if you need to read 3 values, for example reading a Vector3 from memory:

```lua
function readvector3(address: number): vector
    local data = memory.readbuffer(address, 12) :: buffer -- 12 bytes
    
    return vector.create(
        buffer.readf32(data, 0), -- the x
        buffer.readf32(data, 1), -- the y
        buffer.readf32(data, 2)  -- the z
    )
end
```

This is far faster than manually reading individual floats from memory, and this can even match the speed of `memory.readvector` if applied micro-optimizations.
