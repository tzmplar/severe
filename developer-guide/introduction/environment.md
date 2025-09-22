# Environment

## Overview

Unlike **internals, or executors** our external does not have the capability to intercept and/or hook into game scripts. This means that most hooking functions (e.g: `hookfunction`, `hookmetamethod` ) are extremely limited, if not impossible at all.

Whilst we have less capabilities than ordinary/old-school software like **Synapse X**, our model is largely benefiting for the memory namespace, as it allows for low-level interaction with the client, allowing you, for example inject bytecode into game-scripts, achieving traditional but still limited script execution, however it also allows you to tamper around with some instances whilst being almost impossible to detect from the game-scripts context. This means that you almost don't have to worry about game's anti cheat as long as you're sticking purely to reading the memory.

## Design

We're working on mimicking **Synapse V3** state-of-the-art environment, whilst also taking inspiration from Luau's native libraries, noticeably, for memory we used `buffer` library from Luau as an inspiration. We plan to keep our API minimal and simplistic, whilst being ultra focused on performance and developer experience, you may notice this with the object-oriented [engine](../../reference/engine/ "mention").

## Difference

You may ask, "how does this differ from \[insert external name]", let's dive into that topic.

1. Primary focus is performance and simplicity, hence why inherited the traditional way which can be seen in libraries such as [crypt.md](../../reference/namespaces/crypt.md "mention"), and [drawing.md](../../reference/namespaces/drawing.md "mention"), just like **Serotonin** we also sport some **Roblox's** classes and libraries, such as `Color3`, `Vector3`, `Vector2`, and in the future we plan to strongly inherit from **Roblox** on subjects such as `Enum`, `UserInputService` , `Instance.new` (specifically for the user-interfaces that relied on it, we may have an interface that will automatically translate it into [drawing.md](../../reference/namespaces/drawing.md "mention")).
2. We inherit and base our API from **Synapse X**, we look into making it as familiar as possible especially to the developers that have moved in from internals and executors similar to the one mentioned.
3. We expand on our **low-level interaction** with the client, whilst keeping our focus to be as object-oriented as **Serotonin**, our [engine](../../reference/engine/ "mention") closely mimics the native **Roblox OOP**, whilst having performance as native-as-possible.
