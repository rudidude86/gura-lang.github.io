---
layout: page
lang: en
title: Script to Generate Prime Numbers
---

# {{ page.title }}

Gura's `for` function can return an iterator for the repeat process instead of executing the loop immediately.
Following is an example to make an iterator that generates prime numbers.

    prime() = {
        p = []
        for (n in 2..):xiter {
            if (!(n % p == 0).or()) {
                p.add(n)
                n
            }
        }
    }
    println(prime())

An attribute `:xiter` indicates that `for` should return an iterator in which each item is an evaluated result in the `for` block. The function `if` has a returned value which will be set to the evaluated value in block when condition is true, or to `nil` otherwise.  In this case, when the condition `!(n % p == 0).or()` is evaluated as true, `n` becomes the item value. Because an attribute `:xiter` will skip `nil` value, only the value of `n` will be generated from the iterator.

I may have to explain what happens in the code `!(n % p == 0).or()`
because it utilizes one of Gura's important features, [Implicit Mapping](../features/Implicit-Mapping.html).

Consider the case that `p` contains `[2, 3, 5, 7]` and `n` is 9.
This will be evaluated as following.

1. `n % p` will be evaluated as `[1, 0, 4, 2]` after `%` operator is applied to each item in `p` by Implicit Mapping.
2. `n % p == 0` will result in `[false, true, false, false]` by applying `==` operator on each item as well.
3. `(n % p == 0).or()` causes `true` as the list class method `list#or()` returns `true` when one of list's items is `true`.
4. `!(n % p == 0).or()` is evaluated as `false` for this case.

You can improve the code of the condition expresion of `if` as following.

    prime() = {
        p = []
        for (n in 2..):xiter {
            if (!(n % p.each() == 0).or()) {
                p.add(n)
                n
            }
        }
    }

In this case, `list#each()` method converts the list `p` into an iterator,
so the result of `n % p.each()` will be an iterator as well.
And then, `n % p.each() == 0` will also become an iterator.

This means that actual evaluation of operator `%` and `==` will be postponed
until the timing at which `iterator#or()` method requires the value.
This causes a better performance
because there's no need to calculate on all the items in the list `p`.

As prime numbers more than two should be odd,
you can eliminate even numbers from `n`'s sequence except two like following.

    prime() = {
        p = []
        for (n in (2, range(3, nil, 2))):xiter {
            if (!(n % p.each() == 0).or()) {
                p.add(n)
                n
            }
        }
    }

The function call `range(3, nil, 2)` returns an iterator that generates a sequence
starting from three stepped by two.
A pair of parenthehses surronding values and iterators creates an iterator that combines them,
so the code `(2, range(3, nil, 2))` will generate a sequence of 2, 3, 5, 7, 9, 11 ...

Further more, you can limit the range to check
if a certain number is divisible by already found prime numbers.

    prime() = {
        p = []
        for (n in (2, range(3, nil, 2))):xiter {
            if (!(n % p.while(p.each() * p <= n) == 0).or()) {
                p.add(n)
                n
            }
        }
    }

To see what happens in the `if` condition,
consider the case that `p` contains `[2, 3, 5, 7]` and `n` is `11`.

1. `p.each() * p` is an iterator that is supposed to generate squared numbers of `p`
   like `(4, 9, 25, 49)`.
2. `p.each() * p <= n` is an iterator that returns `true`
   when squared value of `p` is less than or equal to `n`,
   which is expected to genrate a sequence like `(true, true, false, false)`.
3. Iterator's method `iterator#while` returns the element values
   only while an iterator in its argument returns `true`.
   So `p.while(p.each() * p <= n)` returns a limited range of sequence `(2, 3)`.
