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


## {{ page.chapter }}.2. Basic Operation

The most common way to create a `string` instance is to specify a string literal.

    str = 'The quick brown fox jumps over the lazy dog'

You can specify an index number embraced by a pair of square brackets
to retrievet sub strings at the specified position.

    str[16]  // returns 'f'
    str[17]  // returns 'o'
    str[18]  // returns 'x'

You can also specify multiple index numbers to get a list of sub strings.

    str[16, 17, 18] // returns ['f', 'o', 'x']



    str[10..14]     // returns ['b', 'r', 'o', 'w', 'n']

    str[35..]       // returns ['l', 'a', 'z', 'y', ' ', 'd', 'o', 'g']



    str.each()
    str.each():utf8
    str.each():utf32

    str.eachline()

    str.fold()
    
    str.split()

`string#len()`

converter:

`string#binary()`

`string#reader()`

`string#encode()`

`string#encodeuri()`

`string#escapehtml()`

`string#unescapehtml()`

`string#zentohan()`


extraction:

`string#mid()`

`string#left()`

`string#right()`


search:

`string#find()`

inspection:

`string#startswith()`

`string#endswith()`

modification:

`string#chop()`

`string#capitalize()`

`string#lower()`

`string#upper()`

`string#replace()`



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

