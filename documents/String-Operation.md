---
layout: page
lang: en
title: String Operation
chapter: 12
---

# Chapter {{ page.chapter }}. {{ page.title }}

## {{ page.chapter }}.1. Basic Operation

string has no operations with side effects

* modification method will return a new instance of string with modified result
* assignment to each character through index access is not permitted

some operations:

    str = 'The quick brown fox jumps over the lazy dog'

    str[16]  // 'f'
    str[17]  // 'o'
    str[18]  // 'x'

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



## {{ page.chapter }}.2. Regular Expression

module `re`

`string#match()`

`string#scan()`

`string#splitreg()`

`string#sub()`

`re.match` class

`m[0]`

`m[1]`

