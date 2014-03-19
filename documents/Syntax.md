---
layout: page
lang: en
title: Syntax
chapter: 2
---

# {{ page.chapter }}. {{ page.title }}

## {{ page.chapter }}.1. Elements

This section explains about syntax elements in the script.

### {{ page.chapter }}.1.1. Symbol

A symbol is used as a name of variable, function, symbol, type name, attribute and suffix.

A symbol starts with a UTF-8 leading byte or one of following characters:

    a b c d e f g h i j k l m n o p q r s t u v w x y z
    A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
    _ $ @

and is followed by UTF-8 leading or trailing byte or characters shown below:

    a b c d e f g h i j k l m n o p q r s t u v w x y z
    A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
    _ $ @
    0 1 2 3 4 5 6 7 8 9

Here are some valid symbols:

    foo
    test_result
    $foo
    @bar@
    test_1_var

Special symbols:

    %
    
    +  *  ?  -


### {{ page.chapter }}.1.2. Number Literal

A decimal number is the most common number literal.

    0 1234 999999

A floating-point number that sometimes comes
with an exponential expression is also acceptable.

    3.14  10.  .001  1e100  3.14e-10  0e0

A sequence of characters that starts with `0b` or `0B` and contains `0` or `1`
represents a binary number.

    0b01010101

A sequence of characters that starts with `0` and contains digit characters between `0` and `7`
represents an octal number.

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
An expression <code>3j</code> is equivalent with <code>complex(0, 3)</code>.</td></tr>
<tr><td><code>r</code></td><td>Converts into <code>rational</code> type.
An expression <code>3r</code> is equivalent with <code>rational(3, 0)</code>.</td></tr>
</table>

Importing modules may add other suffix symbols.
For instance, importing a module named `gmp`, which calculates numbers in arbitrary precision,
would add a suffix `L` that represents numbers that may consist of many digits.

You can also add your own suffix symbols by using Suffix Manager
that is responsible for managing suffix symbols and their associated functions.


### {{ page.chapter }}.1.3. String Literal

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
This feature helps you describe multi-lined strings in indented blocks
without disarranging the appearance.

A string literal prefixed by `b` would be treated
as a sequence of binary data instead of character code.

A string literal can also be appended by a suffix symbol
that has been registered in Suffix Manager.
There's no built-in suffix for string literals.


### {{ page.chapter }}.1.4. Operator

An Operator takes one or two values as its inputs and returns a calculation result.
It's categorized in the following types:

* **Prefixed Unary Operator** takes an input value specified after it.

        +  -  ~  !

  An example code of a Prefixed Unary Operator comes like `+x`.

* **Suffixed Unary Operator** takes an input value specified before it.

        ?  ..

  An example code of a Suffixed Unary Operator comes like `x?`.

* **Binary Operator** takes two input values specified on both sides of them.

        +  -  *  /  %  **  ==  !=  >  <  >=  <=  <=>
        in  &  |  ^  <<  >>  ||  &&  ..  =>

  An example code of a Binary Operator comes like `x + y`.

See section [Operator](Operator.html) for more detail.


### {{ page.chapter }}.1.5. Collector

Multiple elements can be grouped by surronding them with a pair of brackets.
There are three types of brackets as listed below.

* __Square bracket__: `[a, b, c]`
  
  When it appears right after an element that has a value as a result of evaluation,
  it works as an indexer that allows indexing access in the preceding value.

        x[3]  foo['key']

  Otherwise, it forms a list of elements
  that is set to create a `list` instance after evaluation.

        [1, 2, 3, 4]

* __Parentheses__: `(a, b, c)`

  When it appears right after an element that has a value as a result of evaluation,
  it's used as an argument list to evaluate the preceding value as a callable.

        f(1, 2, 3)

  Otherwise, it forms a list of elements
  that is set to create an `iterator` instance after evaluation.

        (1, 2, 3, 4)

* __Curly bracket__: `{a, b, c}`
  
  It forms a list of expressions called Block.
  In general, a Block is used as a body for function assignment
  or provides a procedual part in calling a function.

       f() = { println('hello') }

* __Vertical Bar__: `|a, b, c|`

  This only appears right after opening bracket of Block and is called Block Parameter.
  
        repeat (3) {|i| println(i)}

