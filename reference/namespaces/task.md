# task

## Functions

### defer

```lua
function task.defer(callback: function | thread, ... any) -> thread
```

### spawn

```lua
function task.spawn(callback: function | thread, ... any) -> thread
```

### wait

```lua
function task.wait(amount: number) -> number
```

### delay

```lua
function task.delay(amount: number, callback: function | thread) -> thread
```

### cancel

```lua
function task.cancel(t: thread) -> ()
```

