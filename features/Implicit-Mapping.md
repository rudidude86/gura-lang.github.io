---
layout: page
lang: en
title: Implicit Mapping
---

# {{ page.title }}

## Basic Idea

Here, consider a process to draw a mathematical graph of y = x<sup>2</sup>.
Let us do it by calculating values of y-coordinate for x between -5 and 5 stepped by one
and putting plots on a scrren position corresponding those location.

When you implment this with one of ordinary programming language,
it would be a common way to repeat a calculation by using a loop statement.
With C language, you could come up with the following program.

    const float x[] = {-5, -4, -3, -2, -1, 0, 1, 2, 3, 4, 5 };
    float y[11];
    for (int i = 0; i < 11; i++) {
        y[i] = x[i] * x[i];
    }

When using a language that promotes functional programming,
you would think of applying a higher-order function for the same goal.
In the case of LISP, the above program can be described like follows using map that
performs mapping process.

    (map (lambda (x) (* x x)) '(-5 -4 -3 -2 -1 0 1 2 3 4 5))

It's so elegant. Besides LISP, an idea of higher-order function is a powerful solution
to recognize something in an abstractive way.
However, it would sometimes be hard for beginners to think something abstractively.

What we want to achieve here is a very simple task in the first place:
Get values of x<sup>2</sup> for a list of x values.
Can't we get the answer by the following description?

    x = [-5, -4, -3, -2, -1, 0, 1, 2, 3, 4, 5]
    y = x * x

The expression `x * x` expects a single value for x.
If such an expression has a mechanism to map multiple values implicitly after given
a list of values for x, users are able to get a desirable result without
any care about repeating process.

The implementation of Implicit-mapping has started at this inspiration.


## Case Study

The followings are examples of applying Implicit-mapping to operators.

    >>> [1, 2, 3, 4] + [5, 6, 7, 8]
    [6, 8, 10, 12]
    >>> [1, 2, 3, 4] + 5
    [6, 7, 8, 9]
    >>> ([1, 2, 3, 4] + [5, 6, 7, 8]) / 2
    [3, 4, 5, 6]
    >>> [3, 8, 0, 4] < [4, 5, 3, 1]
    [true, false, true, false]

The following is an example of applying it to function calls.

    >>> math.sqrt([1, 2, 3, 4])
    [1, 1.41421, 1.73205, 2]

You could resolve a lot of problems without control statement
when you combine the usage of Implicit-mapping with variety of functions of
I/O and data processing.
Here's an example.

    >>> x = [1, 2, 3, 4]
    >>> printf('result = %2d, %2d, %2d, %f\n', x, x * x, x * x * x, math.sqrt(x))
    result =  1,  1,  1, 1.000000
    result =  2,  4,  8, 1.414214
    result =  3,  9, 27, 1.732051
    result =  4, 16, 64, 2.000000

Expressions like `x * x` and `math.sqrt(x)` calculate values of each item in the list with Implicit-mapping.
Then, printf also work with Implicit-mapping and prints each item of the lists given as its arguments.
The function printf has no return value, so it doesn't generate a list as a result.

You can write a program that displays contents of a file with line number
like follows.

    printf('%7d %s', (1..), readlines('hoge.txt'))

Expressions `1..` and `file#readlines()` return an iterator, not a list.
Implicit-mapping also work in correspondance with iterators.
Expression `1..` means an infinite sequence from 1 while `file#readlines()`
means each line of a file that finishes in finite amount.
In the case that Implicit-mapping is given with
lists or iterators that has different length of items, it would work until
the shorter one finishes. So, in the above case, the mapping process shall
finish when `file#readlines()` ends.

The following code shows an example that prints information exctracted
from a file.

    import(re)
    lines = readlines('hoge.h')
    println(re.match(r'class (\w+)', lines).skipnil():*group(1))

Function `re.match()` returns an iterator that generates match instance
after processing an iterator lines from `file#readlines()`.
As the function returns nil if the string mismatches the pattern,
`iterator#skipnil()` is used to create an iterator that skips nil value.
Operator `:*` is a Member-mapping operator, and it executes `match#group()` method
for each item in the iterator.
