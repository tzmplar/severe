# Signal

## Constructor <a href="#signal" id="signal"></a>

### new <a href="#new" id="new"></a>

```
function Signal.new(): Signal
```

Creates a new `Signal` object.

## Methods <a href="#connect" id="connect"></a>

### connect <a href="#connect" id="connect"></a>

```
function Signal:connect(callback: (...any) -> ()): Connection
```

Connects the specified callback function to the signal. The callback will be invoked with any arguments passed to the `Fire` method.

### fire <a href="#fire" id="fire"></a>

```
function Signal:fire(... any): ()
```

Fires the signal, invoking all connected callbacks with the provided arguments.

### wait <a href="#wait" id="wait"></a>

```
function Signal:wait(): (... any)
```

Waits for the signal to be fired and returns the arguments passed to the `Fire` method.

### once <a href="#once" id="once"></a>

```
function Signal:once(callback: (...any) -> ()): Connection
```

Connects the specified callback function to the signal, but only for a single invocation. After the signal is fired and the callback is invoked, the connection is automatically disconnected.

## Classes <a href="#connection" id="connection"></a>

### Connection

#### disconnect <a href="#disconnect" id="disconnect"></a>

```
function Connection:disconnect(): ()
```

Disconnects the connection, preventing the associated callback from being invoked when the signal is fired.
