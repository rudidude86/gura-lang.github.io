---
layout: page
lang: en
title: Graphic Image Handling
---

{{ page.title }}
----------------

### Image Instance

An instance of `image` class contains image data and provides functions
such as reading/writing image files, resizing and rotating.

An image instance can be created by a constructor function `image`.
Calling `image` function with an argument that specifies a stream
containing an image data would read that data.
The code below reads a JPEG file and write it in PNG format.

    import(jpeg)
    import(png)
    image('foo.jpg').write('foo.png')

Before `image` function, you have to import a module that can handle an image type.
The following table shows image types and associated module names.

<table>
<tr><th>Image Type</th><th>Module</th><th>Added Methods to <code>image</code></th></tr>
<tr><td>BMP</td><td><code>bmp</code></td><td><code>bmpread</code>, <code>bmpwrite</code></td></tr>
<tr><td>JPEG</td><td><code>jpeg</code></td><td><code>jpegread</code>, <code>jpegwrite</code></td></tr>
<tr><td>GIF</td><td><code>gif</code></td><td><code>gifread</code>, <code>gifwrite</code></td></tr>
<tr><td>PNG</td><td><code>png</code></td><td><code>pngread</code>, <code>pngwrite</code></td></tr>
<tr><td>Microsoft Icon</td><td><code>msico</code></td><td><code>msicoread</code>, <code>msicowrite</code></td></tr>
<tr><td>PPM</td><td><code>ppm</code></td><td><code>ppmread</code>, <code>ppmwrite</code></td></tr>
<tr><td>XPM</td><td><code>xpm</code></td><td><code>xpmdata</code>, <code>xpmwrite</code></td></tr>
<tr><td>TIFF</td><td><code>tiff</code></td><td><code>tiffread</code></td></tr>
</table>

Importing those modules also add methods to `image` class
like `jpeg` module adding `image#jpegread` and `image#jpegwrite`.
