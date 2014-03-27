---
layout: page
lang: en
title: Create Animation GIF
---

# {{ page.title }}

In this article, we're creating an animation GIF file
from a scanned image of a handwritten picture.

Here is a JPEG image file that contains animation frames:
[cat-picture.jpg](../images/cat-picture.jpg).

![cat-picture](../images/cat-picture.jpg)

The program needs to do the following jobs.

* Read a JPEG file as a source image.
* Reduce number of colors in the image down to 256 so that it suits with GIF specification.
* Create a GIF content.
* Split the source image by frames and add them to the GIF content.
* Write the GIF content to a file.

And here is the code:

    import(jpeg)
    import(gif)
    
    img = image('cat-picture.jpg').reducecolor(`win256)
    delayTime = 12
    [nx, ny] = [6, 2]
    [w, h] = [img.width / nx, img.height / ny]
    n = nx * ny
    x = range(nx).cycle(n) * w
    y = int(range(n) / nx) * h
    gif.content().addimage(img.crop(x, y, w, h), delayTime).write('cat-anim.gif')

![cat-picture](../images/cat-anim.gif) [cat-anim.gif](../images/cat-anim.gif)