Elements in a collector can be separated by a comma character or a line feed.
The following two codes have the same result.

    [1, 2, 3, 4]
    
    [1
    2
    3
    4
    ]


### {{ page.chapter }}.1.6. Attribute

A symbol preceded by a colon is called Attribute.

    :foo  :bar

Attributes appear after a variable identifier or an argument list for a callable.
They are used to customize the evaluation result of variables
and the behavior of functions.

More than one attributes can be appended by simply concatenating them like below.

    func():foo:bar


### {{ page.chapter }}.1.7. Symbol and Expression

A symbol preceded by a back quote creates an instance of `symbol` data type.

    `foo  `bar

Each values of `symbol` data type has a unique number that is assigned at parsing phase,
which enables quick identification between them.

Any other elements that has a back quote appended ahead is called an Expression
and creates an instance of `expr` data type.

    `(a + b)  `func()

As an Expression can hold any code without any evaluation,
it can be used to pass a procedure itself to a function as one of the arguments.


### {{ page.chapter }}.1.8. Comment

There are two types of comments: line comment and block comment.

A line comment begins with a marker `#` or `//` and lasts until end of the line.

    # this is a comment
    
    // and this is too
    
    x = 10 // comment after code

A block comment begins with a marker `/*` and ends with `*/`.
It can contain multiple lines and even other block comments nested
as long as pairs of the comment markers are matched.

Following are valid examples of block comment.

    /* block comment */
    
    /*
    block comment
    */
    
    /* /* /* nested comment */ */ */


## {{ page.chapter }}.2. Expression

Expressions are factors that construct a script.

In many cases, you don't need to be aware of them
since they're invisible from usual programs.
But, if necessary, you can refer to them through instances of `expr` class.


### {{ page.chapter }}.2.1. Hierarchy

The following figure shows a hierarchy of all the expression.

    Expr <-+- Value
           +- Identifier
           +- Suffixed
           +- Unary <-----+- UnaryOp
           |              `- Quote
           +- Binary <----+- BinaryOp
           |              +- Assign
           |              `- Member
           +- Collector <-+- Lister
           |              +- Iterer
           |              +- Block
           |              `- Root
           `- Compound <--+- Indexer
                          `- Caller


### {{ page.chapter }}.2.2. Simple Expression

* A `Value` expression holds a value of `number`, `string`, `binary` type.
  
  Class diagram is:

        +----------------------------------+
        |              Value               |
        |----------------------------------|
        |- value: number, string or binary |
        +----------------------------------+

  Those types of value are described with string literal, number literal
  and b-prefixed string literal in a script respectively.

  Examples:

        3.141
        'hello'
        b'\x00\x01\x02\0x03'

* An `Identifier` expression consists of a symbol and zero or more attributes trailing it.

  Class diagram is:

        +----------------------------+
        |          Identifier        |
        |----------------------------|
        |- symbol: symbol            |
        |- attrs: set of symbol      |
        |- attrsOpt: set of symbol   |
        |- attrFront: list of symbol |
        +----------------------------+

  Examples:

        foo:attr1:attr2

* A `Suffixed` expression has a suffix symbol and a preceding literal of string or number.

  Class diagram is:

        +---------------------+
        |      Suffixed       |
        |---------------------|
        |- body: string       |
        |- suffix: symbol     |
        +---------------------+

  Examples:

        123.45foo
        'hello world'foo

### {{ page.chapter }}.2.3. Unary Expression

* A `UnaryOp` expression consists of a unary operator
  and a child expression on which the operator is applied.

  Class diagram is:

        +---------------------+         +----------------+
        |       UnaryOp       |   child |      Expr      |
        |---------------------*---------+----------------|
        |- operator: operator |         |                |
        +---------------------+         +----------------+

  Examples:

        -foo

* A `Quote` expression consists of a back quotation
  and a child expression that is to be quoted by it.

  Class diagram is:

        +---------------------+         +----------------+
        |        Quote        |   child |      Expr      |
        |---------------------*---------+----------------|
        |                     |         |                |
        +---------------------+         +----------------+

  Examples:

        `foo

### {{ page.chapter }}.2.4. Binary Expression

