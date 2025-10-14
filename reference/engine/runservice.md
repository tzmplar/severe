# RunService

## Events

You can connect to these events via `:Connect` method, which takes in a callback.

### Render

The speed of this event matches the render frequency of the overlay. It is not recommended to call memory functions here.

This event is primarily used for [drawingimmediate.md](../namespaces/drawing/drawingimmediate.md "mention").

### Local

This refers to a group of events which are synchronized to match the update frequency of "Local" within the overlay.

#### PreLocal

#### PostLocal

### Model

This refers to a group of events which are synchronized to match "Model" updates within the overlay. This is perfect for `GetChildren` calls.

#### PreModel

#### PostModel

### Data

Group of events which are synchronized for the "Data" updates within the overlay, perfect for storing physics data.

#### PreData

#### PostData
