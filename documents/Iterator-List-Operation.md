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

Consider a task that prints elements in the list shown below:

    words = ['one', 'two', 'three', 'four', 'five', 'six', 'seven', 'eight', 'nine', 'ten']

There are several ways to iterate elements in an iterator or a list.

* As you've already seen a previous chapter,
  iterators and lists can work with functions, methods and operators through Implicit Mapping.
  You can simply call `printf()` function with iterators or lists
  that causes a repetitive evaluation of the function.

        printf('%s\n', words)

  A function with Implicit Mapping is capable of iterating multiple iterables provided as its arguments.
  In addition to the list of words, you can specify an iterator
  that generates numbers starting from zero to print indexing numbers as shown below.

        printf('%d: %s\n', 0.., words)

* Using `for()` function, you can iterate a list or an iterator
  in a way that you may have been familiar with in other languages.

        for (word in words) {
            printf('%s\n', word)
        }

  You can get a loop index starting from zero by specifying a block parameter.

        for (word in words) {|i|
            printf('%d: %s\n', i, word)
        }

* You can also use method `iterator#each()` or `list#each()` to iterate elements on them.
  In this case, the block parameter contains an iterated element as its first value.

        words.each {|word|
            printf('%s\n', word)
        }
  
  It provides a loop index as the second value in the block parameters as below.

        words.each {|word, i|
            printf('%d: %s\n', i, word)
        }

Most functions and methods that return an iterator as their result
are designed to iterate elements when they take a block.
Actually, methods `iterator#each()` and `list#each()`, which are mentioned above,
simply return an iterator when they're called without a block.

    x = words.each()
    // x is an iterator that iterates each element in words

To see other examples that have the same feature,
consider methods `iterator#filter()` and `list#filter()`,
which returns an iterator that pick up elements satisfying a criteria specified in the argument.

    x = words.filter(&{$word.startswith('t')})
    // x is an iterator that generates 'two', 'three' and 'ten'

Specifying a block with the method would repetitively evaluate it
while iterating elements of the result.

    words.filter(&{$word.startswith('t')}) {|word, i|
        printf('%d: %s\n', i, word)
    }

The result comes as below:

    0: two
    1: three
    2: ten


## {{ page.chapter }}.3. Iterator-specific Manipulation

### {{ page.chapter }}.3.1. About This Section

This section explains about methods and ohter manipulation that are specific to iterators.


### {{ page.chapter }}.3.2. Finite Iterator vs. Infinite Iterator

Iterators that generate a limited numer of elements are called Finite Iterator.
An iterator `0..5` is a representative one that is definitely expected to generate 6 elements.
It's possible that you convert a Finite Iterator into a list.

Iterators that generate elements indefinitely
or couldn't predict when elements drain out are called Infinite Iterator.
Among them, there's an iterator `0..` that generates numbers starting from 0 and increasing for ever.
It would occur an error if you try to convert Infinite Iterator into a list.

You can use method `iterator#isinfinite()` to check if an iterator is an infinite one or not.

    (0..5).isinfinite()  // returns false
    (0..).isinfinite()   // returns true

Some functions may possibly create either Finite or Infinite Iterator depending on their arguments.
The second argument in function `rands()` specify how many random values it should generate,
and, if omitted, the function would generate values without end.

    rands(100)     // returns an Infinite Iterator
    rands(100, 80) // returns a Finite Iterator that is expected to generate 80 elements

Infinity of the result of function `readlines()` depends on the attribute of the source stream:
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
    // y is finite

If the source iterator is infinite, the result iterator will be infinite too.
In the code below, `y` is an Infinite Iterator that generates even numbers indefinitely.

    x = 0..
    y = x.filter(&{$n % 2 == 0})
    // y is infinite


### {{ page.chapter }}.3.3. Conversion into List

Embracing iterators with a pair of square brackets would make a list from them.

    [0..5]               // creates [0, 1, 2, 3, 4, 5]

You can specify any numbers of iterators in it as below.

    [0..2, 5..7, 8..10]  // creates [0, 1, 2, 5, 6, 7, 8, 9, 10]

It would occur an error if you try to create a list from Infinite Iterators.

    [0..]                // error!

Another way to create a list from an iterator is to use `iterator#each()` method with `:list` attribute.

    x = 0..5
    x.each():list        // returns [0, 1, 2, 3, 4, 5]


### {{ page.chapter }}.3.4. Operation on Elements

You can retrieve elements from an iterator by using method `iterator#next()`.

    x = 0..5
    x.next()   // returns 0
    x.next()   // returns 1
    x.next()   // returns 2


## {{ page.chapter }}.4. List-specific Manipulation

### {{ page.chapter }}.4.1. About This Section

This section explains about methods and ohter manipulation that are specific to lists.


### {{ page.chapter }}.4.2. Indexing Read from List

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


### {{ page.chapter }}.4.3. Indexing Modification on List

An assignment to elements in a list through indexing access is also available.

If an indexing item is a single number, the element at the specified position will be modified.

    tbl = ['zero', 'one', 'two', 'three', 'four', 'five', 'six', 'seven']
    tbl[2] = '2'
    tbl[4] = '4'
    // tbl is ['zero', 'one', '2', 'three', '4', 'five', 'six', 'seven']

