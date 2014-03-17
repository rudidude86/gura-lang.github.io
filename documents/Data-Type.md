---
layout: page
lang: en
title: Data Type
chapter: 3
---

# {{ page.chapter }}. {{ page.title }}

## {{ page.chapter }}.1. About Data Type

A value has a corresponding Data Type that defines its behavior and properties.

Each Data Type is bound with a type name,
which usually appears in argument list of function call.

Name spaces for Data Type are completely isolated
from those for variable and function names.

As each Data Type has a one-to-one relationship with a corresponding Class,
those terms have almost the same meaning within documents in many cases.

Data types are categorized into two types:
**Primitive Data Type** and **Object Data Type**.

A value of Primitive Data Type holds its content in as small memory as possible.
It doesn't include any Environment in it and doesn't have any methods with side effects.
Among them are `nil`, `boolean`, `complex`, `number`, `rational`,
`string` and `symbol` types.

A value of Object Data Type owns Object data that is a sort of Environment,
which allows operations with side effects.
Most Data Types except for what are picked up as Primitive Data Types above
belong to this.


## {{ page.chapter }}.2. Frequently Used Data Types

Below is a list of some Data Types that often appear in documents,
which also shows one of the typical ways to instantiate values of each type.

* `nil`

  This is a Primitive Data Type.

  A value of `nil` type is used to indicate an invalid result or status.
  It is often used as a returned value of a function when it fails its expected work.
  A variable `nil` has a value of nil type.

        nil

  Since `nil is the only instance of `nil type,
  the term `nil can both mean the name of the value and its type.

* `boolean`

  This is a Primitive Data Type.
 
  Values of `boolean` type are used to determine
  whether something is in a true or a false state.
  Variables named `true` and `false` are assigned
  with a true value and a false value respectively.

        true  false

  In a function like `if` having arguments to check true/false condition
  and in a logical calculation,
  `false` and `nil` only are determined as a false state
  while other values are treated as a true state.
  Note that a zero value of `number` type is recognized as a true, not a false.

* `number`

  This is a Primitive Data Type.

  A number literal without any suffix instantiates a value of `number` type.

        3.14  1000  1e3  0xaabb

* `string`

  This is a Primitive Data Type.

  A string literal without any suffix instantiates a value of `string` type.

        'hello world'
        
        R'''
        message text
        '''

* `symbol`

  This is a Primitive Data Type.

  An identifier preceded by a back quote instantiates a value of `symbol` type.

        `foo  `bar

* `expr`

  This is an Object Data Type.

  Any expression preceded by a back quote instantiates a value of `expr` type.

        `(x + y)  `func(x)  `{ println('hello'), x += 1 }

* `iterator`

  This is an Object Data Type.

  If one or more elements are surrounced by a pair of parentheses,
  it would instantiate a value of `iterator` type.
  Any type of value can be an element of iterators.

        (3, 1, 4, 1, 5, 9)
        
        ('hello', 'world', 3, 4, 5)

  To create an iterator that contains only one element,
  be sure to put a comma afther the element like following:

        (3,)

  An expression `(3)` is recognized as an ordinary value of number `3`.

  See chapter [List and Iterator](List-and-Iterator.html) for more detail.

* `list`

  This is an Object Data Type.

  If one or more elements are surrounced by a pair of square brackets,
  it would instantiate a value of `list` type.
  Any type of value can be an element of lists.

        [3, 1, 4, 1, 5, 9]
        
        ['hello', 'world', 3, 4, 5]

  See chapter [List and Iterator](List-and-Iterator.html) for more detail.

* `dict`

  This is an Object Data Type.

  `dict` is a dictionary that contains key-value pairs as its elements
  where a key is one of `number`, `string` or `symbol` and a value is of any type.

        %{
            `symbol1 => 'value 1'
            `symbol2 => 'value 2'
            `symbol3 => 'value 3'
        }

  See chapter [Dictionary](Dictionary.html) for more detail.

* `complex`

  This is a Primitive Data Type.

  A number literal suffixed by `j` instantiates a value of `complex` type
  that represents a complex number.

        3.14j  1000j  1e3j

  See chapter [Mathematic Functions](Mathematic-Functions.html) for more detail.

* `rational`

  This is a Primitive Data Type.

  A number literal suffixed by `r` instantiates a value of `rational` type
  that represents a rational number.

        3r  123r

  See chapter [Mathematic Functions](Mathematic-Functions.html) for more detail.

* `binary`

  This is an Object Data Type.

  A string literal preceded by `b` instantiates a value of `binary` type.
  
        b'\x00\x01\0x02\0x03'
