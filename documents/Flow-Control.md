---
layout: page
lang: en
title: Flow Control
chapter: 8
---

## {{ page.chapter }}. Flow Control


## {{ page.chapter }}.1. Branch

Branch may be the most common flow-control in a program.
Just like other programming language,
Gura also provides `if` - `elsif` - `else` sequence.
However, they're realized as functions, not as statements.

These elements are implemented by the following functions.

Function `if`:

    if (`cond):leader {block}

Function `elsif`:

    elsif (`cond):leader:trailer {block}

Function `else`:

    else():trailer {block}

They are concatenated with leader-trailer relationship,
which means that a closing curly bracket of the preceding function
must be in the same line as the top of the succceding one.

    if (x) { /* branch 1 */ } elsif (y) { /* branch 2 */ } else { /* branch 3 */ }

Of course, contents in the blocks may be written in multiple lines.
This enables you to write a program in a similar syntax as other languages.

    if (x) {
        
        /* branch 1 */
        
    } elsif (y) {
        
        /* branch 2 */
        
    } else {
        
        /* branch 3 */
        
    }

Function `if` and `elsif` check the evaluated result of the expression `cond`.
If it's determined as `true`, the block procedure will be evaluated,
otherwise, the trailing function will be evaluated.
Function `else` always evaluates its block procedure.

Branch sequence has a result value as well. Consider the following code:

    result = if (x < 0) {
        'less than zero'
    } elsif (x > 0) {
        'greater than zero'
    } else {
        'equal to zero'
    }

In this case, if `x` is less than zero,
the sequence would have a string `'less than zero'` as its result.
It would have `'greater than zero'` for `x` with number greater than zero and
`'equal to zero'` otherwise.

If function `if` and `elsif` have no following `else` and their conditions are not evaluated as `true`,
the result value will be `nil`.


## {{ page.chapter }}.2. Repeat

## {{ page.chapter }}.2.1. Repeating Functions

This subsection explains about some representative functions
that evaluate a procedure repeatedly while it meets a given condition.

A function `repeat()` repeats a procedure for a specific number of times.

    repeat (n?:number) {block}

If argument `n` is omitted, it will repeat the procedure indefinitely.

A function `while()` repeats a procedure while the condition is evaluated as `true`.

    while (`cond) {block}

As a variable `cond` is an expression, it will be evaluated each time in the loop.
In the following example, the function is given with an expression `n < 10`,
which is to be evaluated during the repeating process.

    n = 0
    while (n < 10) {
        println('hello')
        n += 1
    }

A function `for()` takes one or more expressions of iterable assignments,
where an iterable means what can iterate elements including a list and an iterator instance.

    for (`expr+) {block}

An iterator assignment is expressed with an operator <code>in</code> like below.

<pre><code><em>symbol</em> in <em>iterable</em>
[<em>symbol1</em>, <em>symbol2</em> ..] in <em>iterable</em>
</code></pre>

In the first format, it assigns `symbol` with a value in `iterable` each time in the loop.
Below is an example.

    for (name in ['apple', 'grape', 'banana']) {
        // any process
    }

In the second format, if each element in the iterable is a list,
corresponding values in the list are assigned to `symbol1`, `symbol2`, and so on.
An example is shown below.

    for ([name, yen] in [['apple', 100], ['grape', 200], ['banana', 90]]) {
        // any process
    }

When a function `for()` takes more than one iterable assignment,
it advances all the iterables one by one at each loop
and repeats a procedure until one of the iterables reaches to the end.
This means that the loop count is limited up to the smallest length of the iterables.
The example below repeats the process three times.

    for (x in [1, 2, 3, 4], y in [1, 2, 3], z in [1, 2, 3, 4, 5]) {
        // any process
    }

A function `cross()` takes one or more expressions of iterator assignment
and repeats a procedure while advancing each iterator in a nested way.

    cross (`expr+) {block}

In `cross()` function, an iterable on the right advances at each loop
and, when it reaches to its end, it will be rounded up to its first
and causes an iterable on its left advance.

See the example below:

    cross (x in ['A', 'B', 'C'], y in [1, 2, 3, 4]) {
        print(x, '-', y, ' ')
    }
    println()

The result is:

    A-1 A-2 A-3 A-4 B-1 B-2 B-3 B-4 C-1 C-2 C-3 C-4


## {{ page.chapter }}.2.5. Flow Control in Repeat Sequence

    break(value?):symbol_func:void

    continue(value?):symbol_func:void


## {{ page.chapter }}.2.6. List Generation


## {{ page.chapter }}.2.7. Iterator Generation

Appending an attribute `:list` causes the repeating process to generate a list
that contains evaluated result of each loop as its elements.
In the following example, `x` will be a list of `[0, 2, 4, 6, 8]`.

    x = repeat (5):list {|i|
         i * 2
    }

An attribute `:iter` would have a more interesting result. Take a look at the code below:

    x = repeat (5):iter {|i|
         i * 2
    }

In this case, repeating process is not executed when the `repeat` function is evaluated.
`x` is an *iterator* that generates values of 0, 2, 4, 6 and 8,
and these values are only available when the iterator is actually evaluated.

The following code shows how to get the value after evaluating the iterator using Implicit Mapping:

    println(x)

Following code evaluates `x` step by step to confirm that it actually works as an iterator.

    println(x.next())
    println(x.next())
    println(x.next())
    println(x.next())
    println(x.next())

And now, to a next topic about iterators generated by repeating functions.

Consider the following code.

    f() = {
        n = 0
        while (n < 5):iter {
            n += 1
            n
        }
    }
    x = f()

The function `f` returns an iterator created by `while`,
which is expected to generate values of 1, 2, 3, 4 and 5.
In this case, the repeat body has a reference to a variable named `n` that belongs
to the scope of function `f`.
Can an iterator refer to a variable that may be destroyed at the end of a function?

Actually, it's OK. An iterator created by a repeating function owns an environment
in which the function has been called.
In the above example, the variable `n` is owned by the returned iterator.

You'll see more practical usage of this feature in [this](../articles/Script-to-Generate-Prime-Numbers.html).


topic about nesting:

    iterator#repeater()


## {{ page.chapter }}.3. Exception

    try - catch
    
    try():leader {block}
    catch(errors*:error):leader:trailer {block}
    
    raise(error:error, msg:string => 'error', value?)


