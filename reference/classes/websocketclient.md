# WebsocketClient

### Functions <a href="#functions" id="functions"></a>

#### new <a href="#new" id="new"></a>

```lua
function WebsocketClient.new(url: string) -> WebsocketClient
```

### Methods <a href="#methods" id="methods"></a>

#### Disconnect <a href="#disconnect" id="disconnect"></a>

```lua
function WebsocketClient:Disconnect() -> ()
```

#### Send <a href="#send" id="send"></a>

```lua
function WebsocketClient:Send(message: string, is_binary: boolean?) -> ()
```

### Events <a href="#events" id="events"></a>

#### DataReceived <a href="#onmessage" id="onmessage"></a>

```lua
WebsocketClient.DataReceived(payload: string, is_binary: boolean?)
```
