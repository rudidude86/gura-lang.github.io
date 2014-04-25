---
layout: page
lang: en
title: Iterator/List Operation
chapter: 13
---

# Chapter {{ page.chapter }}. {{ page.title }}

## {{ page.chapter }}.1. Overview

`list`

`iterator`

## {{ page.chapter }}.2. Finite Iterator vs. Infinite Iterator

`0..5`

`0..`

`iterator.rands(10)`

`iterator.rands()`

`readlines()`'s infinity depends on the source stream

`iterator#isinfinite()`


## {{ page.chapter }}.3. Conversion between Iterator and List

`:list` attribute

list to iterator: `list#each()`

iterator to list: `[` &hellip `]`


## {{ page.chapter }}.4. Element Look-up


`list#each()`, `iterator#each()`

`list#first()`

`list#last()`

`list#get()`


`iterator#next()`


## {{ page.chapter }}.5. Operation Methods


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



