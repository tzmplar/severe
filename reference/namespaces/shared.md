# shared

## Functions

### get

```lua
function shared.get(key: string): any
```

Returns the value associated with the specified key in the shared storage, or nil if the key does not exist.

### set

```lua
function shared.set(key: string, value: any): ()
```

Sets the value associated with the specified key in the shared storage. If the key already exists, its value is updated.

### remove

```lua
function shared.remove(key: string): ()
```

Removes the specified key and its associated value from the shared storage. If the key does not exist, this function has no effect.

### has

```lua
function shared.has(key: string): boolean
```

Returns true if the specified key exists in the shared storage, false otherwise.
