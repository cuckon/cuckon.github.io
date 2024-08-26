---
author: John
tags: osl rendering
---
There’s an amazing article by Hang Li that talks about [how to make the “swirl micro scratch”](https://mp.weixin.qq.com/s?__biz=MzU3NDg1MDY1OQ==&mid=2247483670&idx=1&sn=dce27d4fcdf7e723d0e4ba74ec71c732&scene=21#wechat_redirect) look(in Chinese). Simply put, the theory is to match the scratch stroke direction with anisotropic direction. The approach used in the article is by file texture. Here I implemented a procedural shader that generate proper texture for you.

Source code and example scenes: [https://github.com/cuckon/scratched](https://github.com/cuckon/scratched)

And here’s how the result looks:

![Metal](/assets/img/posts-202408/26-1-result.png)
![Dielectric](/assets/img/posts-202408/26-20-dielectric.png)

Besides the physical swirl scratch specular, you can achieve some interesting look by tweaking the “offset” parameter:

![Metal](/assets/img/posts-202408/26-31.webp)
![Metal](/assets/img/posts-202408/26-32.webp)

And it’s very easy to be used in Clarissa or Arnold or any other DCC that support OSL:

![Metal](/assets/img/posts-202408/26-clarisse.png)

For detail and source code and example scene, take a look at the github link I gave above.