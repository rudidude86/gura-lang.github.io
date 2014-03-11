---
layout: page
lang: en
title: Launch Program
---

{{ page.title }}
----------------

### Program Files

For Windows, there are two types of program files to launch Gura interpreter:
`gura.exe` and `guraw.exe`. `guraw.exe` doesn't show command prompt window
and you can use it to run a script with graphical user interface.

For Linux, an executable binary `gura` is the interpreter program.


### Interactive Mode

When you run `gura.exe` or `gura` with no script file specified in the argument,
it will enter an interactive mode that waits for user inputs.

    Gura x.x.x [xxxxxxxxxx, xxx xx xxxx] Copyright (C) 2011-2014 ypsitau
    >>> 

When you input a script followed by an enter key after a prompt `>>>`,
it will evaluate the script and show its result.

    >>> 3 + 4
    7
    >>> println('Hello world')
    Hello world

To quit the interpreter, enter `Ctrl+C` from keyboard or execute a script `sys.exit()`.


### Run Script File

You can run a script file by specifying it as an argument for Gura interpreter program.

    $ gura hello.gura

A Gura script file should have a suffix `.gura` or `.guraw`,
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

If a script file contains non-ASCII characters like Japanese and Chinese,
you should save in in UTF-8 character code, which is a default code set for the interpreter.

When you need to save the file in other character codes, there are two ways to parse it properly.
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
This is good to make Emacs determine what character encoding it should choose in editing.

    #!/usr/bin/env gura
    # -*- coding: shift_jis -*-

Available encoding names are described in Chapter.X.


### Composite File

It often happens that an application consists of multiple script files and
other resources such as image files.
Consider that a certain application has following files:

    foo.gura
    utils.gura
    message.txt
    image.png

`foo.gura` is a main script that imports `utils.gura`
and reads files `message.txt` and `image.png`.

It could be bothersome to treat these files separately
especially when you try to distribute them.

For such a case, Gura has a feature that can run a ZIP archive file
containing scripts and any other files.
Such a file is called Composite File and can be created by ordinary archiving
commands like following:

    $ zip foo.zip foo.gura utils.gura message.txt image.png
    $ mv foo.zip foo.gurc

Then you can run it as following:

    $ gura foo.gurc

A Composite File must a suffix `.gurc` or `.gurcw`
where `.gurc` is for command-line scripts and `.gurcw` for ones with GUI.
These suffixes are also associated with `gura.exe` and `guraw.exe` respectively
in Windows environment.
A script file that has the same name with that of the Composite File except for their suffix part
is recognized as a main script.
The interpreter reads that file at first when given with the Composite File.

You can also use a Gura module to create a Composite File.
Below is a script to create a Composite File `foo.gurc`.

    import(gurcbuild)
    gurcbuild.build(['foo.gura', 'utils.gura', 'message.txt', 'image.png'])

This script is more useful than using other archiving tools to create a Composite File
because the script will embed shebang comment at top of the file
and put executable attribute to it so that the created one can run
independently under Linux environment.


### Command Line Options

Available command line options are listed below:

Option             | Explanation
-------------------|------------------------------------------------------------
`-h`               | Prints a help message.
`-t`               | Runs a script file specified and then enters interactive mode.
`-i` *module*[`,` ..] | Imports modules in the same way as
                   calling `import` function in a script.
                   You can specify more than one module names for this option by separating them with comma.
                   Or, you can also specify the option in multiple times to import several modules.
`-I` *dir*         | Specifies a directory in which modules are searched.
                   | You can specify the option in multiple times to add several directories for module search.
`-c` *cmd*         | Runs *cmd* as a Gura script.
`-T` *template*    | Runs template engine to evaluate the specified template file.
`-C` *dir*         | Changes the current directory before running scripts.
`-d` *encoding*    | Specifies character encoding that the parser uses to read scripts.
`-v`               | Prints a version number.
