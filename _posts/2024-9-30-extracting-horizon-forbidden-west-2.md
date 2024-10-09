---
author: John
tags: extraction
---
Extracting, together with frame capture, is a very good way to learn from a game. By extracting, you can retrieve the models, textures, animations from the game and study their specification, reuse them for POV etc.

# Extracting Horizon Forbidden West 2 PC

First you need to download the game via Steam.
And download the extracting tool. Someone has created [a very comprehensive version](https://reshax.com/topic/828-horizon-forbidden-west-pc-complete-modelanimation-extractor/)([archive](/assets/files/posts-202409/HorizonExtractor.zip)) that not only extracts but also organize and merges.


# Parsing
## Loading the models

the `.SMD` only works with Blender 4.2 or higher so if you are using older versions you need to upgrade your blender.

Unfortunitely, the `io_import_scene_ascii.py` shipped with the `HorizonExtractor` is not compatible with 4.2 and will throw an error. To fix it, comment out the `use_auto_smooth` variable:

![](/assets/img/posts-202409/30-1.png)


Additionally, you might encounter the following error:
```
IndexError: bpy_struct: item.attr = val: sequence expected at dimension 1, not 'int'. Check the input data or file format.
after
    0.00600433349609375 secs
  3c13_2_static
```
This issue was identified as occurring only when creating materials. So the quickest fix is to uncheck "Materials" when importing.

![](assets/img/posts-202409/30-3.png)

## Loading the animations
As for the animations, it's much simpler. You just need to install the [Blender Source Tools](https://developer.valvesoftware.com/wiki/Blender_Source_Tools). And after importing, blender will drive the binded models automatically.

![](assets/img/posts-202409/30-4.png)
