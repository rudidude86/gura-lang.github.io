---
layout: default
lang: en
title: Top
---

Latest News
-----------

<table>
<tr><td>2014-02-25</td><td><a href="Download.html">Gura v0.4.2</a> was released.</td></tr>
<tr><td>2014-02-14</td><td>Gura v0.4.1 was released.</td></tr>
<tr><td>2014-02-06</td><td>Gura v0.4.0 was released.</td></tr>
</table>

What's This?
------------

**Gura** is an **iterator-oriented** programming language
that focuses on iterators with improved functions for calculation and data processing.
It gives you a new possibility to write more elegant codes than ever,
but with a familiar appearance.

Take a look at a simple example.
The following code prints content of a text file with line numbers.

    printf('%d %s', 1.., readlines('foo.txt'))

Apparently, there seems to be no special trick with this program.
But a new feature called [Implicit Mapping](features/ImplicitMapping.html) is working internally,
which automatically repeats evaluation of `printf` function
after it's given with iterators, `1..` and `readlines('foo.txt')`, as its arguments.

Language Features
-----------------

- [Flow Control](features/Flow-Control.html)
- [Function Definition](features/Function-Definition.html)
- [Object Oriented Programming](features/Object-Oriented-Programming.html)
- [Implicit Mapping](features/Implicit-Mapping.html)
- [Member Mapping](features/Member-Mapping.html)

Extensions
----------

- [Graphic Image Handling](extensions/Graphic-Image-Handling.html)
- [GUI Programming with wxWidgets](extensions/GUI-Programming-with-wxWidgets.html)
- [GUI Programming with Tk](extensions/GUI-Programming-with-Tk.html)
- [GUI Programming with SDL](extensions/GUI-Programming-with-SDL.html)
- [Programming with OpenGL](extensions/Programming-with-OpenGL.html)
- [Programming with Cairo](extensions/Programming-with-Cairo.html)
- [HTTP Access](extensions/Http-Access.html)
- [HTTP Server](extensions/Http-Server.html)
- [Database Access](extensions/Database-Access.html)
- [Create Your Own Binary Module](extensions/Create-Your-Own-Binary-Module.html)

Articles
--------

- [Comparison between Java 8 and Gura](articles/Comparison-between-Java8-and-Gura.html)
- [Script to Generate Prime Numbers](articles/Script-to-Generate-Prime-Numbers.html)

Documentation
-------------

- ![pdf-icon](images/pdf.png) Gura Language Manual ([Japanese](https://github.com/gura-lang/gura-doc/blob/master/gura-lang-j.pdf?raw=true))
- ![pdf-icon](images/pdf.png) Gura Library Reference ([Japanese](https://github.com/gura-lang/gura-doc/blob/master/gura-lib-j.pdf?raw=true))
- ![pdf-icon](images/pdf.png) Gura Developer's Manual ([Japanese](https://github.com/gura-lang/gura-doc/blob/master/gura-dev-j.pdf?raw=true))

Any opinions and suggestions are welcome via [E-mail](mailto:ypsitau@nifty.com).
