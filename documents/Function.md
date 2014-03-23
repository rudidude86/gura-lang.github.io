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

The body must a single expression.
If you want to describe more than one expression,
you have to use a Block expression embracing them like following.

    f(x, y, z) = {
        printf('x = %s, y = %s, z = %s\n', x, y, z)
    }

After defining a function, a `function` instance is assigned to a variable with the identifier.
You can see the declaration by simply printing the instance like following.

    println(f)

The argument list is a list of Identifier expressions.
If no argument is necessary, specify an empty list.

    f() = {}

You can specify a type name by describing it as an attribute
after an identifier's symbol.

    f(x:number) = {}



    f(`x) = {}

    f(x?) = {}

    f(x+) = {}

    f(x*) = {}


    f(x => y) = {}


    f(x) {block} = {}

    f(x) {block?} = {}

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
