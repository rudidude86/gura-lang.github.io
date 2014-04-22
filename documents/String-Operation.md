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

    str = 'The quick brown fox jumps over the lazy dog'
    str[16]  // returns 'f'
    str[17]  // returns 'o'
    str[18]  // returns 'x'

You can also specify a list of indexing items, numbers or iterators,
to get a list of sub strings. These items can be mixed together.

    str = 'The quick brown fox jumps over the lazy dog'
    str[16, 17, 18]   // returns ['f', 'o', 'x']
    str[10..14]       // returns ['b', 'r', 'o', 'w', 'n']
    str[4..8, 35..38] // returns ['q', 'u', 'i', 'c', 'k', 'l', 'a', 'z', 'y']

If you specify an infinite iterator as an indexing item,
you would get sub strings within an available range.

    str = 'The quick brown fox jumps over the lazy dog'
    str[35..]       // returns ['l', 'a', 'z', 'y', ' ', 'd', 'o', 'g']

To see the length of a string, `string#len()` is available.
Note that `string#len()` returns the number of characters, not the size in byte.

    str = 'The quick brown fox jumps over the lazy dog'
    n = str.len()
    // n is 43

A method `string#each()` creates an iterator that returns each character as a sub string.

    str = 'The quick brown fox jumps over the lazy dog'
    x = str.each()
    // x is an iterator that returns 'T', 'h', 'e' ...

A call of `string#each()` with attribute `:utf8` or `:utf32` would create an iterator
that returns character code numbers in UTF-8 or UTF-32 instead of sub strings.

    str = '日本語'
    x = str.each():utf8
    // x is an iterator that returns 0xe697a5, 0xe69cac and 0xe7aa9e

    x = str.each():utf32
    // x is an iterator that returns 0x65e5, 0x672c and 0x8a9e

A method `string#eachline()` creates an iterator that splits a string by a newline character
and returns strings of each line.

    str = R'''
    1st
    2nd
    3rd
    '''
    lines = str.eachline()
    // lines is an iterator that returns '1st\n', '2nd\n' and '3rd\n'

A method `string#chop()` is useful when you want to remove a newline character
appended at the bottom.

    x = str.eachline()
    lines = x:*chop()  // apply string#chop() to each value in x
    // lines is an iterator that returns '1st', '2nd' and '3rd'

A method `string#eachline()` and others that split a multi-lined text into strings of each line
like `readlines()` are equipped with an attribute `:chop`
that applies the same process as `string#chop()`.

    lines = str.eachline():chop
    // lines is an iterator that returns '1st', '2nd' and '3rd'

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

A method `string#capitalize()` returns a string with the top alphabet converted to uppper case.

    str = 'hello, WORLD'
    str.capitalize()  // returns 'Hello, WORLD'

Methods `string#upper()` and `string#lower()` return a string after converting
all the alphabet characters to upper and lower case respectively.

    str = 'hello, WORLD'
    str.upper()       // returns 'HELLO, WORLD'
    str.lower()       // returns 'hello, world'

A method `string#binary()` returns a `binary` instance
that contains a binary sequence of the string in UTF-8 format.

    str = '日本語'
    str..binary()  // returns a binary b'\xe6\x97\xa5\xe6\x9c\xac\xe8\xaa\x9e'

You can use `string#encode()` to get a binary sequence in other codec other than UTF-8.

    str = '日本語'
    str.encode('shift_jis')  // returns a b'\x93\xfa\x96\x7b\x8c\xea'

A method `string#reader()` returns a `stream` instance
that reads a binary sequence of the string in UTF-8 format.

    str = 'The quick brown fox jumps over the lazy dog'
    x = str.reader()
    // x is a stream instance for reading

A method `string#encodeuri()` converts characters that can not be described in URI
by a percent-encoding rule,
while a method `string#decodeuri()` converts such encoded string into normal characters.

A method `string#escapehtml()` escapes characters that can not be described in HTML
with character entities prefixed by an ampersand,
while a method `string#unescapehtml()`converts such escaped ones into normal characters.



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

