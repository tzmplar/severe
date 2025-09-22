# debug

## info

```lua
function debug.info(co: thread, level: number, s: string): ...any
function debug.info(level: number, s: string): ...any
function debug.info(f: function, s: string): ...any
```

Given a stack frame or a function, and a string that specifies the requested information, returns the information about the stack frame or function.

Each character of `s` results in additional values being returned in the same order as the characters appear in the string:

* `s` returns source path for the function
* `l` returns the line number for the stack frame or the line where the function is defined when inspecting a function object
* `n` returns the name of the function, or an empty string if the name is not known
* `f` returns the function object itself
* `a` returns the number of arguments that the function expects followed by a boolean indicating whether the function is variadic or not

For example, `debug.info(2, "sln")` returns source file, current line and function name for the caller of the current function.

## traceback

```lua
function debug.traceback(co: thread, msg: string?, level: number?): string
function debug.traceback(msg: string?, level: number?): string
```

Produces a stringified callstack of the given thread, or the current thread, starting with level `level`. If `msg` is specified, then the resulting callstack includes the string before the callstack output, separated with a newline. The format of the callstack is human-readable and subject to change.
