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

The interpreter itself provides fundamental operations for strings.
Importing module named `re` expand the capability so that it can process regular expressions.


## {{ page.chapter }}.2. Basic Operation


### {{ page.chapter }}.2.1. Character Manipulation

You can specify an index number starting from zero embraced by a pair of square brackets
to retrieve a character as a sub string at the specified position.
Multiple numbers for indexing can also be specified to get a list of sub strings.

    str = 'abcdefghijklmnopqrstuvwxyz'
    str[6]            // returns 'g'
    str[20]           // returns 'u'
    str[17]           // returns 'r'
    str[0]            // returns 'a'
    str[6, 20, 17, 0] // returns ['g', 'u', 'r', 'a']

You can also specify iterators to get a list of sub strings.
Numbers and iterators can be mixed together as indexing items.

    str = 'The quick brown fox jumps over the lazy dog'
    str[10..14]       // returns ['b', 'r', 'o', 'w', 'n']
    str[4..8, 35..38] // returns ['q', 'u', 'i', 'c', 'k', 'l', 'a', 'z', 'y']

If you specify an infinite iterator as an indexing item,
you would get sub strings within an available range.

    str = 'The quick brown fox jumps over the lazy dog'
    str[35..]       // returns ['l', 'a', 'z', 'y', ' ', 'd', 'o', 'g']

Function `chr()` returns a string that contains a character of the given UTF-8 character code.

    chr(65)         // returns 'A'

Function 'ord()` takes a string and returns UTF-8 character code of its first character.

    ord('A')        // returns 65


### {{ page.chapter }}.2.2. Iteration

Method `string#each()` creates an iterator that returns each character as a sub string.

    str = 'The quick brown fox jumps over the lazy dog'
    x = str.each()
    // x is an iterator that returns 'T', 'h', 'e' ...

A call of `string#each()` with attribute `:utf8` or `:utf32` would create an iterator
that returns character code numbers in UTF-8 or UTF-32 instead of sub strings.

    str = 'XXX'  // assumes it contains kanji characters 'ni-hon-go'
    x = str.each():utf8
    // x is an iterator that returns 0xe697a5, 0xe69cac and 0xe7aa9e

    x = str.each():utf32
    // x is an iterator that returns 0x65e5, 0x672c and 0x8a9e

Method `string#eachline()` creates an iterator that splits a string by a newline character
and returns strings of each line.

    str = R'''
    1st
    2nd
    3rd
    '''
    lines = str.eachline()
    // lines is an iterator that returns '1st\n', '2nd\n' and '3rd\n'

Method `string#chop()` is useful when you want to remove a newline character
appended at the bottom.

    x = str.eachline()
    lines = x:*chop()  // an iterator to apply string#chop() to each value in x
    // lines is an iterator that returns '1st', '2nd' and '3rd'

Method `string#eachline()` and others that split a multi-lined text into strings of each line
like `readlines()` are equipped with an attribute `:chop`
that applies the same process as `string#chop()`.

    lines = str.eachline():chop
    // lines is an iterator that returns '1st', '2nd' and '3rd'

Method `string#split()` creates an iterator that splits a string
by a separator string specified in the argument.

    str = 'The quick brown fox jumps over the lazy dog'
    x = str.split(' ')
    // x is an iterator that returns 'The', 'quick', 'brown', 'fox' ...

If you want to split a string into segments with the same length,
use `string#fold()` method.

    str = 'abcdefghijklmnopqrstuvwxyz'
    x = str.fold(5)
    // x is an iterator that returns 'abcde', 'fghij', 'klmno', 'pqrst', 'uvwxy' and 'z'


### {{ page.chapter }}.2.3. Modification and Conversion

Applying an operator `+` between two `string` instances would concatenate them together.

    str1 = 'abcd'
    str2 = 'efgh'
    str1 + str2   // returns 'abcdefgh'

An operator `*` between a `string` and a `number` value would concatenate the string the specified number of times.

    str = 'abcd'
    str * 3      // returns 'abcdabcdabcd'

Method `list#join()` joins all the string in the list and returns the result.
If it contains elements other than `string`, they're converted to strings before joined.

    ['abcd', 'efgh', 'ijkl'].join()    // returns 'abcdefghijkl'

The method can take a separator string as its argument that is inserted between elements.

    ['abcd', 'efgh', 'ijkl'].join(', ') // returns 'abcd, efgh, ijkl'

Method `string#capitalize()` returns a string with the top alphabet converted to uppper case.

    str = 'hello, WORLD'
    str.capitalize()  // returns 'Hello, WORLD'

Methods `string#upper()` and `string#lower()` return a string after converting
all the alphabet characters to upper and lower case respectively.

    str = 'hello, WORLD'
    str.upper()       // returns 'HELLO, WORLD'
    str.lower()       // returns 'hello, world'

