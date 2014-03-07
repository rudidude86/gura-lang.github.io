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

For Linux, an executable binary `gura` is the interpreter program.


### Interrupt Mode

When you run `gura.exe` or `gura` with no script file specified in the argument,
it will enter an interrupt mode that waits for user inputs.

    Gura x.x.x [xxxxxxxxxx, xxx xx xxxx] Copyright (C) 2011-2014 ypsitau
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

    $ gura hello.gura

Gura script file should have a suffix `.gura` or `.guraw`,
where `.gura` is for command-line scripts and `.guraw` for ones with GUI.
In Windows environment, the suffix `.gura` is associated with the program `gura.exe`
and `.guraw` with `guraw.exe`.

As a Gura script is a plain text file, you can use any of your favorite editor to create it.
The code below shows the content of `hello.gura` script.

    println('Hello World')

If you want to make a script executable on UNIX-like OS such as Linux,
it might be a good idea to add shebang at the top of the script file.
Below is a Hello World script with a shebang.

    #!/usr/bin/env gura
    println('Hello World')

If you want to use shebang, be careful to save the script file
with each line ended with LF code.
This is to avoid an error caused by specifications of shell programs, not of Gura.

If a sciript file contains non-ASCII characters like Japanese and Chinese,
you should save in in UTF-8 character code, which is a default code set for Gura interpreter.
When you need to save the file in other character codes, there are two ways to handle it.

One is to specify `-d` option in command line as following.

    $ gura -d shift_jis foo.gura

Another one is to describe a magic comment that specifies a character encoding
at top of the script but after shebang if exists.

    #!/usr/bin/env gura
    # coding: shift_jis
    println('... string that may contain characters in Shift-JIS ...')

A magic comment has a format like `coding: XXXXXX`
where `XXXXXX` indicates what encoding the parser is to use.
It can be detected when it appears at the first or second line of a script
and is described as a single-line comment.

The following format is acceptable too.
This is good to make Emacs determine what character encoding it should choose.

    #!/usr/bin/env gura
    # -*- coding: shift_jis -*-

### Composite Script File


