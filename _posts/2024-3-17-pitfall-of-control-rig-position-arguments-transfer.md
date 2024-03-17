---
author: John
tags: UE controlrig
---

When you want to position a controller of a control rig with Blueprint/AnimBlueprint, it's not unsual that you do so with the following workflow:

- Expose the controller to AnimBP as a pin.
- Pass the position as a vector to the pin.
- Utilize it within your ControlRig and pass it through a `From World` node.
- Pipe the value to your own logic.

However, this afternoon when I was working on my own project, the `From World` seemed malfunctioning - no matter how I tried to match the space, it appeared to behave in a different space, with rotation.

It took hours to pinpoint the reason, during which I even began to suspect it might be a UE's bug.

Luckily, I managed to figure out that **everything worked correctly when I used a pure exposed variable** instead of a controller. Having found this, I quickly find the root cause: there is rotation applied on the controller's `Transfor Offset`.

![](/assets/img/posts-202403/03-controlrig-offset.png)

 So even the value of the parameter is in **Global space + World space**, it's still be under a local transformation when dealing with the incoming position.
