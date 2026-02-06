# coroutine

## create

```lua
function coroutine.create(f: function): thread
```

Returns a new coroutine that, when resumed, will run function `f`.

## running

```lua
function coroutine.running(): thread?
```

Returns the currently running coroutine, or `nil` if the code is running in the main coroutine (depending on the host environment setup, main coroutine may never be used for running code).

## status

```lua
function coroutine.status(co: thread): string
```

Returns the status of the coroutine, which can be `"running"`, `"suspended"`, `"normal"` or `"dead"`. Dead coroutines have finished their execution and can not be resumed, but their state can still be inspected as they are not dead from the garbage collector point of view.

## wrap

```lua
function coroutine.wrap(f: function): function
```

Creates a new coroutine and returns a function that, when called, resumes the coroutine and passes all arguments along to the suspension point. When the coroutine yields or finishes, the wrapped function returns with all values returned at the suspension point.

## yield

```lua
function coroutine.yield(args: ...any): ...any
```

Yields the currently running coroutine and passes all arguments along to the code that resumed the coroutine. The coroutine becomes suspended; when the coroutine is resumed again, the resumption arguments will be forwarded to `yield` which will behave as if it returned all of them.

## isyieldable

```lua
function coroutine.isyieldable(): boolean
```

Returns `true` iff the currently running coroutine can yield. Yielding is prohibited when running inside metamethods like `__index` or C functions like `table.foreach` callback, with the exception of `pcall`/`xpcall`.

## resume

```lua
function coroutine.resume(co: thread, args: ...any): (boolean, ...any)
```

Resumes the coroutine and passes the arguments along to the suspension point. When the coroutine yields or finishes, returns `true` and all values returned at the suspension point. If an error is raised during coroutine resumption, this function returns `false` and the error object, similarly to `pcall`.

## close

```lua
function coroutine.close(co: thread): (boolean, any?)
```

Closes the coroutine which puts coroutine in the dead state. The coroutine must be dead or suspended - in particular it can't be currently running. If the coroutine that's being closed was in an error state, returns `false` along with an error object; otherwise returns `true`. After closing, the coroutine can't be resumed and the coroutine stack becomes empty.
