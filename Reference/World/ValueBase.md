# ValueBase

Value objects are instances that store a single value of a specific type.

## Applies To

- BoolValue
- IntValue
- NumberValue
- Vector3Value
- ObjectValue
- StringValue
- CFrameValue

## Value

### Definition

Depends on the ValueBase type:
```luau
BoolValue.Value: boolean
IntValue.Value: number
NumberValue.Value: number
Vector3Value.Value: Vector3
ObjectValue.Value: Instance?
StringValue.Value: string
CFrameValue.Value: CFrame
```

### Description

The value stored by this value object. Can be read and written.
