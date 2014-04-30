---
layout: page
lang: en
title: Iterator/List Operation
chapter: 13
---

# Chapter {{ page.chapter }}. {{ page.title }}

## {{ page.chapter }}.1. Overview

An iterator and a list are quite similar in terms of
handling multiple values in a flat structure.
In fact, many of their methods share the same names and functions each other.

The difference is that a list is a container that actually owns its element values
while an iterator only provides a method that retrieves a "next" value of a sequence
and doesn't necessarily have to own values.
This feature leads to the following principles:

* An iterator can handle a sequence of data that continues indefinitely
  because it doesn't need to keep all the values in it.
* An iterator consumes less memory than a list in many cases.
* A list provides an indexing method that enables random access for its elements.
* A list provides methods to append or remove values.

Note that Gura makes it a rule to implement most functions to return an iterator by default
if they have multiple values as its result.
Even with such functions, you can easily get a list as their result
by calling it with `:list` attribute.


## {{ page.chapter }}.2. Iteration on Iterators and Lists

There are several ways to iterate elements in an iterator or a list.
In this section, consider a task to print elements in the list shown below:

    words = ['one', 'two', 'three', 'four', 'five', 'six', 'seven', 'eight', 'nine', 'ten']

As you've already seen a previous chapter,
iterators and lists can work with functions, methods and operators through Implicit Mapping.
You can simply call `printf()` function with iterators or lists
that causes a repetitive evaluation of the function.

    printf('%s\n', words)

Since Implicit Mapping would iterate each element if a function takes more than one iterables,
you can specify an iterator that generates numbers starting from zero
to print indexing numbers along with the words.

    printf('%d: %s\n', 0.., words)

Using `for()` function, you can iterate a list or an iterator
in a way that you may have been familiar with in other languages.

    for (word in words) {
        printf('%s\n', word)
    }

You can get a loop index starting from zero by specifying a block parameter.

    for (word in words) {|i|
        printf('%d: %s\n', i, word)
    }

Other than `for()` function,
you can also use `iterator#each()` or `list#each()` method to iterate elements on them.

    words.each {|word|
        printf('%s\n', word)
    }

In this case, the block parameter contains an iterated element as its first value.
It provides a loop index as the second value as below.

    words.each {|word, i|
        printf('%d: %s\n', i, word)
    }

Most functions and methods that return an iterator as their result
are designed to iterate elements when they take a block.
Consider methods `iterator#filter()` and `list#filter()`,
which returns an iterator that pick up elements satisfying a criteria specified in the argument.
Following is a code that prints words beginning with 't'.

    words.filter(&{$word.startswith('t')}) {|word, i|
        printf('%d: %s\n', i, word)
    }

The result comes as below:

    0: two
    1: three
    2: ten


## {{ page.chapter }}.3. Iterator-specific Manipulation

### {{ page.chapter }}.3.1. Finite Iterator vs. Infinite Iterator

Iterators that generate a limited numer of elements are called Finite Iterator.
An iterator `0..5` is a representative one that you can know in advance would generate 6 elements.
It's possible that you convert a Finite Iterator into a list.

Iterators that generate elements indefinitely
or couldn't predict when elements drain out are called Infinite Iterator.
Among them, there's an iterator `0..` that generates numbers starting from 0 and increasing for ever.
It would occur an error if you try to convert Infinite Iterator into a list.

You can use method `iterator#isinfinite()` to check if an iterator is an infinite one or not.

    (0..5).isinfinite()  // returns false
    (0..).isinfinite()   // returns true

Some functions may possibly create Finite or Infinite Iterator depending on their arguments.
Function `rands()` specify how many random values it should generate with its second argument,
and it would generate values without end if the argument is omitted.

    rands(100)     // returns an Infinite Iterator
    rands(100, 80) // returns a Finite Iterator that is expected to generate 80 elements

Infinity of the result of function `readlines()` depends on the status of the source stream:
it would be an Infinite Iterator if the stream is infinite
while it would be a Finite Iterator for a finite stream.

An iterator's infinity may be derived from one to another.
This happens with iterators that are designed to manipulate values
after retrieving them from other source iterator.
For example, method `iterator#filter()` returns an iterator that picks up elements
from values in the target iterator. In the following code, `y` is a Finite Iterator
that generates numbers 0, 2, 4, 6, 8 and 10.

    x = 0..10
    y = x.filter(&{$n % 2 == 0})

