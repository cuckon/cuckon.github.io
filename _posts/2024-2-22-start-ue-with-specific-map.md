---
author: John
tag: UE
---

When developing a level, it's not unsual that your UE is not stable and keeps crashing. So you need to re-enter that level again and again.

To make it a bit easier of course you can specify the start up level in the project setting. But it will affect all people - unless you don't commit the config.

There's another way though: Via **shortcut**.

Create a short cut of your UE, edit the target to:

```
"D:\UE-Path\UnrealEditor.exe" D:\Project-Path\PreDemo_UE5.uproject /Game/Levels/CharacterTest
```

There you go, click the shortcut to go into it straightly!