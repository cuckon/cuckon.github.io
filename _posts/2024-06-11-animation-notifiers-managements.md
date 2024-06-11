---
author: John
tags: UE ABP
---
When I right clicked in my ABP eventgraph, under "Add Anim Notify Event" there are couple of actions:

![](/assets/img/posts-202406/11-event-actions.jpg)

It troubled me that I could not trace where they are coming from: just not from anywhere in the whole project.

GPT was not much help in this case. I managed to dug into the
`Engine\Source\Runtime\Engine\Private\Animation\Skeleton.cpp`, and in
`void USkeleton::CollectAnimationNotifies(TArray<FName>& OutNotifies) const` it indicates that it's from the skeleton
animation notifies.

But I couldn't find any notifiers.

Finnally, I found that even the notifiers are not referenced anymore, they still show up in the event graph action list.
To manage them, you need to use the "Manage Notifiers" menu:

![](/assets/img/posts-202406/11-manage-notifiers.jpg)
