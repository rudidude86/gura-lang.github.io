---
layout: page
lang: en
title: String Operation
chapter: 12
---

# Chapter {{ page.chapter }}. {{ page.title }}

## {{ page.chapter }}.1. Overview

A string is a sequence of character codes in UTF-8 format
and is represented by `string` class that has a variety of operations on strings.
Among them, there's no operation that has side effects on `string` instance,
which leads to the following rules.

* It's not allowed to edit each character in a string content through index access.
* Modification methods are supposed to return a new `string` instance with modified result.

While the interpreter itself provides fundamental operations for strings,
importing module named `re` expand the capability so that it can process regular expressions.


## {{ page.chapter }}.2. Basic Operation


### {{ page.chapter }}.2.1. Character Access and Splitting

The most common way to create a `string` instance is to specify a string literal.

    str = 'The quick brown fox jumps over the lazy dog'

You can specify an index number embraced by a pair of square brackets
to retrieve characters as sub strings at the specified position.

    str[16]  // returns 'f'
    str[17]  // returns 'o'
    str[18]  // returns 'x'

You can also specify a list of indexing items, numbers or iterators,
to get a list of sub strings. These items can be mixed together.

    str[16, 17, 18]   // returns ['f', 'o', 'x']
    str[10..14]       // returns ['b', 'r', 'o', 'w', 'n']
    str[4..8, 35..38] // returns ['q', 'u', 'i', 'c', 'k', 'l', 'a', 'z', 'y']

If you specify an infinite iterator as an indexing item,
you would get sub strings within an available range.

    str[35..]       // returns ['l', 'a', 'z', 'y', ' ', 'd', 'o', 'g']

To see the length of a string, `string#len()` is available.

    n = str.len()
    // n is 43

A method `string#each()` creates an iterator that returns each character as a sub string.

    x = str.each()
    // x is an iterator that returns 'T', 'h', 'e' ...

A call of `string#each()` with attribute `:utf8` or `:utf32` would create an iterator
that returns character code numbers in UTF-8 or UTF-32 instead of sub strings.

    x = str.each():utf8
    // x is an iterator that returns 84, 104, 101, ...

    x = str.each():utf32
    // x is an iterator that returns 84, 104, 101, ...

A method `string#eachline()` creates an iterator that splits a string by a newline character
and returns strings of each line.

    str = R'''
    1st
    2nd
    3rd
    '''
    x = str.eachline()
    // x is an iterator that returns '1st\n', '2nd\n' and '3rd\n'

A method `string#split()` creates an iterator that splits a string
by a separator string specified in the argument.

    str = 'The quick brown fox jumps over the lazy dog'
    x = str.split(' ')
    // x is an iterator that returns 'The', 'quick', 'brown', 'fox' ...

If you want to split a string into segments with the same length,
use `string#fold()` method.

    str = 'abcdefghijklmnopqrstuvwxyz'
    x = str.fold(5)
    // x is an iterator that returns 'abcde', 'fghij', 'klmno', 'pqrst' ...


### {{ page.chapter }}.2.2. Modification and Conversion


`string#chop()`


`string#eachline()`, `readlines()` `:chop`


`string#capitalize()`

`string#lower()`

`string#upper()`




`string#binary()` `binary`

`string#encode()` `binary`

`string#reader()` `stream`


`string#encodeuri()`

`string#decodeuri()`

`string#escapehtml()`

`string#unescapehtml()`

`string#zentohan()`


### {{ page.chapter }}.2.3. Extraction


`string#mid()`

`string#left()`

`string#right()`


### {{ page.chapter }}.2.4. Search, Replace and Inspection

`string#find()`

`string#replace()`

`string#startswith()`

`string#endswith()`


## {{ page.chapter }}.3. Formatter

C language's "printf"-like formatter is available.


## {{ page.chapter }}.4. Regular Expression

module `re`

`string#match()`

`string#scan()`

`string#splitreg()`

`string#sub()`

`re.match` class

`m[0]`

`m[1]`

