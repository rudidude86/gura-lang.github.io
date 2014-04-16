---
layout: page
lang: en
title: Module
chapter: 11
---

# Chapter {{ page.chapter }}. {{ page.title }}

## {{ page.chapter }}.1. Module as Environment

A **module** is a kind of environment and capable of containing variables and functions inside it.
You can use `module()` function that takes a block procedure containing expressions
of variable and function assignments. Below is an example:

    foo = module {
        var:public = 'hello'
        func() = { /* body */ }
    }

Then, you can call functions and read/modify variables in the module
with a member accessing operator `.` specifying the module on its left.

    foo.func()
    println(foo.var)

By default, functions defined in a module are marked as public and are accessible from outside.
On the other hand, variables are marked as private
and would cause an error with an access from outer scope.
You have to put `:public` attribute in a variable assignment to make it public.

You can use modules to isolate variables and functions from the current scope
by giving them an independent name space.
But its main purpose is to provide a mechanism to load external files
that extend the language's capability.


## {{ page.chapter }}.2. Import of Module File

Gura language has a policy that the interpreter itself should provide functions
that are less dependent on external libraries, operating systems and hardware specifications.
So, variety of functions such as handling regular expressions, image processing and GUI are
realized by dynamically loadable files called **module files**.

There are two types of module files: script module file and binary module file.

Module File        | Suffix  | Content
-------------------|---------|-------------------------------------------------
script module file | `.gura` | a usual Gura script file
binary module file | `.gurd` | a dynamic link library that has been compiled from C++ source code

A process of loading a module file and registering its properties to the current environment is called "import".
You can use `import()` function in your script to import a module like below:

    import(re)

This loads a module file `re.gurd` and creates a module `re` in the current scope.
After importing, functions like `re.match()` and `re.sub()` that the module provides become available.

You can also import modules at the timing of launching the interpreter
by specifying a command line option `-i` with module names.
Below is an example that imports a module `re` before parsing the script file `foo.gura`.

    $ gura -i re foo.gura

You can specify multiple module names by separating them with a comma character.

    $ gura -i re,http,png foo.gura

Under Windows, the interpreter searches module files in the following path,
where `GURA_VERSION` and `GURA_DIR` represent
the interpreter's version and the path name in which the program has been installed respectively.

1. current directory
2. directories specified by `-I` option in the command line
3. directories specified by environment variable `GURAPATH`
4. `%LOCALAPPDATA%\Gura\GURA_VERSION\module`
5. `GURA_DIR\module`
6. `GURA_DIR\module\site`

Under Linux, the interpreter searces module files in the following path.

1. current directory
2. directories specified by `-I` option in the command line
3. directories specified by environment variable `GURAPATH`
4. `$HOME/.gura/GURA_VERSION/module`
5. `/usr/lib/gura/GURA_VERSION/module`
6. `/usr/lib/gura/GURA_VERSION/module/site`

A variable `sys.path` is assigned with a list that contains path names to search module files.
You can add path names into the list while a script is running.


## {{ page.chapter }}.3. Script Module File

Take a look at how you can create a script module file and use it.
At first, create a file named `foo.gura` that contains the script below:

    var:public = 'hello'
    func() = { /* body */ }

Then, you can import it to make its properties available.

    import(foo)
    println(foo.var)
    foo.func()


## {{ page.chapter }}.4. Binary Module File

import binary module file only:

    import(bar):binary


## {{ page.chapter }}.5. List of Modules

Image file format:

<table>
<tr><th>Module</th><th>Note</th></tr>
<tr><td><code>bmp</code></td><td></td></tr>
<tr><td><code>gif</code></td><td></td></tr>
<tr><td><code>jpeg</code></td><td></td></tr>
<tr><td><code>msico</code></td><td></td></tr>
<tr><td><code>png</code></td><td></td></tr>
<tr><td><code>ppm</code></td><td></td></tr>
<tr><td><code>tiff</code></td><td></td></tr>
<tr><td><code>xpm</code></td><td></td></tr>
</table>

Compression/depression/archiving:

<table>
<tr><th>Module</th><th>Note</th></tr>
<tr><td><code>bzip2</code></td><td></td></tr>
<tr><td><code>gzip</code></td><td></td></tr>
<tr><td><code>tar</code></td><td></td></tr>
<tr><td><code>zip</code></td><td></td></tr>
</table>

Image operation:

<table>
<tr><th>Module</th><th>Note</th></tr>
<tr><td><code>cairo</code></td><td></td></tr>
<tr><td><code>freetype</code></td><td></td></tr>
<tr><td><code>glu</code></td><td></td></tr>
<tr><td><code>opengl</code></td><td></td></tr>
</table>

GUI operation:

<table>
<tr><th>Module</th><th>Note</th></tr>
<tr><td><code>canvas</code></td><td></td></tr>
<tr><td><code>sdl</code></td><td></td></tr>
<tr><td><code>tcl</code></td><td></td></tr>
<tr><td><code>tk</code></td><td></td></tr>
<tr><td><code>wx</code></td><td></td></tr>
<tr><td><code>show</code></td><td></td></tr>
<tr><td><code>wx.show</code></td><td></td></tr>
<tr><td><code>tk.show</code></td><td></td></tr>
</table>

Audio operation:

<table>
<tr><th>Module</th><th>Note</th></tr>
<tr><td><code>midi</code></td><td></td></tr>
<tr><td><code>wav</code></td><td></td></tr>
</table>

Network operation:

<table>
<tr><th>Module</th><th>Note</th></tr>
<tr><td><code>curl</code></td><td></td></tr>
<tr><td><code>http</code></td><td></td></tr>
</table>

Windows specific:

<table>
<tr><th>Module</th><th>Note</th></tr>
<tr><td><code>mswin</code></td><td></td></tr>
<tr><td><code>msxls</code></td><td></td></tr>
</table>

Text file operation:

<table>
<tr><th>Module</th><th>Note</th></tr>
<tr><td><code>csv</code></td><td></td></tr>
<tr><td><code>markdown</code></td><td></td></tr>
<tr><td><code>re</code></td><td></td></tr>
<tr><td><code>tokenizer</code></td><td></td></tr>
<tr><td><code>xhtml</code></td><td></td></tr>
<tr><td><code>xml</code></td><td></td></tr>
<tr><td><code>yaml</code></td><td></td></tr>
<tr><td><code>sed</code></td><td></td></tr>
</table>

Helper to build modules:

<table>
<tr><th>Module</th><th>Note</th></tr>
<tr><td><code>gurcbuild</code></td><td></td></tr>
<tr><td><code>modbuild</code></td><td></td></tr>
<tr><td><code>modgen</code></td><td></td></tr>
</table>

<table>
<tr><th>Module</th><th>Note</th></tr>
</table>

<table>
<tr><th>Module</th><th>Note</th></tr>
<tr><td><code>conio</code></td><td></td></tr>
<tr><td><code>gmp</code></td><td></td></tr>
<tr><td><code>guri</code></td><td></td></tr>
<tr><td><code>hash</code></td><td></td></tr>
<tr><td><code>sample</code></td><td></td></tr>
<tr><td><code>sqlite3</code></td><td></td></tr>
<tr><td><code>uuid</code></td><td></td></tr>

<tr><td><code>argopt</code></td><td></td></tr>
<tr><td><code>calendar</code></td><td></td></tr>
<tr><td><code>graph</code></td><td></td></tr>
<tr><td><code>testutil</code></td><td></td></tr>
<tr><td><code>units</code></td><td></td></tr>
<tr><td><code>utils</code></td><td></td></tr>
</table>

