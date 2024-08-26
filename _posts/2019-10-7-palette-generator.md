---
author: John
tags: python archive
---

This is a brief explanation about why I wrote *Sucialism Color Palette Generator *.

![ui](/assets/img/posts-2019/201910-pallette-generator-1.png)

Yet another palette generator .

Its is not a novel stuff when we talking about generating palette from a given picture. But as the progress going on and on of that I study colours, I found none of those existing generators meet my primary request: **to extract the colours that really “matters”, not simply the colours that dominate**.

Take the following paiting as an example:

![ui](/assets/img/posts-2019/201910-pallette-generator-2.webp)
![ui](/assets/img/posts-2019/201910-pallette-generator-2.jpeg)

Left is what the most mainline generators do. As you can see it does a pretty good job to represent the overall color distribution, “Dark Slate Gray”, “Dim Gray”, “Silver” obviously are the perfect colours we need if we are selecting limited colours to make a GIF.

But if you are a painter, things are **different**, in which situation the really important colours to build that elegent look, is the cool and warm part, or in other word the **“extreme”** part of the colours, no matter how little part they played.

Back to the example painting, it’s the “Dark Blue” and “Red” asides the “White”, “Black”, “Orange” etc build the look of touchable depth and rich tones. You can image **how dull the picture will be if without “Red”**, even thought it’s rare.

That’s the whole point of my palette generator.

![ui](/assets/img/posts-2019/201910-pallette-generator-3.png)
![ui](/assets/img/posts-2019/201910-pallette-generator-4.webp)
![ui](/assets/img/posts-2019/201910-pallette-generator-5.webp)

Notice the relationship between the colours Vladimir chosed and the one on the canvas.

Compared with the above palette from reality, you can tell the similarity. All the rich colours are mixed out of these “extreme” colours.

So if you are a artist and want to get the initial colours instead of the mixed result, Sucialism Color Palette Generator is what you need.