# vector

This library implements functionality for the vector type in addition to the built-in primitive operator support. Default configuration uses vectors with 3 components (`x`, `y`, and `z`). If the _4-wide mode_ is enabled by setting the `LUA_VECTOR_SIZE` VM configuration to 4, vectors get an additional `w` component.

Individual vector components can be accessed using the fields `x` or `X`, `y` or `Y`, `z` or `Z`, and `w` or `W` in 4-wide mode. Since vector values are immutable, writes to individual components are not supported.

## zero/one

```lua
vector.zero
vector.one
```

Constant vectors with all components set to 0 and 1 respectively. Includes the fourth component in _4-wide mode_.

## create

```lua
vector.create(x: number, y: number, z: number): vector
vector.create(x: number, y: number, z: number, w: number): vector
```

Creates a new vector with the given component values. The first constructor sets the fourth (`w`) component to 0.0 in _4-wide mode_.

## magnitude

```lua
vector.magnitude(vec: vector): number
```

Calculates the magnitude of a given vector. Includes the fourth component in _4-wide mode_.

## normalize

```lua
vector.normalize(vec: vector): vector
```

Computes the normalized version (unit vector) of a given vector. Includes the fourth component in _4-wide mode_.

## cross

```lua
vector.cross(vec1: vector, vec2: vector): vector
```

Computes the cross product of two vectors. Ignores the fourth component in _4-wide mode_ and returns the 3-dimensional cross product.

## dot

```lua
vector.dot(vec1: vector, vec2: vector): number
```

Computes the dot product of two vectors. Includes the fourth component in _4-wide mode_.

## angle

```lua
vector.angle(vec1: vector, vec2: vector, axis: vector?): number
```

Computes the angle between two vectors in radians. The axis, if specified, is used to determine the sign of the angle. Ignores the fourth component in _4-wide mode_ and returns the 3-dimensional angle.

## floor

```lua
vector.floor(vec: vector): vector
```

Applies `math.floor` to every component of the input vector. Includes the fourth component in _4-wide mode_.

## ceil

```lua
vector.ceil(vec: vector): vector
```

Applies `math.ceil` to every component of the input vector. Includes the fourth component in _4-wide mode_.

## abs

```lua
vector.abs(vec: vector): vector
```

Applies `math.abs` to every component of the input vector. Includes the fourth component in _4-wide mode_.

## sign

```lua
vector.sign(vec: vector): vector
```

Applies `math.sign` to every component of the input vector. Includes the fourth component in _4-wide mode_.

## clamp

```lua
vector.clamp(vec: vector, min: vector, max: vector): vector
```

Applies `math.clamp` to every component of the input vector. Includes the fourth component in _4-wide mode_.

## max

```lua
vector.max(...: vector): vector
```

Applies `math.max` to the corresponding components of the input vectors. Includes the fourth component in _4-wide mode_. Equivalent to `vector.create(math.max((...).x), math.max((...).y), math.max((...).z), math.max((...).w))`.

## min

```lua
vector.min(...: vector): vector
```

Applies `math.min` to the corresponding components of the input vectors. Includes the fourth component in _4-wide mode_. Equivalent to `vector.create(math.min((...).x), math.min((...).y), math.min((...).z), math.min((...).w))`.
