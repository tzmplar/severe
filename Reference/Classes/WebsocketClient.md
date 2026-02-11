# WebsocketClient

A websocket client for establishing and managing WebSocket connections.

## Constructors

### WebsocketClient.new

### Definition

```luau
function WebsocketClient.new(url: string): WebsocketClient
```

### Parameters

| Name | Type   | Description                              |
| ---- | ------ | ---------------------------------------- |
| url  | string | The WebSocket connection URL             |

### Returns

| Type            |
| --------------- |
| WebsocketClient |

### Description

Creates a new WebsocketClient and connects to the specified URL.

### Code Samples

```luau
-- Create a WebSocket connection
local ws = WebsocketClient.new("ws://example.com:8080")

-- Handle incoming messages
ws.DataReceived:Connect(function(payload, isBinary)
    if isBinary then
        print("Received binary data:", #payload, "bytes")
    else
        print("Received text:", payload)
    end
end)

-- Send a message
ws:Send("Hello, server!")

-- Disconnect when done
ws:Disconnect()
```

***

## Properties

### Url

```luau
WebsocketClient.Url: string [readonly]
```

The WebSocket connection URL that this client is connected to. This property is read-only.

***

## Methods

### Disconnect

### Definition

```luau
function WebsocketClient:Disconnect(): ()
```

### Description

Disconnects the WebSocket. Yields until the client is fully disconnected. After calling this method, the WebSocket connection is closed and no further messages can be sent or received.

### Code Samples

```luau
local ws = WebsocketClient.new("ws://example.com:8080")

-- Do some work...
ws:Send("Goodbye")

-- Disconnect (yields until fully disconnected)
ws:Disconnect()
print("WebSocket disconnected")
```

***

### Send

### Definition

```luau
function WebsocketClient:Send(message: string, isBinary: boolean?): ()
```

### Parameters

| Name     | Type     | Description                                               |
| -------- | -------- | --------------------------------------------------------- |
| message  | string   | The message payload to send                               |
| isBinary | boolean? | Whether to send as binary data (defaults to false)        |

### Description

Sends a message through the WebSocket connection. The message can be sent as either text or binary data based on the `isBinary` parameter.

### Code Samples

```luau
local ws = WebsocketClient.new("ws://example.com:8080")

-- Send text message (default)
ws:Send("Hello, world!")

-- Explicitly send text
ws:Send("Text message", false)

-- Send binary data
local binaryData = "\x01\x02\x03\x04"
ws:Send(binaryData, true)
```

***

## Events

### DataReceived

### Definition

```luau
WebsocketClient.DataReceived: Signal<(payload: string, isBinary: boolean) -> ()>
```

### Parameters

| Name     | Type    | Description                                    |
| -------- | ------- | ---------------------------------------------- |
| payload  | string  | The received message data                      |
| isBinary | boolean | Whether the received data is binary            |

### Description

Fires when data is received from the WebSocket connection. The event provides the payload as a string and a boolean indicating whether it's binary data.

### Code Samples

```luau
local ws = WebsocketClient.new("ws://example.com:8080")

-- Connect to the DataReceived event
ws.DataReceived:Connect(function(payload, isBinary)
    if isBinary then
        print("Received binary payload of length:", #payload)
        -- Process binary data...
    else
        print("Received text message:", payload)
        -- Process text data...
    end
end)

-- Example with JSON parsing
ws.DataReceived:Connect(function(payload, isBinary)
    if not isBinary then
        local success, data = pcall(function()
            return game:GetService("HttpService"):JSONDecode(payload)
        end)
        
        if success then
            print("Received JSON data:", data)
        else
            print("Received non-JSON text:", payload)
        end
    end
end)
```
