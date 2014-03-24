---
layout: page
lang: en
title: Function
chapter: 7
---

# Chapter {{ page.chapter }}. {{ page.title }}

## {{ page.chapter }}.1. Overview

A function is an instance of `function` class.


## {{ page.chapter }}.2. Function Definition

The figure below shows an example of function definition with each part's designation.

        +-- declaration
        |
    ----------
    f(x, y, z) = printf('x = %s, y = %s, z = %s\n', x, y, z)
    - -------    -------------------------------------------
    |   |                            |
    |   +-- argument list            +-- body
    +-- identifier

It composes of a declaration and a body with an assignment operator,
and the declaration is made up with an identifier and an argument list.

The body must be a single expression.
If you want to describe more than one expression,
you have to use a Block expression embracing them like following.

    f(x, y, z) = {
        printf('x = %s, y = %s, z = %s\n', x, y, z)
    }

After defining a function, a `function` instance is assigned
in the scope environment with the identifier.
If the same identifier already exists in the environment,
the existing one is overwritten no matter whether it's a `function` instance or other.

You can see a function's declaration by simply printing the instance like following.

    println(f)

The argument list is a list of Identifier expressions.
If no argument is necessary, specify an empty list.

    f() = { /* body */ }

You can specify a type name by describing it as an attribute
after an Identifier's symbol.

    f(x:number) = { /* body */ }

When calling a function that has arguments with type name,
the Interpreter first check the type of the given value and try to cast it
into specified type if possible.
If the type doesn't match and also fails to be casted correctly,
it would occur an error.

You can declare an optional argument by putting `?` right after an Identifier's symbol.

    f(x?) = { /* body */ }

If you want to declare a type name for an optional argument, specify it like following.

    f(x?:number) = { /* body */ }

For such a function, you can call it like following.

    f(3)
    f()

If the Caller omits a value for an optional argument,
a variable for the argument would be in undefined state.
You can use `isdefined()` function to check if the variable is defined or not.

    f(x?) = {
        if (isdefined(x)) {
            // when x is specified
        } else {
            // when x is omitted
        }
    }

You can specify more than one optional argument.
Note that it's inhibited to declare any non-optional arguments following after optional one.

    f(x?, y?, z?) = { /* body */ }  // OK
    f(x, y?, z?)  = { /* body */ }  // OK
    f(x?, y?, z)  = { /* body */ }  // error

An argument with a default value can be declared with an operator `=>`.

    f(x => -1) = { /* body */ }

If you want to declare a type name for an argument with a default value, specify it like following.

    f(x:number => -1) = { /* body */ }

For such a function, you can call it like following.

    f(3)
    f()

If the Caller omits a value for an argument with a default value,
a variable for the argument would be set to the specified default value.

You can specify more than one arguments with default value.
Note that any arguments that don't have a default value can not
follow after one with a default value.

    f(x => 1, y => 2, z => 3) = { /* body */ }  // OK
    f(x, y => 2, z => 3)      = { /* body */ }  // OK
    f(x => 1, y => 2, z)      = { /* body */ }  // error

Optional arguments and arguments with default value
follow the same positioning rule each other in an argument list.

    f(x => 1, y => 2, z?) = { /* body */ }  // OK

You can also declare a variable-length argument by putting `+` or `*`
right after an Identifier's symbol.

    f(x+) = { /* body */ }
    f(x*) = { /* body */ }

For the first one, the Caller can call it with **one** or more values.
If it doesn't specify any value for the argument, it would occur an error.

For the second one, the Caller can call it with **zero** or more values.
It can even call it without any argument.

If you want to declare a type name for a variable-length argument, specify it like following.

    f(x+:number) = { /* body */ }

The variable-length argument can only be declared once and must be placed at the last.

    f(x, y, z+)  = { /* body */ }  // OK
    f(x, y+, z+) = { /* body */ }  // error
    f(x, y+, z)  = { /* body */ }  // error



quoted value

    f(`x) = { /* body */ }

block declaration

    f(x) {block} = { /* body */ }

    f(x) {block?} = { /* body */ }

attributes

    f(x):[foo,bar] = {
        __args__.isset(`foo)
    }


## {{ page.chapter }}.3. Function Call

When the interpreter evaluated a `Caller` expression
and its car element is of `function` type,
it will evaluate the function with specified arguments.


## {{ page.chapter }}.4. Flow Control

## {{ page.chapter }}.4.1. Branch

    

    if - elsif - else

    

    if (`cond):leader {block}
    elsif (`cond):leader:trailer {block}
    else():trailer {block}

## {{ page.chapter }}.4.2. Repeat

    repeat (n?:number) {block}
    
    while (`cond) {block}
    
    for
    
    cross
    
    break
    
    continue
    
## {{ page.chapter }}.4.3. Exception

    try - catch
    
    raise
