---
layout: page
lang: en
title: Module
chapter: 11
---

# Chapter {{ page.chapter }}. {{ page.title }}

## {{ page.chapter }}.1. Module File

script module `.gura`

binary module `.gurd`

`import`

    import(`module, `alias?):void:[binary,mixin_type,overwrite] {block?}

search path for Windows

1. current directory
2. directories specified by `-I` option
3. directories specified by environment variable `GURAPATH`
4. `%LOCALAPPDATA%\Gura\GURA_VERSION\module`
5. `GURA_DIR\module`
6. `GURA_DIR\module\site`

search path for Linux

1. current directory
2. directories specified by `-I` option
3. directories specified by environment variable `GURAPATH`
4. $HOME/.gura/GURA_VERSION/module
5. `/usr/lib/gura/GURA_VERSION/module`
6. `/usr/lib/gura/GURA_VERSION/module/site`


`sys.path`




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
