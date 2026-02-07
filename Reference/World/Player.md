# Player

Represents a player in the game.

## DisplayName

### Definition

```luau
Player.DisplayName: string
```

### Description

The display name of the player (read-only).

***

## UserId

### Definition

```luau
Player.UserId: number
```

### Description

The unique user ID of the player (read-only).

***

## Character

### Definition

```luau
Player.Character: Model?
```

### Description

The player's character model in the game, or `nil` if the player doesn't have a character (read-only).

***

## Team

### Definition

```luau
Player.Team: Team?
```

### Description

The team the player is currently on, or `nil` if not on a team (read-only).
