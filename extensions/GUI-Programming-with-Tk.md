---
layout: page
lang: en
title: GUI Programming with Tk
---

# {{ page.title }}

Gura provides modules named `tcl` and `tk` that use [Tcl/Tk](http://www.tcl.tk/) library for GUI programming.


## Simple Example

The following example creates a window that has one Button widget.

    import(tk)
    
    tk.mainwindow() {|mw|
        mw.Button(text =&gt; 'Push me') {|w|
            w.pack()
            w.bind(`command) {
                w.tk$MessageBox(title =&gt; 'event', message =&gt; 'hello')
            }
        }
    }
    tk.mainloop()


## Sample Script

The code below is a drawing program. I have ported it from a sample in
[TkDocs](http://www.tkdocs.com/).

    import(tk)
    
    tk.mainwindow() {|mw|
        mw.Canvas(bg => 'white') {|c|
            c.pack(fill => 'both', expand => true)
            [lastx, lasty] = [0, 0]
            color = 'black'
            c.bind('<1>') {|x:number, y:number|
                [lastx, lasty] = [x, y]
            }
            c.bind('<B1-Motion>') {|x:number, y:number|
                addLine(x, y)
            }
            addLine(x:number, y:number) = {
                extern(lastx, lasty)
                c.Line(lastx, lasty, x, y, fill => color, width => 3)
                [lastx, lasty] = [x, y]
            }
            setColor(colorNew:string) = {
                color:extern = colorNew
            }
            function(color:string, y:number):map {
                c.Rectangle(10, y, 30, y + 20, fill => color) {|item|
                    item.bind('<1>') { setColor(color) }
                }
            }(['red', 'blue', 'black'], 10 + (0..) * 25)
        }
    }
    tk.mainloop()

Sample result.

![tk-demo](../images/tk-demo.png)


## More Sample Scripts

You can find sample scripts using Tk on
[GitHub repository](https://github.com/gura-lang/gura/tree/master/sample/tk/).
