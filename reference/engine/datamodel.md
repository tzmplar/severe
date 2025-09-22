# DataModel

Documentation for these functions and properties can be found [here](https://create.roblox.com/docs/reference/engine/classes/DataModel).

## Properties

### PlaceId

```lua
Instance.PlaceId: number
```

### GameId

```lua
Instance.GameId: number
```

### JobId

```lua
Instance.JobId: string
```

## Methods

### HttpGet

```lua
function DataModel:HttpGet(url: string, content: string): unknown
```

### HttpPost

```lua
function DataModel:HttpPost(url: string, data: string, content: string, accept: string, cookie: string?, referer: string?, origin: string?): unknown
```

### GetService

```lua
function DataModel:GetService(name: string): Instance
```

### GetHwid

```lua
function DataModel:GetHwid(): string
```