* A `BinaryOp` expression consists of a binary operator
  and two child expressions on which the operator is applied.

  Class diagram is:

                                            +----------------+
                                      left  |      Expr      |
                                   +--------+----------------|
        +---------------------+    |        |                |
        |       BinaryOp      *----+        +----------------+
        |---------------------|
        |- operator: operator *----+        +----------------+
        +---------------------+    |  right |      Expr      |
                                   +--------+----------------|
                                            |                |
                                            +----------------+

  Examples:

        x + y

* An `Assign` expression consists of an equal symbol,
  an expression on the left side that is a target of the assignment
  and an expression on the right side that is an assignment source.
  Elements that can be specified on the left are
  `Identifer`, `Lister`, `Indexer`, `Caller` and `Member`.

  Class diagram is:

                                            +----------------+
                                      left  |      Expr      |
                                   +--------+----------------|
        +---------------------+    |        |                |
        |       Assign        *----+        +----------------+
        |---------------------|
        |- operator: operator *----+        +----------------+
        +---------------------+    |  right |      Expr      |
                                   +--------+----------------|
                                            |                |
                                            +----------------+

  Examples:

        x = y

* A `Member` expression is responsible for accessing variables
  in a property owner like instance, class and module.
  Below are available Member accessors.

  Class diagram is:

                                            +----------------+
                                      left  |      Expr      |
                                   +--------+----------------|
        +---------------------+    |        |                |
        |       Member        *----+        +----------------+
        |---------------------|
        |- mode: mode         *----+        +----------------+
        +---------------------+    |  right |      Expr      |
                                   +--------+----------------|
                                            |                |
                                            +----------------+

  Examples:

        x.y  x::y  x:*y  x:&y

  Member accessor `x.y` takes a reference to a property owner on the left side
  and a variable identifier on the right side.

  Others are for what is called Member Mapping and take a list or an iterator on the left side,
  each of which elements is a reference to a property owner.


### {{ page.chapter }}.2.5. Collector Expression

* A `Lister` expression is a series of element expressions embraced by a pair of square brackets.

  Class diagram is:

        +---------------------+           +----------------+
        |        Lister       |  elements |      Expr      |
        |---------------------*-----------+----------------|
        |                     |         * |                |
        +---------------------+           +----------------+


* An `Iterer` expression is a series of element expressions embraced by a pair of parentheses.

  Class diagram is:

        +---------------------+           +----------------+
        |        Iterer       |  elements |      Expr      |
        |---------------------*-----------+----------------|
        |                     |         * |                |
        +---------------------+           +----------------+

* A `Block` expression is a series of element expressions embraced by a pair of square curly brackets.

  Class diagram is:

        +---------------------+           +----------------+
        |        Block        |  elements |      Expr      |
        |---------------------*-----------+----------------|
        |                     |         * |                |
        +---------------------+           +----------------+

* A `Root` expression represents a series of element expressions that appear in the top sequence.

  Class diagram is:

        +---------------------+           +----------------+
        |        Root         |  elements |      Expr      |
        |---------------------*-----------+----------------|
        |                     |         * |                |
        +---------------------+           +----------------+

### {{ page.chapter }}.2.6. Compound Expression

* An `Indexer` expression consists of a head element
  and a series of element expressions embraced by a pair of square brackets.

  Class diagram is:

                                            +----------------+
                                        car |      Expr      |
                                   +--------+----------------|
        +---------------------+    |        |                |
        |       Indexer       *----+        +----------------+
        |---------------------|
        |                     *----+        +----------------+
        +---------------------+    |    cdr |      Expr      |
                                   +--------+----------------|
                                          * |                |
                                            +----------------+

* A `Caller` expression consists of a head element,
  a series of element expressions embraced by a pair of parentheses
  and a block expression.

  Class diagram is:

                                                   +----------------+
                                               car |      Expr      |
                                          +--------+----------------|
        +----------------------------+    |        |                |
        |       Caller               *----+        +----------------+
        |----------------------------|
        |- symbol: symbol            *----+        +----------------+
        |- attrs: set of symbol      |    |    cdr |      Expr      |
        |- attrsOpt: set of symbol   |    +--------+----------------|
        |- attrFront: list of symbol |           * |                |
        +----------------------------+             +----------------+
