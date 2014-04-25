---
layout: page
lang: en
title: Iterator/List Operation
chapter: 13
---

# Chapter {{ page.chapter }}. {{ page.title }}

## {{ page.chapter }}.1. Overview

`list`

Using `iterator`, you can realize what other languages call "infinite list."


### {{ page.chapter }}.2. List-specific Manipulation

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


## {{ page.chapter }}.3. Iterator-specific Manipulation

Finite Iterator vs. Infinite Iterator

`0..5`

`0..`

`iterator.rands(10)`

`iterator.rands()`

`readlines()`'s infinity depends on the source stream

`iterator#isinfinite()`

`iterator#next()`


## {{ page.chapter }}.4. Conversion between Iterator and List

`:list` attribute

list to iterator: `list#each()`

iterator to list: `[` &hellip; `]`



## {{ page.chapter }}.5. Operation Methods

`list#each()`, `iterator#each()`

inspecting and reducing method:

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

mapping method:

`list#map()`, `iterator#map()`

`list#nilto()`, `iterator#nilto()`

`list#rank()`, `iterator#rank()`

`list#replace()`, `iterator#replace()`


element manipulation:


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

destructive methods:

`list#add()`

`list#append()`

`list#clear()`

`list#erase()`

`list#shift()`



