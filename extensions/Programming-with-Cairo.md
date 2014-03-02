---
layout: page
lang: en
title: Programming with Cairo
---

Programming with Cairo
----------------------

### Simple Example

Here is a simple example using Cairo.

    import(cairo)
    import(show)
    
    img = image(`rgba, 300, 300)
    img.cairo {|cr|
        cr.scale(img.width, img.height)
        cairo.pattern.create_linear(0, 0, 1, 1) {|pat|
            pat.add_color_stop_rgb(0, 0, 0, 0)
            pat.add_color_stop_rgb(1, 1.0, 1.0, 1.0)
            cr.set_source(pat)
        }
        cr.rectangle(0.1, 0.1, 0.8, 0.8)
        cr.fill()
    }
    img.show()

### Render in Exisiting Image

The following is an example that performs reading a JPEG file,
drawing something on it with Cairo APIs and writing it out as a JPEG file.

    import(jpeg)
    import(cairo)
    I(filename:string) = path.join(sys.datadir, 'sample/resource', filename)
    img = image(I('Winter.jpg'))
    img.cairo {|cr|
        repeat (10) {|i|
            [x, y, r] = [128 + 30 * i, 128 + 30 * i, 60 - i * 4]
            pat = cairo.pattern_create_radial(
                x - r / 10, y - r / 6, r / 5, x - r / 6, y - r / 6, r * 1.2)
            pat.add_color_stop_rgba(0, 1, 1, 1, 1)
            pat.add_color_stop_rgba(1, 0, 0, 0, 1)
            cr.set_source(pat)
            cr.arc(x, y, r)
            cr.fill()
        }
    }
    img.write('result.jpg')

### Output Animation GIF File Combining Multiple Image Files

The following example will output an animation GIF file that combines
several images from PNG files together.

    import(gif)
    import(png)
    gif.content().addimage(['cell1.png', 'cell2.png', 'cell3.png'], 10).write('anim1.gif')

You can also create a GIF file that has a dynamically produced image.
The example below shows how to output an animation GIF file that contains
images created by Cairo APIs.

    import(cairo)
    import(gif)
    str = 'Hello'
    img = image(`rgba, 64, 64, `white)
    gifobj = gif.content()
    img.cairo {|cr|
        cr.select_font_face('Georgia', cairo.FONT_SLANT_NORMAL, cairo.FONT_WEIGHT_BOLD)
        cr.set_font_size(64)
        te = cr.text_extents(str)
        cr.set_source_rgb(0.0, 0.0, 0.0)
        for (x in interval(64, -te.width, 30)) {|i|
            img.fill(`white)
            cr.move_to(x, 50)
            cr.show_text(str)
            gifobj.addimage(img.clone(), 10)
        }
    }
    gifobj.write('anim2.gif')

### More Sample Scripts

You can find sample scripts using Cairo on
[GitHub repository](https://github.com/gura-lang/gura/tree/master/sample/cairo/).