If the source iterator is infinite, the result iterator will be infinite too.
In the code below, `y` is an Infinite Iterator that generates even numbers indefinitely.

    x = 0..
    y = x.filter(&{$n % 2 == 0})


### {{ page.chapter }}.3.2. Operation on Elements


`iterator#next()`

iterator to list: `[x]`, `x.each():list`

    x.each {|i|
        
    }

## {{ page.chapter }}.4. List-specific Manipulation

### {{ page.chapter }}.4.1. Random Access in List

You can specify an index number starting from zero embraced by a pair of square brackets
to retrieve an element at the specified position.
Multiple numbers for indexing can also be specified to get a list of elements.

    tbl = ['zero', 'one', 'two', 'three', 'four', 'five', 'six', 'seven']
    tbl[2]        // returns 'two'
    tbl[4]        // returns 'four'
    tbl[1, 3, 5]  // returns ['one', 'three', 'five']

You can also specify iterators and lists to get a list of elements.
Numbers and iterators can be mixed together as indexing items.

    tbl = ['zero', 'one', 'two', 'three', 'four', 'five', 'six', 'seven']
    tbl[2..4]        // returns ['two', 'three', 'four']
    tbl[1..3, 5..7]  // returns ['one', 'two', 'three', 'five', 'six', 'seven']

If you specify an infinite iterator as an indexing item,
you would get elements within an available range.

    tbl = ['zero', 'one', 'two', 'three', 'four', 'five', 'six', 'seven']
    tbl[5..]        // returns ['five', 'six', 'seven']

An index with a negative number points the position from the bottom,
where `-1` is the last position.

    tbl = ['zero', 'one', 'two', 'three', 'four', 'five', 'six', 'seven']
    tbl[-1]         // returns 'seven'
    tbl[-2]         // returns 'six'

Method `list#first()` returns the first item in the list
and method `list#last()` the last item.
These have the same effect with index accesses by numbers 0 and -1 respectively.

    tbl = ['zero', 'one', 'two', 'three', 'four', 'five', 'six', 'seven']
    tbl.first()     // returns 'zero'
    tbl.last()      // returns 'seven'

You can use method `list#get()` for index access,
which would be useful when used with Member Mapping.

    tbl = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
    tbl::get(0)     // returns [1, 4, 7]


list to iterator: `list#each()`


### {{ page.chapter }}.4.2. Element Modification

`list#add()`

`list#append()`

`list#clear()`

`list#erase()`

`list#shift()`


## {{ page.chapter }}.5. Operation Methods

### {{ page.chapter }}.5.1. Inspecting and Reducing

`list#isempty()`

`list#len()`, `iterator#len()`

`list#count()`, `iterator#count()`

`list#and()`, `iterator#and()`

`list#or()`, `iterator#or()`

`list#average()`, `iterator#average()`

`list#contains()`, `iterator#contains()`

`list#join()`, `iterator#join()`

`list#joinb()`, `iterator#joinb()`

`list#max()`, `iterator#max()`

`list#min()`, `iterator#min()`

`list#reduce()`, `iterator#reduce()`

`list#stddev()`, `iterator#stddev()`

`list#sum()`, `iterator#sum()`

`list#variance()`, `iterator#variance()`


### {{ page.chapter }}.5.2. Mapping Method

`list#map()`, `iterator#map()`

`list#nilto()`, `iterator#nilto()`

`list#rank()`, `iterator#rank()`

`list#replace()`, `iterator#replace()`


### {{ page.chapter }}.5.3. Element Manipulation

`list#align()`, `iterator#align()`

`list#cycle()`, `iterator#cycle()`

`list#filter()`, `iteraotr#filter()`

`list#find()`, `iterator#find()`

`list#fold()`, `iterator#fold()`

`list#head()`, `iterator#head()`

`list#offset()`, `iterator#offset()`

`list#pingpong()`, `iterator#pingpong()`

`list#reverse()`, `iterator#reverse()`

`list#runlength()`, `iterator#runlength()`

`list#since()`, `iterator#since()`

`list#skip()`, `iterator#skip()`

`list#skipnil()`, `iterator#skipnil()`

`list#sort()`, `iterator#sort()`

`list#tail()`, `iterator#tail()`

`list#while()`, `iterator#while()`


## {{ page.chapter }}.6. Iterator Generation

`iterator.range()`

`iterator.interval()`

`iterator.consts()`

`iterator.rands()`


`list#combination()`

`list#permutation()`

`list#shuffle()`


list generation

`list.zip()`

`list#flat()`




