---
layout: page
lang: en
title: Module
chapter: 11
---

# Chapter {{ page.chapter }}. {{ page.title }}

## {{ page.chapter }}.1. Module File

Gura language has a policy that the interpreter itself should provide functions
that can be realized without external libraries.
So, variety of functions such as handling regular expressions, image processing and GUI are
provided by dynamically loadable **module files**.

There are two types of module files: script module file and binary module file.

* Script module file is a usual Gura script file and has a suffix `.gura`.
* Binary module file is a dynamic library file that has been compiled from C++ source code
and has a suffix `.gurd`.

A process of loading a module file and registering its properties to the current environment is called "import".
You can import a module using `import()` function in a script like below:

    import(re)

This loads a module file `re.gurd` and creates a module `re` in the current scope.
After importing, functions like `re.match()` and `re.sub()` that the module provides become available.

Under Windows, the interpreter searches module files in the following path,
where `GURA_VERSION` and `GURA_DIR` represent
the interpreter's version and the path name in which the program has been installed respectively.

1. current directory
2. directories specified by `-I` option
3. directories specified by environment variable `GURAPATH`
4. `%LOCALAPPDATA%\Gura\GURA_VERSION\module`
5. `GURA_DIR\module`
6. `GURA_DIR\module\site`

Under Linux, the interpreter searces module files in the following path.

1. current directory
2. directories specified by `-I` option
3. directories specified by environment variable `GURAPATH`
4. `$HOME/.gura/GURA_VERSION/module`
5. `/usr/lib/gura/GURA_VERSION/module`
6. `/usr/lib/gura/GURA_VERSION/module/site`

A variable `sys.path` is assigned with a list that contains path names to search module files.
You can add path names into the list in the script as well.


    import(`module, `alias?):void:[binary,mixin_type,overwrite] {block?}

`foo.gura`

    var1 = 'hello'
    var2:public = 'hello'

    func1() = {}
    func2():private = {}

`main.gura`

    import(foo)
    println(foo.var1)  // 
    println(foo.var2)  // 
    foo.func1()        // 
    foo.func2()        // 


module as naming space

    foo = module {
    
    }
