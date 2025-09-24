# luau

## Functions

### compile

```lua
function luau.compile(source: string, options: {
    optimizationLevel: 0 | 1 | 2?,
    coverageLevel: 0 | 1 | 2?,
    debugLevel: 0 | 1 | 2?
}): string
```

Compiles the given source code into Luau bytecode. An error will be thrown if the source code contains syntax errors or other issues that prevent successful compilation.

#### Example

```lua
local bytecode = luau.compile("print('Hello, World!')", {
    optimizationLevel = 2,
    coverageLevel = 0,
    debugLevel = 1,
})

local func = load(bytecode)
func()  -- Outputs: Hello, World!
```

### load

```lua
function luau.load(bytecode: string, options: {
    debugName: string?,
    environment: { [string]: any }?,
    injectGlobals: boolean?,
    codegenEnabled: boolean?
}): (... any?) -> (... any?)
```

Loads a function from the given Luau bytecode string. An error will be thrown if the bytecode is invalid or cannot be loaded. Note that if `environment` is enabled, native code generation and optimizations are forcefully disabled.

#### Example

```lua
local bytecode = luau.compile("return 42", {
    optimizationLevel = 2,
    coverageLevel = 0,
    debugLevel = 1,
})

local func = luau.load(bytecode, "MyChunk")
print(func())  -- Outputs: 42
```