Method `string#binary()` returns a `binary` instance
that contains a binary sequence of the string in UTF-8 format.

    str = 'XXX'    // assumes it contains kanji characters 'ni-hon-go'
    str..binary()  // returns a binary b'\xe6\x97\xa5\xe6\x9c\xac\xe8\xaa\x9e'

You can use `string#encode()` to get a binary sequence in other codec other than UTF-8.

    str = 'XXX'              // assumes it contains kanji characters 'ni-hon-go'
    str.encode('shift_jis')  // returns a b'\x93\xfa\x96\x7b\x8c\xea'

Method `string#reader()` returns a `stream` instance
that reads a binary sequence of the string in UTF-8 format.

    str = 'The quick brown fox jumps over the lazy dog'
    x = str.reader()
    // x is a stream instance for reading

Method `string#encodeuri()` converts characters that can not be described in URI
by a percent-encoding rule,
while method `string#decodeuri()` converts such encoded string into normal characters.

Method `string#escapehtml()` escapes characters that can not be described in HTML
with character entities prefixed by an ampersand,
while method `string#unescapehtml()`converts such escaped ones into normal characters.


### {{ page.chapter }}.2.4. Extraction

Method `string#strip()` removes space characters that exist on both sides of the string.
Attributes `:left` and `:right` would specify the side to remove spaces.

    str = '    hello  '
    str.strip()        // returns 'hello'
    str.strip():left   // returns 'hello  '
    str.strip():right  // returns '    hello'

Method `string#left()` returns a sub string
that has extracted specified number of characters from the left side,
while method `string#right()`extracts from the right side.

    str = 'The quick brown fox jumps over the lazy dog'
    str.left(3)  // returns 'The'
    str.right(3) // returns 'dog'

Method `string#mid()` returns a sub string
that has extracted specified number of characters from the specified position.

    str = 'The quick brown fox jumps over the lazy dog'
    str.mid(10, 5)  // returns 'brown'


### {{ page.chapter }}.2.5. Search, Replace and Inspection

To see the length of a string, `string#len()` is available.
Note that `string#len()` returns the number of characters, not the size in byte.

    str = 'abcdefghijklmnopqrstuvwxyz'
    n = str.len()
    // n is 26

Method `string#find()` searches the specified sub string in the target string
and returns the found position starting from zero. If not found, it returns `nil`.

    str = 'The quick brown fox jumps over the lazy dog'
    str.find('fox')  // returns 16
    str.find('cat')  // returns nil

Method `string#replace()` replaces the sub string with the specified one.

    str = 'The quick brown fox jumps over the lazy dog'
    str.replace('fox', 'cat') // returns 'The quick brown cat jumps over the lazy dog'

Method `string#startswith()` returns `ture` if the string starts with the specified sub string,
and returns `false` otherwise.
Method `string#endswith()` checks if the string ends with the specified sub string.

    str = 'abcdefghijklmnopqrstuvwxyz'
    str.startswith('abcde') // returns true
    str.startswith('hoge')  // returns false
    str.endswith('vwxyz')   // returns true
    str.endswith('hoge')    // returns false

