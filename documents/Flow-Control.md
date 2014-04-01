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


### {{ page.chapter }}.2.1. Repeating Functions

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

A function `cross()` takes one or more expressions of iterable assignment
and repeats a procedure with all the conceivable combination of elements from the iterables.

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

You can specify any number of iterable assignments.

    cross (x in ['A', 'B', 'C'], y in [1, 2, 3, 4], z in ['a', 'b', 'c']) {
        print(x, '-', y, '-', z, ' ')
    }


### {{ page.chapter }}.2.2. Block Parameter

When calling `for()`, `while()` and `for()`,
you can specify a block parameter in a format of `|i:number|`
that takes an index number of loop starting from zero.
In the following example,
the parameter `i` takes `0`, `1`, `2`, `3` and `4` at each loop.

    repeat (5) {|i|
        // any process
    }

A block parameter for `cross()` function has a format of
`|i:number, i1:number, i2:number, ..|` where `i` indicates an index number of loop,
and each of `i1`, `i2` and so on takes an index number of corresponding iterable.

    cross (x in ['A', 'B', 'C'], y in [1, 2, 3, 4], z in ['a', 'b', 'c']) {|i, ix, iy, iz|
        // any process
    }

If you don't need indices information, you can omit whole the block parameter
or part of its parameters.


### {{ page.chapter }}.2.3. Result Value of Repeat

Like a branch sequence, a repeat sequence also has a result value
that comes from an evaluation of the last expression in the block procedure.

In default, among result values that have been generated from each loop,
only the last one becomes the final result.

    x = repat (10) {|i|
        // any process
        i * 10
    }
    // x is 90

When you call a repeat function with `:list` attribute,
it will return a list that contains result values in the loop.

    x = repat (10):list {|i|
        // any process
        i * 10
    }
    // x is [0, 10, 20, 30, 40, 50, 60, 70, 80, 90]

With an attribute `:xlist`, you can remove `nil` value from the created list.

    x = repeat (10):xlist {|i|
        // any process
        if (i % 2 == 0) { i * 10 }
    }
    // x is [0, 20, 40, 60, 80]

Using this feature, you can create a list that only contains elements
that suit some conditions.

Attributes `:set` and `:xset` work in a similar way with `:list` and `:xlist` respectively,
but they would create a list that contains unique values
by rejecting a value that already exists in the list.


### {{ page.chapter }}.2.4. Flow Control in Repeat Sequence

If you want to quit a repeat sequence, you can use `break()` function.
Aiming for a similar appearance with C and Java,
you can call `break()` without any arguments.

    repeat (10) {|i|
        // any process
        if (i == 5) {
            break
        }
        // not evaluated when break() is called
    }

The function `break()` takes an argument of any type
that affects a result value of the repeat.
When `break()` is called without an argument,
the repeat's result doesn't contain a value of the last loop.

    x = repeat (10):list {|i|
        if (i == 5) {
            break
        }
        i
    }
    // x is [0, 1, 2, 3, 4]

If you call `break()` with a valid argument, that will be included in the repeat's result.

    x = repeat (10):list {|i|
        if (i == 5) {
            break(99)
        }
        i
    }
    // x is [0, 1, 2, 3, 4, 99]

If you need to go to the next loop after skipping remaining procedure,
you can use `continue()` function.
As with the function `break`, you can call it without arguments.

    repeat (10) {|i|
        // any process
        if (i % 2 == 0) {
            continue
        }
        // not evaluated when continue() is called
    }

When you call `continue()` with no argument,
the repeat's result doesn't contain a value of that loop.

    x = repeat (10):list {|i|
        if (i % 2 == 0) {
            continue
        }
        i
    }
    // x is [1, 3, 5, 7, 9]

If you call `continue()` with a valid argument, that will be included in the repeat's result.

    x = repeat (10):list {|i|
        if (i % 2 == 0) {
            continue(99)
        }
        i
    }
    // x is [99, 1, 99, 3, 99, 5, 99, 7, 99, 9]


### {{ page.chapter }}.2.5. Generate Iterator

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


