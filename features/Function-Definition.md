---
layout: page
lang: en
title: Function Definition
---

{{ page.title }}
----------------

### Simple Definition

In Gura, function can be defined in the same way with variable assignment
except that the assignee should be described in a function form.
Following is the simple example

    hello() = println('hello world')

And you can call it like following:

    hello()

If you want to pass arguments to a function,
specify them in the assignee's argument list.

    hello(name) = println('hello, ', name)

You can also specify a variable type of each argument by declaring the type name followed by a colon.

    hello(name:string) = println('hello, ', name)

The declaration of type is convenient
because it's capable of checking the data type and casting them if possible.

If the function body consists of multiple expressions,
they have to be described in a block.

    hello(name:string) = {
        println('hello, ', name)
    }

### Arguments

You can specify optional arguments, default values and variable-length arguments
for function declarations.


    f1(a, b?, c?) = printf('%s, %s, %s\n', a, b, c)
    f1(2)                                # 2, nil, nil
    
    f2(a, b = 10, c => 'abc') = printf('%s, %s, %s\n', a, b, c)
    f2(2)                                # 2, 10, abc
    
    f3(a, b, c*) = printf('%s, %s, %s\n', a, b, c):nomap
    f3(2, 3, 4, 5, 6, 7)                 # 2, 3, [4, 5, 6, 7]
    f3(2, 3)                             # 2, 3, []
    
    f4(a, b, c+) = printf('%s, %s, %s\n', a, b, c):nomap
    f4(2, 3, 4, 5, 6, 7)                 # 2, 3, [4, 5, 6, 7].
    f4(2, 3)                             # error. c has to get at least one value.


When calling a function, you can specify each argument value by a keyword.
A keyword shall be associated with its value with dictionary assignment operator
`=>`.

    g1(a, b, c) = printf('%s, %s, %s\n', a, b, c)
    g1(2, b => 3, c => 4)                # 2, 3, 4


If the argument declaration list contains a symbol suffixed by percent character `%`,
the symbol shall be assigned with a dictionary consisting of pairs of
keywords and values that have not matched the argument list.

    g2(a, b, dict%) = printf('%s, %s, %s\n', a, b, dict)
    g2(2, b => 3, c => 4, d => 5)        # 2, 3, %{c => 4, d => 5}
    g2(2, 3, c => 4, d => 5)             # 2, 3, %{c => 4, d => 5}


### Block Expression

You can declare functions that has a block expression.
This mechanism is used in variety of ways such as implementation of statements like `if` and `while`,
initial declaration of list and dictionary items, and so on.

The following is a simple example of declaring a function with a block.

    f(x:number) {block} = {
        block(x)
        block(x + 1)
        block(x + 2)
    }

You can call it like follows.

    f(2) {|x|
        print(x)
    } # 234

A block itself is a function object that has a special variable scope.
and it takes a list of block parameter as its arguments.
You can use any argument specifier like optional argument, default values
and variable-length arguments for block parameters as well.

    x = 0
    f(2) {|x|
        print(x)
    }
    println(x)        # 0

You can use any symbol to specify the block.

    f(x:number) {yield} = {
        yield(x)
        yield(x + 1)
        yield(x + 2)
    }

A block specified by a symbol with a question character suffix shall be
treated as an optional one. If the function is called without a block,
that symbol is assigned to `nil`.

    f_opt() {block?} = {
        if (block == nil) {
            println('not specified')
        } else {
            block()
        }
    }
    
    f_opt() # print 'not specified'
    
    f_opt() {
        println('message from block')
    }       # print 'message from block'

A block usually works with a variable scope that can access to an 'external' environment
of the function.

    g() {block} = {
        block()
    }
    
    n = 2
    g() {
        n = 5
    }
    printf('n = %d\n', n) # n = 5


### Quoted Value

In normal case, when you specify expressions in the argument list of function call,
their evaluation results are passed to a function.
However, if the function specify an argument symbol prefixed with a backquote character
in its declaration, a pre-evaluated expression shall be passed to the function as a
Quoted value.

The following example creates a function that works just like for statement
in C language.

    c_like_for(`init, `cond, `next) {`block} = {
        env = outers()
        init.eval(env)
        while (cond.eval(env)) {
            block.eval(env)
            next.eval(env)
        }
    }
    
    n = 0
    c_like_for (i = 1, i <= 10, i += 1) {
        n += i
    }
    printf('i = %d, sum = %d\n', i, n)