Multiple numbers can also be specified for indexing.
In this case, if the assigned value is an iterable,
each element in the iterable will be stored at the specified positions in the target list.

    tbl = ['zero', 'one', 'two', 'three', 'four', 'five', 'six', 'seven']
    tbl[1, 3, 5] = ['1', '3', '5']
    // tbl is ['zero', '1', 'two', '3', 'four', '5', 'six', 'seven']

If the assigned value is a scholar, the same value is stored at the positions.

    tbl = ['zero', 'one', 'two', 'three', 'four', 'five', 'six', 'seven']
    tbl[1, 3, 5] = '1'
    // tbl is ['zero', '1', 'two', '1', 'four', '1', 'six', 'seven']

You can also specify an iterator as indexing item.

    tbl = ['zero', 'one', 'two', 'three', 'four', 'five', 'six', 'seven']
    tbl[1..3, 5..7] = ['1', '2', '3', '5', '6', '7']
    // tbl is ['zero', '1', '2', '3', 'four', '5', '6', '7']

When you specify an Infinite Iterator for an indexing item,
all the elements in the assigned iterable are stored at the specified position.

    tbl = ['zero', 'one', 'two', 'three', 'four', 'five', 'six', 'seven']
    tbl[5..] = ['5', '6']
    // tbl is ['zero', 'one', 'two', 'three', 'four', '5', '6', 'seven']

Negative number can also be specified for indexing.

    tbl = ['zero', 'one', 'two', 'three', 'four', 'five', 'six', 'seven']
    tbl[-1] = '7'
    tbl[-2] = '6'
    // tbl is ['zero', 'one', 'two', 'three', 'four', 'five', '6', '7']


### {{ page.chapter }}.4.4. Conversion into Iterator

Method `list#each()` returns an iterator that generates values based on the list's elements.

    tbl = ['one', 'two', 'three', 'four']
    x = tbl.each()
    // x is an iterator that generates 'one', 'two', 'three' and 'four'.


### {{ page.chapter }}.4.5. Operation on Elements

Method `list#isempty()` will check if a list is empty or not.

    tbl = []
    tbl.isempty()    // returns true

Both of methods `list#add()` and `list#append()` will add values to the target list.
They have the same behavior when they try to add a scholar value.
Below is a sample of `list#add()`:

    tbl = ['one', 'two', 'three']
    tbl.add('four')
    // tbl is ['one', 'two', 'three', 'four']

And a sample of `list#append()` is shown below:

    tbl = ['one', 'two', 'three']
    tbl.append('four')
    // tbl is ['one', 'two', 'three', 'four']

They have different results when they're given with a list as an element to add.
Method `list#add()` adds the list itself to the target list as one of its elements.

    tbl = ['one', 'two', 'three']
    tbl.add(['four', 'five', 'six'])
    // tbl is ['one', 'two', 'three', ['four', 'five', 'six']]

Method `list#append()` adds each of the list's element to the target list.

    tbl = ['one', 'two', 'three']
    tbl.append(['four', 'five', 'six'])
    // tbl is ['one', 'two', 'three', 'four', 'five', 'six']

Method `list#clear()` will create all the contet of the target list.

    tbl = ['one', 'two', 'three']
    tbl.clear()
    // tbl is []

Method `list#erase()` will erase elements at positions specified by its arguments.
You can specify multiple indices at which elements are erased.

    tbl = ['zero', 'one', 'two', 'three', 'four', 'five', 'six', 'seven']
    tbl.erase(2, 4, 6)
    // tbl is ['zero', 'one', 'three', 'five', 'seven']

Method `list#shift()` erase the first element before it returns the value.

    tbl = ['one', 'two', 'three']
    x = tbl.shift()  // returns 'one'
    // tbl is ['two', 'three']


## {{ page.chapter }}.5. Common Manipulation for Iterator and List

### {{ page.chapter }}.5.1. About This Section

This section explains about methods and ohter manipulation that can commonly be applied to iterators and lists.
Here, for simple descriptions, a pseudo class name `iterable` is used to represent `list` or `iterator` class.


### {{ page.chapter }}.5.2. Inspecting and Reducing

Methods `iterable#len()` return the number of elements in the iterable.

`iterable#count()`
`iterable#contains()`

`iterable#and()`
`iterable#or()`

`iterable#average()`
`iterable#max()`
`iterable#min()`
`iterable#stddev()`
`iterable#sum()`
`iterable#variance()`


`iterable#join()`
`iterable#joinb()`

`iterable#reduce()`


### {{ page.chapter }}.5.3. Mapping Method

`iterable#map()`

`iterable#nilto()`

`iterable#rank()`

`iterable#replace()`


### {{ page.chapter }}.5.4. Element Manipulation

`iterable#align()`

`iterable#cycle()`

`iterable#filter()`

`iterable#find()`

`iterable#fold()`

`iterable#head()`

`iterable#offset()`

`iterable#pingpong()`

`iterable#reverse()`

`iterable#runlength()`

`iterable#since()`

`iterable#skip()`

`iterable#skipnil()`

`iterable#sort()`

`iterable#tail()`

`iterable#while()`


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




