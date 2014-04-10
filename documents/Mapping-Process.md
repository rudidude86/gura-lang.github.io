---
layout: page
lang: en
title: Mapping Process
chapter: 10
---

# Chapter {{ page.chapter }}. {{ page.title }}

## {{ page.chapter }}.1. About This Chapter

This chapter explains about Gura's mapping process, Implicit Mapping and Member Mapping.
In the explanation, following terms are used to describe species of values.

* scholar &mdash; an instance of any type except for `list` and `iterator`
* list &mdash; an instance of `list`
* iterator &mdash; an instance of `iterator`


## {{ page.chapter }}.2. Implicit Mapping

### {{ page.chapter }}.2.1. Overview

**Implicit Mapping** is a feature that evaluates a function or an operator repeatedly
when it's given with a list or an iterator.

A function that is capable of Implicit Mapping is marked with an attribute `:map`.
Consider a function `f(n:number):map` that takes a number value and returns a squared number of it.
You can call it like `f(3)`, which is expected to return a number `9`.
Here, using Implicit Mapping, you can call it with a list of numbers like below:

    f([2, 3, 4])

This will result in a list `[4, 9, 16]` after evaluating each number in the list.

Implicit Mapping also works with operators.
Below is an example that applies Implicit Mapping on plus operator:

    [2, 3, 4] + 3

This will result in `[5, 6, 7]`. Of course,
you can also apply it on an operation between two lists.
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

   Consider a function `g(str:string):map` that takes a string and returns a result
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

   Consider the function `g(str:string):map` that has been mentioned above.
   If you call it with an iterator, it will return an iterator as its result.
   
        strs = ['hello', 'Gura', 'world']
        x = g(strs.each())  // list#each() returns an iterator
        // x is an iterator that will generates 'HELLO', 'GURA' and 'WORLD'.
   
   It means that the actual evaluation of the function `g()` will be postponed
   by the time when the created iterator is evaluated.
   This is important because using an iterator will enable you to
   avoid unnecessary calculation and memory consumption.

3. You can use Implicit Mapping to repeat a function call without an explicit repeat procedure.

   A built-in function `println():map` prints a content of the given value
   before putting out a line-feed.
   Consider a case that you need to print each value in the list `strs`
   that contains `['hello', 'Gura', 'world']`.
   With an ordinary idea, you may use `for()` to process each item in a list.

        for (str in strs) {
            println(str)
        }

   Using Implicit Mapping, you can simply do it like below:

        println(strs)

4. Implicit Mapping can work on any number of lists and iterators
   given in an argument list of a function call.
   
   Consider that there's a function `f(a:string, b:number, c:string):map`,
   and you give it lists as its arguments like below:

        as = ['first', 'second', 'third', 'fourth']
        bs = [1, 2, 3, 4]
        cs = ['one', 'two', 'three', 'four']
        f(as, bs, cs)

   This has the same effect as below:

        f('first', 1, 'one')
        f('second', 2, 'two')
        f('third', 3, 'three')
        f('fourth', 4, 'four')


### {{ page.chapter }}.2.2. Mapping Rule with Operator

Implicit Mapping works on most of the operators even though there are a few exceptions.
In the description below, a symbol `o` is used to represent a certain operator.

With a Prefixed Unary Operator,
the species of the result is the same as that of the given value.
Below is a summary table:

Operation    | Result
-------------|----------------
`o scholar`  | scholar
`o list`     | list
`o iterator` | iterator

With a Suffixed Unary Operator,
the species of the result is the same as that of the given value.
Below is a summary table:

Operation    | Result
-------------|----------------
`scholar o`  | scholar
`list o`     | list
`iterator o` | iterator

There are some exceptions:

* An operation `x?` checks if `x` can be determined as `true` or not.
* An operation `x*` generates an iterator from `x`.

With a Binary Operator, the folloiwing rules are applied.

* If both of left or right value are of scholar species, the result becomes a scholar.
* If either of left or right value is of iterator species, the result becomes an iterator.
* Otherwise, the result becomes a list.

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

There are some exceptions:

* An operation `x * y` where `x` is of `function` type
* An operation `x % y` where `x` is of `string` type
* An operation `x in y`
* An operation `x => y`


### {{ page.chapter }}.2.3. Mapping Rule with Function

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

### {{ page.chapter }}.2.4. Disable Implicit Mapping

    f():nomap
    
    x = [1, 2, 3, 4]
    println(x)
    println(x):nomap

### {{ page.chapter }}.2.5. Definition of Function Capable of Implicit Mapping

    f():map = { /* body */ }


## {{ page.chapter }}.3. Member Mapping

### {{ page.chapter }}.3.1. Overview

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


### {{ page.chapter }}.3.2. Mapping Rule

Accessor |Name
---------|------------------
`::`     |map-to-list
`:*`     |map-to-iterator
`:&`     |map-along

    iterable::variable
    iterable:*variable
    iterable:&variable
    iterable::func()
    iterable:*func()
    iterable:&func()
    
    
