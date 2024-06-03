---
author: John
tags: UE C++
---
I encountered a problem when I was trying to bind a delegate to a function.

Here is the delegate:
```cpp
DECLARE_DYNAMIC_MULTICAST_DELEGATE_OneParam(FHenCaughtDelegate, const AHen*, Self);
```
UE complains that "EventOnThrowGrapple_Event Signature Error: The function/event ‘EventOnCaught_Event’ does not match the necessary signature - has the delegate or function/event changed?".

At first I suspected that it's because the function signature is wrong. But no.

I tried to replace `const AHen*` to a simple `int` but got the same error.

After some googling, I was luckly found [this link](https://forums.unrealengine.com/t/wtf-event-signature-error-the-function-event-xxx-does-not-match-the-necessary-signature-has-the-delegate-or-function-event-changed/502045)!

It says that you should never name the parameter `self`. I haven't investigated it further but here's the modified code:

```cpp
DECLARE_DYNAMIC_MULTICAST_DELEGATE_OneParam(FHenCaughtDelegate, const AHen*, Me);
```
