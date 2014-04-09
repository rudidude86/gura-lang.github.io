---
layout: page
lang: en
title: Mapping Process
chapter: 10
---

# Chapter {{ page.chapter }}. {{ page.title }}

## {{ page.chapter }}.1. Overview

**Implicit Mapping** is a feature that evaluates a function or an operator repeatedly
when it's given with a list or an iterator.

Consider a function `f(n)` that takes a number value and returns a squared number of it.
You can call it like `f(3)`, which is expected to return a number `9`.
Here, using Implicit Mapping, you can call it with a list of numbers like below:

    f([2, 3, 4])

This will result in a list `[4, 9, 16]` after evaluating each number in the list.

Implicit Mapping also works with operators.
Below is an example that applies Implicit Mapping on plus operator:

    [2, 3, 4] + 3

This will result in `[5, 6, 7]`. Of course, an operation between two lists is also available.
See the following example:

    [2, 3, 4] + [3, 4, 5]

As you might expect, it returns a list `[5, 7, 9]`.

The above example may just look like a vector calculation.
Actually, this type of operation,
which applies some operations on a set of numbers at once,
is known as "vectorization", and has been implemented in languages and libraries
that compute vectors and matrices.

Implicit Mapping enhances that idea so that it has the following capabilities:

1. Implicit Mapping can handle any type of objects other than number.

   Consider a function `g(str)` that takes a string and returns a result
   after converting alphabet characters in the string to upper case.
   When you call it with a single value, it will return one result.

        str = 'hello'
        x = g(str)
        // x is 'HELLO'

   You can call it with a list of string
   to get a list of results by using Implicit Mapping feature.

        strs = ['hello', 'Gura', 'world']
        x = g(strs)
        // x is ['HELLO', 'GURA', 'WORLD']

2. Implicit Mapping can operate with an iterator as well.

   Consider the function `g(str)` mentioned above.
   If you call it with an iterator, it will return an iterator as well.
   
        strs = ['hello', 'Gura', 'world']
        x = g(strs.each())
        // x is an iterator that will generates 'HELLO', 'GURA' and 'WORLD'.
   
   It means that the actual evaluation of the function `g()` will be postponed
   by the time when the created iterator is evaluated.
   This is important because using an iterator will enable you to
   avoid unnecessary calculation and memory consumption.

3. You can use Implicit Mapping to repeat a function call without an explicit repeat procedure.

   A built-in function `println()` prints a content of the given value along with line-feed.
   Consider a case that you need to print each value in the list `strs`
   containing `['hello', 'Gura', 'world']`.
   With an ordinary idea, you may use `for()` to process each item in a list.

        for (str in strs) {
            println(str)
        }

   Using Implicit Mapping, you can simply do it like below:

        println(strs)

4. A function with Implicit Mapping can take any number of lists and iterators as its argument.
   
   In the example below the function `f()` takes each item of `a`, `b` and `c`
   and ends up being evaluated four times.

        a = ['first', 'second', 'third', 'fourth']
        b = [1, 2, 3, 4]
        c = ['one', 'two', 'three', 'four']
        f(a, b, c)

**Member Mapping** is a feature to access members of instances
that are stored in a list or are generated from an iterator.

For example, there's a method `string#len()` that retrieves a length of the string.
You can call it like below:

    x = 'first'
    n = x.len()
    // n is 5

Using Member Mapping, you can apply the method on instances in a list.

    xs = ['first', 'second', 'third', 'fourth']
    ns = xs::len()
    // ns is [5, 6, 5, 6]

This chapter explains details about Gura's mapping process,
Implicit Mapping and Member Mapping, using the following terms.

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
    
    