Specifying an attribute `:rest` indicates that these functions return a string
excluding the specified sub string when that matches the head or the bottom part.
If the sub string doesn't match, they would return `nil`.

    str.startswith('abcde):rest // returns 'fghijklmnopqrstuvwxyz'
    str.startswith('hoge'):rest // returns nil
    str.endswith('vwxyz'):rest  // returns 'abcdefghijklmnopqrstu'
    str.endswith('hoge'):rest   // returns nil


## {{ page.chapter }}.3. Formatter

## {{ page.chapter }}.3.1. Functions Equipped with Formatter

You can use format specifiers in some functions that are similar to what are realized in C language's `printf`
to convert objects like numbers into readable strings.

Function `printf()` takes a string containing format specifiers
and values you want to print in its argument list
and put the result out to `sys.stdout` stream.

    printf('x = %d, y = %d\n', x, y)

Method `stream#printf()` has the same argument declaration with `printf()`
and puts the result to the target stream capable of writing
instead of `sys.stdout` stream.

    open('foo.txt', 'w').printf('x = %d, y = %d\n', x, y)

Method `list#printf()` is another form of `printf()`,
which takes values to print in the list of the target instance, not in the argument list.

    [x, y].printf('x = %d, y = %d\n')

Function `format()` takes arguments in the same way as `printf()`
but it returns the result as a `string` instance.

    str = format('x = %d, y = %d\n', x, y)

You can also use `%` operator to get the same result with `format()`,
which takes a format string on the left and a list containing values for printing on the right.

    str = 'x = %d, y = %d\n' % [x, y]

If there's only one value for printing,
you can even give the operator the value without a list.

    str = 'x = %d\n' % x


## {{ page.chapter }}.3.2. Syntax of Format Specifier

A format specifier begins with a percent character and has the syntax below,
where optional fields are embraced by square brackets:

    %[flags][width][.precision]specifier

You always have to specify one of the following characters for the `specifier` field.

<table>
<tr><th>specifier</th><th>Note</th></tr>
<tr><td><code>d</code>, <code>i</code></td><td>decimal integer number with a sign mark</td></tr>
<tr><td><code>u</code></td><td>decimal integer number wihout a sign mark</td></tr>
<tr><td><code>b</code></td><td>binary integer number without a sign mark</td></tr>
<tr><td><code>o</code></td><td>octal integer number without a sign mark</td></tr>
<tr><td><code>x</code></td><td>hexadecimal integer number in lower character without a sign mark</td></tr>
<tr><td><code>X</code></td><td>hexadecimal integer number in upper character without a sign mark</td></tr>
<tr><td><code>e</code></td><td>floating number in exponential form</td></tr>
<tr><td><code>E</code></td><td>floating number in exponential form (in upper character)</td></tr>
<tr><td><code>f</code></td><td>floating number in decimal form</td></tr>
<tr><td><code>g</code></td><td>better form between e and f</td></tr>
<tr><td><code>G</code></td><td>better form between E and F</td></tr>
<tr><td><code>s</code></td><td>string</td></tr>
<tr><td><code>c</code></td><td>character</td></tr>
</table>

You can specify one of the following characters for the optional `flags` field.

<table>
<tr><th>flags</th><th>Note</th></tr>
<tr><td><code>+</code></td><td><code>+</code> precedes for positive numbers</td></tr>
<tr><td><code>-</code></td><td>adjust a string to left</td></tr>
<tr><td>(space)</td><td>space character precedes for positive numbers</td></tr>
<tr><td><code>#</code></td><td>converted results of binary, octdecimal and hexadecimal are
  preceded by <code>'0b'</code>, <code>'0'</code> and <code>'0x'</code> respectively</td></tr>
<tr><td><code>0</code></td><td>fill lacking columns with <code>'0'</code></td></tr>
</table>

The optional field `width` takes a decimal number that specifies a minimum width for the corresponding value.
If the value's length is shorter than the specified width, the rest would be filled with space characters.
If you specify `*` for that field, the formatter would try to get the minimum width from the argument list.

The optional field `precision` has different meanings depending on the specifier as below:

<table>
<tr><th>specifier</th><th>Note</th></tr>
<tr><td><code>d</code>, <code>i</code>, <code>u</code>, <code>b</code>, <code>o</code>, <code>x</code>, <code>X</code></td>
  <td>It specifies the minimum number of digits. If the value is shorter than this number,
    lacking digits are filled with zero.</td></tr>
<tr><td><code>e</code>, <code>E</code>, <code>f</code></td>
  <td>It specifies the number of digits after a decimal point.</td></tr>
<tr><td><code>g</code>, <code>G</code></td>
  <td>It specifies the maximum number of digits for significand part.</td></tr>
<tr><td><code>s</code></td>
  <td>It specifies the maximum number of characters to print.</td></tr>
</table>


## {{ page.chapter }}.4. Regular Expression

You can import module `re` to use regular expression for string search and substition,
which supports a syntax based on POSIX Extended Regular Expression.

Importing module `re` would equip `string` class with methods that can handle regular expressions.
See the sample code below:

    import(re)
    
    str = '12:34:56'
    
    m = str.match(r'(\d\d):(\d\d):(\d\d)')
    if (m) {
        printf('hour=%s, min=%s, sec=%s\n', m[1], m[2], m[3])
    } else {
        println('not match')
    }

Method `string#match()` that is provided by `re` module takes a regular expression pattern.
It would return `re.match` instance if the pattern matches, and return `nil` otherwise.
As regular expressions often contain back slash as a meta character,
it would be convenient to use an expression `r'` &hellip; `'` for a pattern string
to avoid recognizing a backslash as an escaping character.

An instance of `re.match` contains information about matching result.
It supports indexing access where `m[0]` has a string that matches the whole pattern
and `m[1]`, `m[2]` &hellip; returns a string of each group.
You can specify a string instead of a number to index each group
when you use `?<name>` specifier for the group in a regular expression pattern.

    m = str.match(r'(?<hour>\d\d):(?<min>\d\d):(?<sec>\d\d)')
    if (m) {
        printf('hour=%s, min=%s, sec=%s\n', m['hour'], m['min'], m['sec'])
    } else {
        println('not match')
    }

Although you can pass a string containing a pattern to method `string#match()`,
it actually takes `re.pattern` instance in its argument that is capable of
accepting a `string` instance through casting feature.
Above example is equivalent with below:

    pat = re.pattern(r'(\d\d):(\d\d):(\d\d)')
    m = str.match(pat)

When you give a string to a function or a method that expects `re.pattern`,
it always compile the string to create `re.pattern` instance,
which may cause some overhead in a process of huge amount of data.
In such a case, it may be a good idea to call a function with a `re.pattern` instance
that has explicitly been created by `re.pattern()` function in advance like shown above.

`string#sub()`





