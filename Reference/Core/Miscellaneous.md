# Functions
## gethwid
### Definition
```lua
function gethwid(): string
```
### Returns
```horizontal
string
```
### Description
Returns the user's HWID, this is primarily useful for fingerprinting and authentication.
## isrbxactive
### Definition
```lua
function isrbxactive(): (boolean)
```
### Returns
```horizontal
### boolean
```
### Description
Will return `true` if the currently focused window is **Roblox**, otherwise returns `false`.

---

## send_notification
### Definition
```lua
function send_notification(content: string): ()
```
### Parameters

|  Name   |  Type  |                       Description                       |
| :-----: | :----: | :-----------------------------------------------------: |
| content | string | Message, that you want to be visualized on the overlay. |
### Description
This will visualize `content` on the screen thru an notification on the overlay.
### Code Samples
```lua
send_notification 'Hello, world!'
```

---

## setclipboard
### Definition
```lua
function setclipboard(content: string): ()
```
### Parameters

| Name    | Type   | Description                                        |
| ------- | ------ | -------------------------------------------------- |
| content | string | Whatever you want to be copied into the clipboard. |
### Description
This will essentially copy the string to your system's clipboard.
### Code Samples
```lua
setclipboard 'Clipboard!'
```

---

## block_roblox_window
### Definition
```lua
function block_roblox_window(state: boolean): ()
```
### Parameters

| Name  | Type    | Description                                                  |
| ----- | ------- | ------------------------------------------------------------ |
| state | boolean | Whether or not you're trying to block or unblock the window. |
### Description
Will effectively disable input pass-through on the overlay, forcing you to interact with **it** rather than the game. This is useful when creating custom a user-interface.

---

## pointer_to_userdata
### Definition
```lua
function pointer_to_userdata(address: number): userdata
```
### Parameters

| Name    | Type   | Description                                        |
| ------- | ------ | -------------------------------------------------- |
| address | number | The address that you want to turn into a userdata. |
### Description
This is a useful function that you'll find yourself utilizing when interacting with the memory functions. This will effectively turn valid addresses back into **world objects**, allowing you to index/namecall them.
### Code Samples
```lua
-- Find the DataModel by reading Workspace's parent offset, and then recasting it back to userdata.
local Parent = memory.readu64(workspace, 0x50)
local DataModel = pointer_to_userdata(Parent)

print(DataModel == game) -- Ideally, would be true, however due to version changes, 0x50 might be an invalid offset.
```

---
## get_overlay_fps
### Definition
```lua
function get_overlay_fps(): number
```
### Returns
```horizontal
## number
```
### Description
Returns the number amount of **FPS** (frames per second) that the overlay is currently running at.

---

## is_forcefield_check_active
### Definition
```lua
function is_forcefield_check_active(): boolean
```
### Returns
```horizontal
## boolean
```
### Description
Returns a boolean (true/false) based if the player has **Forcefield Check** on in their settings.

---

## is_local_health_check_active
### Definition
```lua
function is_local_health_check_active(): boolean
```
### Returns
```horizontal
## boolean
```
### Description
Returns a boolean (true/false) based if the player has **Health Check** on in their settings.

---

## is_team_check_active
### Definition
```lua
function is_team_check_active(): boolean
```
### Returns
```horizontal
## boolean
```
### Description
Returns a boolean (true/false) based if the player has **Team Check** on in their settings.

---

## add_model_data
### Definition
```lua
function add_model_data(data: table, key: string): boolean
```
### Parameters

| Name | Type   | Description |
|-----|--------|-------------|
| data | table  | Character data structure with fields like `Username` (string), `Displayname` (string), `Userid` (number), `Character` (Instance), `PrimaryPart` (Instance), `Head` (Instance), `LeftLeg` (Instance), `LeftArm` (Instance), `RightLeg` (Instance), `RightArm` (Instance), `Torso` (Instance), `ToolName` (string), `TeamName` (string), `BodyHeightScale` (number), `RigType` (number), `Whitelisted` (boolean), `Archenemies` (boolean), `Aimbot_Part` (Instance), `Aimbot_TP_Part` (Instance), `Triggerbot_Part` (Instance), `Health` (number), `MaxHealth` (number), `body_parts_data` (table), `full_body_data` (table). |
| key  | string | Unique identifier for storing the model data. |

### Returns
```horizontal
### boolean
```
### Description
Declares a new character model data under the given key for use in targeting and ESP. Processed in a dedicated model thread, and will return `true` on success.
### Code Samples
```lua
local data = {
    Username = "Player1",
    Displayname = "CoolPlayer",
    Userid = 123456,
    Character = workspace.Player1.Character,
    PrimaryPart = workspace.Player1.Character.HumanoidRootPart,
    -- ... other fields
}
add_model_data(data, "player1_key")
```

---

## edit_model_data
### Definition
```lua
function edit_model_data(data: table, key: string): boolean
```
### Parameters

| Name | Type   | Description |
|-----|--------|-------------|
| data | table  | Partial updates with fields like `RigType` (number), `Whitelisted` (boolean), `Archenemies` (boolean), `Aimbot_Part` (Instance), `Aimbot_TP_Part` (Instance), `Triggerbot_Part` (Instance), `Health` (number), `MaxHealth` (number), `BodyHeightScale` (number). |
| key  | string | Key of existing model data to update. |

### Returns
```horizontal
### boolean
```
### Description
Updates specific fields in existing model data stored under the key. Efficient for runtime changes like health or target parts. Returns `true` on success.
### Code Samples
```lua
local edit = {
    Health = 50,
    Aimbot_Part = workspace.Player1.Character.Head
}
edit_model_data(edit, "player1_key")
```

---

## remove_model_data
### Definition
```lua
function remove_model_data(key: string): boolean
```
### Parameters

| Name | Type   | Description |
|-----|--------|-------------|
| key  | string | Key of the model data to remove. |

### Returns
```horizontal
### boolean
```
### Description
Deletes specific model data by key. Returns `true` on success.

---

## clear_model_data
### Definition
```lua
function clear_model_data(): boolean
```
### Returns
```horizontal
### boolean
```
### Description
Removes all stored model data. Returns `true` on success.

---

## override_local_data
### Definition
```lua
function override_local_data(data: table): boolean
```
### Parameters

| Name | Type   | Description |
|-----|--------|-------------|
| data | table  | Local player data with fields like `LocalPlayer` (userdata), `Displayname` (string), `Username` (string), `Userid` (number), `Character` (userdata), `Team` (userdata), `RootPart` (userdata), `LeftFoot` (userdata), `Head` (userdata), `LowerTorso` (userdata), `Tool` (userdata), `Humanoid` (userdata), `Health` (number), `MaxHealth` (number), `RigType` (number). |

### Returns
```horizontal
### boolean
```
### Description
Sets or overrides local player data for UI rendering and local thread processing. Returns `true` on success.

### Code Samples
```lua
local data = {
    LocalPlayer = game.Players.LocalPlayer,
    Character = game.Players.LocalPlayer.Character,
    -- ... other fields
}
override_local_data(data)
```

---

## clear_local_data
### Definition
```lua
function clear_local_data(): boolean
```
### Returns
```horizontal
### boolean
```
### Description
Clears all local player data. Returns `true` on success.
## ismenuopened
### Definition
```lua
function ismenuopened(): boolean
```
### Returns
```horizontal
### boolean
```
### Description
Whether the menu is opened returns `true`, otherwise `false`.
