# task

Task scheduler library providing thread management functions for asynchronous execution.

## Functions

## task.spawn

### Definition

```luau
function task.spawn(functionOrThread: (() -> ()) | thread, ...: any): thread
```

### Parameters

| Name             | Type                       | Description                                      |
| ---------------- | -------------------------- | ------------------------------------------------ |
| functionOrThread | (() -> ()) \| thread       | The function or thread to execute immediately    |
| ...              | any                        | Optional arguments to pass to the function       |

### Returns

<table data-header-hidden data-full-width="false"><thead><tr><th valign="middle">Type</th></tr></thead><tbody><tr><td valign="middle"><pre class="language-luau"><code class="lang-luau">thread
</code></pre></td></tr></tbody></table>

### Description

Immediately executes the provided function or resumes the provided thread in a separate thread without yielding the current thread. The new thread runs in parallel with the calling thread. Returns the thread that was spawned.

### Code Samples

```luau
-- Spawn a function
task.spawn(function()
    print("This runs immediately in a new thread")
    task.wait(1)
    print("After 1 second")
end)

-- Spawn with arguments
task.spawn(function(message, delay)
    task.wait(delay)
    print(message)
end, "Hello!", 2)

-- Spawn a thread
local thread = coroutine.create(function()
    print("Thread spawned")
end)
task.spawn(thread)
```

---

## task.defer

### Definition

```luau
function task.defer(functionOrThread: (() -> ()) | thread, ...: any): thread
```

### Parameters

| Name             | Type                       | Description                                      |
| ---------------- | -------------------------- | ------------------------------------------------ |
| functionOrThread | (() -> ()) \| thread       | The function or thread to execute after deferral |
| ...              | any                        | Optional arguments to pass to the function       |

### Returns

<table data-header-hidden data-full-width="false"><thead><tr><th valign="middle">Type</th></tr></thead><tbody><tr><td valign="middle"><pre class="language-luau"><code class="lang-luau">thread
</code></pre></td></tr></tbody></table>

### Description

Defers the execution of the provided function or thread until the next resumption cycle. Unlike `task.spawn`, deferred functions do not run immediately but wait until the current thread yields. This is useful for scheduling work that should happen after the current frame or operation completes.

### Code Samples

```luau
-- Defer a function
task.defer(function()
    print("This runs after the current thread yields")
end)

-- Defer with arguments
task.defer(function(text)
    print("Deferred: " .. text)
end, "Hello, world!")

print("This prints first")

-- Output:
-- This prints first
-- This runs after the current thread yields
-- Deferred: Hello, world!
```

---

## task.cancel

### Definition

```luau
function task.cancel(thread: thread): ()
```

### Parameters

| Name   | Type   | Description                 |
| ------ | ------ | --------------------------- |
| thread | thread | The thread to cancel        |

### Description

Cancels a thread that was created with `task.spawn`, `task.defer`, or `task.delay`. Once cancelled, the thread will not resume execution. If the thread is already completed or cancelled, this function has no effect.

### Code Samples

```luau
-- Cancel a spawned thread
local thread = task.spawn(function()
    task.wait(5)
    print("This will never print")
end)

task.wait(1)
task.cancel(thread)
print("Thread cancelled")

-- Cancel a deferred thread
local deferredThread = task.defer(function()
    print("This will not execute")
end)
task.cancel(deferredThread)
```

---

## task.wait

### Definition

```luau
function task.wait(duration: number?): number
```

### Parameters

| Name     | Type    | Description                                                       |
| -------- | ------- | ----------------------------------------------------------------- |
| duration | number? | The time in seconds to wait. Defaults to 0 if not provided.      |

### Returns

<table data-header-hidden data-full-width="false"><thead><tr><th valign="middle">Type</th></tr></thead><tbody><tr><td valign="middle"><pre class="language-luau"><code class="lang-luau">number
</code></pre></td></tr></tbody></table>

### Description

Yields the current thread for at least the specified duration in seconds. Returns the actual time elapsed. This is the preferred way to yield execution in modern Luau code, replacing the legacy `wait()` function.

### Code Samples

```luau
-- Wait for 2 seconds
local elapsed = task.wait(2)
print("Waited for " .. elapsed .. " seconds")

-- Wait with default duration
task.wait() -- Waits for the next frame/cycle

-- Use in a loop
for i = 1, 5 do
    print("Iteration " .. i)
    task.wait(1)
end

-- Countdown timer
for i = 10, 1, -1 do
    print(i)
    task.wait(1)
end
print("Blast off!")
```
