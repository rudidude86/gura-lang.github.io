---
layout: page
lang: en
title: Create Your Own Binary Module
---

Create Your Own Binary Module
-----------------------------

Gura has a mechanism to support users who create binary modules.
This document shows how to create an original binary module hoge.

At first, execute the following command.

    $ gura -i modgen hoge

This would generate a builder script, build.gura, and a template source file of module,
Module_hoge.cpp. Although the file Module_hoge.cpp is just a C++ source file
that consists of less than 40 lines of codes, it already has an implementation
for a Gura function named test.

Executing build.gura would create the module by launching a proper C++ compiler.
If you try it in Windows, you need to install
Visual Studio 2010 in advance.
You may use Express version that is available for free of charge.

    $ gura build.gura --here

If you find a binary module file hoge.gurd has successfully been built in the current directory,
import it into Gura's script and test it.

    $ gura
    >>> import(hoge)
    >>> dir(hoge)
    [`__name__, `test]
    >>> hoge.test(3, 5)
    8

Congratulations! It's ready to edit Module_hoge.cpp for implementations as you like.
If you get what you want, execute the following command to install the module
into Gura's environment.

    $ sudo gura build.gura install

By the way, you need to get some information about C++ functions and
classes provided by Gura for actual programming.
The best way for it is to see source files of other binary modules.
At first, find out a module from those provided by Gura,
which has a function similar to what you want to create.
You can find module source files in a directory gura/src/Module_module
in a source package.
Each module is so simple that consists of one to two source files.
I'm sure it's relatively easy to know how to realize your purpose by investigating them,
because they have been developed in the same coding policy.
