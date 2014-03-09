---
layout: page
lang: en
title: Syntax
---

{{ page.title }}
----------------

### Number Literal

A decimal number is the most common number literal.

    0 1234 999999

A floating-point number that sometimes comes with an exponential expression is also acceptable.

    3.14  10.  .001  1e100  3.14e-10  0e0

A sequence of characters that starts with `0b` or `0B` and contains `0` or `1`
represents a binary number.

    0b01010101

A sequence of characters that starts with `0` and contains digit characters between `0` and `7`
represents a octal number.

    01234567

A sequence of characters that starts with `0x` or `0X` and contains digit characters and
alphabet characters between `a` and `f` or between `A` and `F`
represents a hexadecimal number.

    0x7feaa00
    0x7FEAA00

A suffix symbol can be appended after a number literal
to convert it into other types rather than `number`.
Two suffix symbols are available as standard.

<table>
<tr><th>Suffix Symbol</th><th>Function</th></tr>
<tr><td><code>j</code></td><td>Converts into <code>complex</code> type.
<code>3j</code> is equivalent with <code>complex(0, 3)</code></td></tr>
<tr><td><code>r</code></td><td>Converts into <code>rational</code> type.
<code>3r</code> is equivalent with <code>rational(0, 3)</code></td></tr>
</table>

Importing modules may add other suffix symbols.
For instance, importing a module named `gmp`, which calculates numbers in arbitrary precision,
would add a suffix `L` that represents such numbers.

You can also add your own suffix symbols by using Suffix Manager
that is responsible for managing suffix symbols and their associated functions.


### String Literal

A string literal is a sequence of characters surrounded
by a pair of single or double quotations.
A string surrounded by single quotations can contain double quotation characters in its body
while a string with double quotations can have single quotation characters inside.

    'Hello "World"'
    "Hello 'World'"

Although you can choose one of them case by case,
single quotation is more preferable in general.

Within a string literal, you can use following escape characters.

<table>
<tr><th>Escape Character</th><th>Note</th></tr>
<tr><td><code>\\</code></td><td>back slash</td></tr>
<tr><td><code>\'</code></td><td>single quotation</td></tr>
<tr><td><code>\"</code></td><td>double quotation</td></tr>
<tr><td><code>\a</code></td><td>bell</td></tr>
<tr><td><code>\b</code></td><td>back space</td></tr>
<tr><td><code>\f</code></td><td>page feed</td></tr>
<tr><td><code>\r</code></td><td>carriage return</td></tr>
<tr><td><code>\n</code></td><td>line feed</td></tr>
<tr><td><code>\t</code></td><td>tab</td></tr>
<tr><td><code>\v</code></td><td>vertical tab</td></tr>
<tr><td><code>\0</code></td><td>null character</td></tr>
<tr><td><code>\x<em>hh</em></code></td><td>any byte of character code <code><em>hh</em></code> in hexadecimal</td></tr>
</table>

If a string is prefixed by `r`, a back slash is treated as a normal character, not one for escaping.
This feature is convenient to describe a path name in Windows style
and a regular expression that often uses back slash as a metacharacter.

    r'C:\users\foo\bar.txt'
    r'(\w+) (\d+):(\d+):(\d)'



You can describe a string containing multiple lines
by surrounding it with a triple sequence of single or double quotations.

    '''
    ABCD
    EFGH
    IJKL
    '''
    
    """
    ABCD
    EFGH
    IJKL
    """

These codes are equivalent to an expression `'\nABCD\nEFGH\nIJKL\n'`,
which contains a line-feed character at the beginning.
If you want to eliminate the first line-feed,
you need to begin the string body right after the starting quotations
or put a back slash at that position followed by a line feed
since a back slash placed at end of a line results in an elimination of the tailing line feed.

    '''ABCD
    EFGH
    IJKL
    '''
    
    '''\
    ABCD
    EFGH
    IJKL
    '''

Both of the examples above have the same result `'ABCD\nEFGH\nIJKL\n'`.

You can also specify `r` prefix for the multi-lined string
so that it can contain back slash characters without escaping.
In this case, you cannot use the second example shown above
because a back slash doesn't work to eliminate a line feed.
For such a case, a prefix `R` is useful,
which eliminates a line feed that appears right after the starting quotation.

    R'''
    ABCD
    EFGH
    IJKL
    '''

This is parsed as `'ABCD\nEFGH\nIJKL\n'`.

The prefix `R` also removes indentation characters that appear at each line.

    if (flag) {
        print(R'''
        ABCD
        EFGH
        IJKL
        ''')
    }

Assuming that there are four spaces before the expression `print(R'''`,
the parser would remove four spaces at top of each line within the multi-lined string.
This feature helps you describe multi-lined strings in indentation blocks
without disarranging the appearance.

A string literal prefixed by `b` would be treated
as a sequence of binary data instead of character code.

A string literal can also be appended by a suffix symbol
that has been registered in suffix manager.
There's no built-in suffix for string literals.


### Identifier

An identifier starts with a UTF-8 leading byte or one of following characters:

    a b c d e f g h i j k l m n o p q r s t u v w x y z
    A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
    _ $ @

and is followed by UTF-8 leading or trailing byte or characters shown below:

    a b c d e f g h i j k l m n o p q r s t u v w x y z
    A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
    _ $ @
    0 1 2 3 4 5 6 7 8 9

### Group

    []
    ()

### Block

    {}

### Operator


unary operator
binary operator

    +, -, *, /

### Attribute

    :foo, :bar

### Member Selector

    ., ::, :*, :&

### Comment

    //, #, /*..*/
