---
layout: page
lang: en
title: Data Type
---

{{ page.title }}
----------------

### About Data Type

Each Data Type is assigned with a type name,
which often appears in argument list of function call.

Name spaces for Data Type is completely isolated
from those for other resources like variable.

As each Data Type has a one-to-one relationship with a Class,
those terms have almost the same meaning within a context in many cases.


### List of Data Types

Below is a list of some Data Types that often appear in documents.

* `nil`

  A value of `nil` type is used to indicate an invalid result or status.
  It is often used as a returned value of a function when it fails its expected work.
  A variable `nil` has a value of nil type.

* `boolean`

  Values of `boolean` type are used to determine
  whether something is in a true or a false state.
  Variables named `true` and `false` are assigned
  with a true value and a false value respectively.

  In a conditional part of `if` function and in a logical calculation,
  `false` and `nil` only are determined as a false state
  while other values are treated as a true state.
  Note that a zero value of `number` type is recognized as a true, not a false.

* `complex`

  A number literal suffixed by `j` creates a value of `complex` type
  that represents complex numbers.

        3.14j  1000j  1e3j

* `number`

  A number literal without any suffix creates a value of `number` type.

        3.14  1000  1e3  0xaabb

* `rational`

  A number literal suffixed by `r` created a value of `rational` type
  that represents rational numbers.

        3r  123r

* `string`

  A string literal without any suffix creates a value of `string` type.

        'hello world'
        
        R'''
        message text
        '''

* `symbol`

  An identifier preceded by a back quote creates a value of `symbol` type.

        `foo  `bar

* `binary`

  A string literal preceded by `b` creates a value of `binary` type.
  
        b'\x00\x01\0x02\0x03'

* `iterator`

  If elements are surrounced by a pair of parentheses,
  it would create a value of `iterator` type.
  Any type of values are stored in it as elements.

        (3, 1, 4, 1, 5, 9)
        ('hello', 'world', 3, 4, 5)

* `list`

  If elements are surrounced by a pair of square brackets,
  it would create a value of `list` type.
  Any type of values are stored in it as elements.

        [3, 1, 4, 1, 5, 9]
        ['hello', 'world', 3, 4, 5]
