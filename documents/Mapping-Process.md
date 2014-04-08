---
layout: page
lang: en
title: Mapping Process
chapter: 10
---

# Chapter {{ page.chapter }}. {{ page.title }}

## {{ page.chapter }}.1. Overview

Using Implicit Mapping, you don't have to write repeat procedure
to evaluate iterables such as iterator and list.

* scholar &mdash; instance of any type except `list` and `iterator`
* list &mdash; instance of `list`
* iterator &mdash; instance of `iterator`

## {{ page.chapter }}.2. Implicit Mapping


### {{ page.chapter }}.2.1. Implicit Mapping with Operator


Operation    | Result
-------------|----------------
`o scholar`  | scholar
`o list`     | list
`o iterator` | iterator

Operation             | Result
----------------------|----------------
`scholar o scholar`   | scholar
`scholar o list`      | list
`scholar o iterator`  | iterator
`list o scholar`      | list
`list o list`         | list
`list o iterator`     | iterator
`iterator o scholar`  | iterator
`iterator o list`     | iterator
`iterator o iterator` | iterator


### {{ page.chapter }}.2.2. Implicit Mapping with Function

A function capable of Implicit Mapping has `:map` attribute in its declaration.

Consider a function that has a declaration of `f(x):map`.

Operation     | Result
--------------|----------------
`f(scholar)`  | scholar
`f(list)`     | list
`f(iterator)` | iterator

If a function contains an argument that expects `list` or `iterator`,
Implicit Mapping would not work with that argument.

`:nomap` attribute

`f(list):iter`
    
`f(iterator):list`


    f(x:nomap, y:nomap) = {}

### {{ page.chapter }}.2.3. Disable Implicit Mapping

    f():nomap
    
    x = [1, 2, 3, 4]
    println(x)
    println(x):nomap

### {{ page.chapter }}.2.4. Definition of Function Capable of Implicit Mapping

    f():map = { /* body */ }

## {{ page.chapter }}.3. Member Mapping

Member Mapping

    iterable::variable
    iterable:*variable
    iterable:&variable
    iterable::func()
    iterable:*func()
    iterable:&func()
    
    
