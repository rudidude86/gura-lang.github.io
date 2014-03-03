---
layout: page
lang: en
title: Flow Control
---

Flow Control
------------

### Conditional Branch

Like other programming languages, Gura also provides conditional branch control
that you've already been familiar with. See the code below:

    if (x < 0) {
        println('x is less than zero')
    } elsif (x > 0) {
        println('x is greater than zero')
    } else {
        println('x is equal to zero')
    }

Although appearance is very similar with that of other languages, there's a big problem.
In Gura, `if` is NOT a statement but a function, which means that `if` has a return value.

Consider the following code:

    str = if (x < 0) {
        'less than zero'
    } elsif (x > 0) {
        'greater than zero'
    } else {
        'equal to zero'
    }

In this case, `if` would have a return
with a value of last-evaluated result of `if`, `elsif` or `else`.

When `if` has no following `else` and its condition is not evaluated as `true`,
it will return `nil`.

### Repeat Control

Here are some simple codes that use typical repeat controls.

Sample code of `for`:

    for (fruit in ['orange', 'apple', 'grape']) {
        println(fruit)
    }

Sample code of `repeat`:


    repeat (10) {
        println('hello world')
    }

Sample code of `while`:

    n = 0
    while (n < 10) {
        println(n)
        n += 1
    }

You can specify a block parameter that takes a number of repeating index as following:

    repeat (10) {|i|
        println('hello world ', i)
    }

As these are also implemented as functions, you can see more special features with them.

    x = repeat (10):list {|i|
         i * 2
    }



    x = repeat (10):iter {|i|
         i * 2
    }

You can see more practical usage of this feature in [this](../articles/Script-to-Generate-Prime-Numbers.html).
