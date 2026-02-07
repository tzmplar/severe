# DataModel

The DataModel (accessed via the `game` global) is the root object of the game hierarchy.

## HttpGet

### Definition

```luau
function game:HttpGet(url: string): string
```

### Parameters

| Name | Type   | Description                        |
| ---- | ------ | ---------------------------------- |
| url  | string | The URL to send a GET request to   |

### Returns

| Type   |
| ------ |
| string |

### Description

Sends an HTTP GET request to the specified URL and returns the response as a string.

***

## HttpPost

### Definition

```luau
function game:HttpPost(url: string, data: string): string
```

### Parameters

| Name | Type   | Description                         |
| ---- | ------ | ----------------------------------- |
| url  | string | The URL to send a POST request to   |
| data | string | The data to send in the POST request|

### Returns

| Type   |
| ------ |
| string |

### Description

Sends an HTTP POST request to the specified URL with the provided data and returns the response as a string.

***

## GetService

### Definition

```luau
function game:GetService(name: string): Instance
```

### Parameters

| Name | Type   | Description             |
| ---- | ------ | ----------------------- |
| name | string | The name of the service |

### Returns

| Type     |
| -------- |
| Instance |

### Description

Returns the service with the specified name. Creates the service if it doesn't exist.

***

## GetHwid

### Definition

```luau
function game:GetHwid(): string
```

### Returns

| Type   |
| ------ |
| string |

### Description

Returns the hardware ID of the current machine.

***

## GetPing

### Definition

```luau
function game:GetPing(): number
```

### Returns

| Type   |
| ------ |
| number |

### Description

Returns the current network ping in milliseconds.

***

## PlaceId

### Definition

```luau
game.PlaceId: number
```

### Description

The unique identifier for the current place (read-only).

***

## GameId

### Definition

```luau
game.GameId: number
```

### Description

The unique identifier for the current game (read-only).

***

## JobId

### Definition

```luau
game.JobId: string
```

### Description

The unique identifier for the current server job (read-only).
