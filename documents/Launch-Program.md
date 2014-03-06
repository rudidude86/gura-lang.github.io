---
layout: page
lang: en
title: Launch Program
---

Launch Program
--------------

### Program Files

For Windows, there are two types of program files to launch Gura interpreter:
`gura.exe` and `guraw.exe`. `guraw.exe` doesn't show command prompt window
and you can use it to run a script with graphical user interface.

For Linux, an executable binary `gura` is the program.


### Interrupt Mode

When you run `gura.exe` or `gura` with no script file specified in the argument,
it will enter an interrupt mode that waits for user inputs.

    Gura 0.4.2 [MSC v.1600, Feb 25 2014] Copyright (C) 2011-2014 ypsitau
    >>> 

When you input Gura's script followed by an enter key after a prompt `>>>`,
it will evaluate the script and show its result.

    >>> 3 + 4
    7
    >>> println('Hello world')
    Hello world

To quit the interpreter, enter `Ctrl+C` from keyboard or execute a script `sys.exit()`.


### Run Script File

You can run Gura script file by specifying it as an argument for Gura interpreter program.

Gura script file should have suffixes `.gura` or `.guraw`,
`.gura` for console programs and `.guraw` for ones with graphical user interface.
In Windows environment, the suffix `.gura` is associated with the program `gura.exe`
and `.guraw` with `guraw.exe`.
