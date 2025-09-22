# thread

## Functions

### create

```lua
function thread.create(name: string, callback: () -> ()): ()
```

Creates a new thread that runs the specified callback function. The thread is identified by the given name.

### suspend

```lua
function thread.suspend(name: string): ()
```

Suspends the thread with the specified name. If the thread is already suspended or does not exist, this function has no effect.

### resume

```lua
function thread.resume(name: string): ()
```

Resumes the thread with the specified name. If the thread is not suspended or does not exist, this function has no effect.

### terminate

```lua
function thread.terminate(name: string): ()
```

Terminates the thread with the specified name. If the thread does not exist, this function has no effect.

### clear

```lua
function thread.clear(): ()
```

Removes all existing threads.
