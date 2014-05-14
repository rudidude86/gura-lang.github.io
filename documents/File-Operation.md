---
layout: page
lang: en
title: File Operation
chapter: 14
---

# Chapter {{ page.chapter }}. {{ page.title }}

## {{ page.chapter }}.1. Overview

Gura provides mechanism of **Stream** and **Directory** to work on files:
Stream is prepared to read and write content of a file
and Directory to retrieve lists of files stored in some containers.
Here, a term "file" is not limited to what is stored in a file system of an OS.
You can also use Stream and Directory to access files through networks
and even ones stored in an archive files.
Gura provides a generic framework to handle these resources
so that you can expand the capabilities by importing Modules.

Each of Streams and Directories is associated with a uniquely identifiable string called **pathname**.
A framework called **Path Manager** is responsible of recognizing pathname for Stream and Directory
and dispatching file operations to appropriate processes
that have been registered by built-in and imported Modules.


## {{ page.chapter }}.2. Pathname

## {{ page.chapter }}.2.1. Acceptable Format of Pathname

A pathname is a string that identifies Stream and Directory, which should be handled by Path Manager.

By default, built-in module `fs` has been registered to Path Manager,
which tries to recognize a pathname as what is for ones stored in a file system.
Below are some of such examples:

    /home/foo/work/example.txt
    C:\Users\foo\source\main.cpp

You can use both a slash or a backslash as a directory separator for a file in file systems,
which is to be converted by `fs` module to what the current OS can accept.
You can see variable `path.sep_file` to check what character is favorable to the OS.

Importing `curl` module, which provides features to access network using [curl](http://curl.haxx.se/) library,
or importing `http` module would make Path Manager able to recognize URIs that begin with protocol names like "http" and "ftp".

    http://www.example.com/doc/index.html

After importing `zip` module, you can specify a pathname that represents entries in a ZIP archive file.
The example below indicates an entry named `src/main.cpp` in a ZIP file `/home/foo/example.zip`.

    /home/foo/example.zip/src/main.cpp


## {{ page.chapter }}.2.2. Utility Functions to Parse Pathname

Function `path.dirname()` extracts a directory part by eliminating a file part from a pathname.

    rtn = path.dirname('/home/foo/work/example.txt')
    // rtn is '/home/foo/work/'

If the pathname ends with a directory separator,
the function determines it doesn't contain a file part and returns the whole string.

    rtn = path.dirname('/home/foo/work/')
    // rtn is '/home/foo/work/'

Function `path.filename()` extracts a file part from a pathname.

    rtn = path.fileame('/home/foo/work/example.txt')
    // rtn is 'example.txt'

When given with a pathname that ends with a directory separator,
the function determines it doesn't contain a file part and returns a null string.

    rtn = path.filename('/home/foo/work/')
    // rtn is ''

Function `path.split()` splits a pathname by a directory separator
and returns a list containing its directory part and file part.
This works the same as a combination of `path.dirname()` and `path.filename()`.

    rtn = path.split('/home/foo/work/example.txt')
    // rtn is ['/home/foo/work/', 'example.txt']

Function `path.cutbottom()` eliminates the last element in the directory hierarchy.
This works the same as `path.dirname()` when the pathname ends with a file part.

    rtn = path.cutbottom('/home/foo/work/example.txt')
    // rtn is '/home/foo/work/'

Note that it would have a different result if the pathname ends with a directory separator.

    rtn = path.cutbottom('/home/foo/work/')
    // rtn is '/home/foo/'

Function `path.bottom()` splits a pathname and returns the last element.
This works the same as `path.filename()` when the pathname ends with a file part.

    rtn = path.bottom('/home/foo/work/example.txt')
    // rtn is 'example.txt'

Note that it would have a different result if the pathname ends with a directory separator.

    rtn = path.bottom('/home/foo/work/')
    // rtn is 'work'

Function `path.splitext()` splits a pathname by a period existing last
and returns a list containing its preceding part and suffix part.

    rtn = path.splitext('/home/foo/work/example.txt')
    // rtn is ['/home/foo/work/example', 'txt']

Function `path.absname()` takes a relative path name in a file system
and returns an absolute name based on the current directory.


## {{ page.chapter }}.3. Stream

### {{ page.chapter }}.3.1. Stream Instance

A Stream is represented by an instance of `stream` class,
which has a constructor function named `stream()`.
Below shows a declaration of the constructor function:

    stream(pathname:string, mode?:string, codec?:codec):map {block?}

In many platforms and languages, people are accustom to using a term `open`
as a function name for opening a file, or a stream.
So, Gura provides function `open()` as a complete synonym for `stream()`,
which has the same declaration with it.

    open(pathname:string, mode?:string, codec?:codec):map {block?}

In most cases, this document uses `open()` instead of `stream()` to create a `stream` instance.

Function `open()` takes a pathname string as its argument and creates a `stream` instance.

    fd = open('foo.txt')
    // fd is a stream to read data from "foo.txt"

When it is called with its second argument `mode` set to `'w'`,
the function would create a new file and returns a `stream` instance to write data into it.

    fd = open('foo.txt', 'w')
    // fd is a stream to write data into "foo.txt"

A `stream` instance will be closed when method `stream#close()` is called on it.

    fd.close()

When a stream for writing is closed, all the data stored in some buffer would be flushed out.

The method would also automatically be called when the instance is destroyed
after its reference count decreases to zero.
At times, it may be ambiguous about when the instance is destroyed,
so it may be better to use `stream#close()` explicitly
when you want to control the closing timing.

Another way to create and utilize a `stream` instance is to call `open()` function with a block procedure
that will take a `stream` instance through its block parameter.

    open('foo.txt') {|fd|
        // (any jobs)
    }

Using this description, you can access the created instance only within the block,
which will be automatically destroyed at the end of the procedure.


### {{ page.chapter }}.3.2. Cast to Stream Instance

If a certain function has an argument that expects a `stream` instance,
you can pass it a string of a pathname,
which will automatically be converted to a `stream` instance by a casting mechanism.
The `stream` instance would be created as one for reading.

    f(fd:stream) = {
        // fd is a stream instance for reading
        // (any jobs)
    }
    f('foo.txt')   // same as f(open('foo.txt'))

If the argument is declared with `:w` attribute,
the `stream` instance would be created for writing.

    f(fd:stream:w) = {
        // fd is a stream instance for writing
        // (any jobs)
    }
    f('foo.txt')   // same as f(open('foo.txt', 'w'))

Attribute `:r` is also prepared
to explicitly declara that the stream is to be opened for reading.


### {{ page.chapter }}.3.3. Stream Instance for Standard Input/Output

There are three `stream` instances that access standard input and output,
which are assigned to variables in `sys` module.

* `sys.stdin` &hellip; Standard input that retrieves data from key board.
* `sys.stdout` &hellip; Standard output that outputs texts to console screen.
* `sys.stderr` &hellip; Standard error output that outputs texts to console screen without interference of pipe redirection.

Functions `print()`, `printf()` and `println()` output texts to the stream `sys.stdout`.
This means that the following two codes would cause the same result.

    println('Hello world')
    sys.stdout.println('Hello world')

You can also assign a `stream` instance you create to these variables.
Assignment to `sys.stdout` would affect the behavior of printing functions such as `println()`.

    sys.stdout = open('foo.txt', 'w')
    println('Hello world')   // result will be written into 'foo.txt'.


### {{ page.chapter }}.3.4. Stream with Text Data

There are fundamental functions that print texts out to standard output stream.

* Function `print()` takes multiple values that are to be printed out in a proper format to `sys.stdout`.
* Function `println()` works the same as `print()` but also puts a line feed at the end.
* Function `printf()` works similar with C language's `printf()` function
  and prints values to `sys.stdout` based on format specifiers.
  See chapter [String Operation](String-Operation.html) for more details about formatter.

Below is a sample code using above functions to get the same result each other.

    n = 3, name = 'Tanaka'
    print('No.', n, ': ', name, '\n')
    println('No.', n, ': ', name)
    printf('No.%d: %s\n', n, name)

Class `stream` is equipped with methods `stream#print()`, `stream#println()` and `stream#printf()`
that correspond to functions `print()`, `println()` and `printf()` respectively
but output result to the target `stream` instread of `sys.stdout`.
The code below outputs string to a file `foo.txt`.

    n = 3, name = 'Tanaka'
    open('foo.txt', 'w') {|fd|
        fd.print('No.', n, ': ', name, '\n')
        fd.println('No.', n, ': ', name)
        fd.printf('No.%d: %s\n', n, name)
    }

Method `stream#readline()` returns a string containing one line of text from the stream.
It will return `nil` when it reaches to end of the stream,
so you can write a program that prints content of a file as below:

    fd = open('foo.txt')
    while (line = fd.readline()) {
        print(line)
    }

Regarding that there are more cases you need to read multiple lines from a stream,
method `stream#readlines()` may be more useful.
It creates an iterator that returns each line's string as its element.
A program to prints contet of a file comes as below:

    fd = open('foo.txt')
    lines = fd.readlines()
    print(lines)

Using function `readlines()` that takes `stream` instance as its argument,
you don't need to explicitly open a stream because of casting mechanism from `string` to `stream`.
This is the simplest way to read text files.

    lines = readlines('foo.txt')
    print(lines)

If you want to eliminate a line feed character that exists at each line,
specify `:chop` attribute.

    lines = readlines('foo.txt'):chop
    println(lines)

Method `stream#readtext()` returns a string containing the whole content of the stream.

    txt = fd.readtext()


### {{ page.chapter }}.3.5. Character Codecs

While a `string` instance holds string data in UTF-8 format,
there are various character code sets to describe texts in files.
A `stream` instance may contain an instance of `codec` class
that is responsible of converting characters between UTF-8 and those codes.
You can specify a `codec` instance to a `stream` by passing it as a third argument of `open()` function.

    fd = open('foo.txt', 'r', codec('cp932'))

Since there's a casting feature from `string` to `codec` instance,
you can simply specify a codec name to the argument as well.

    fd = open('foo.txt', 'r', 'cp932')

Below is a table that shows what codecs are available and what module provides them.

<table>
<tr><th>Module</th><th>Available Codec Names</th></tr>
<tr><td><code>codecs.basic</code></td><td><code>base64</code>, <code>us-ascii</code>, <code>utf-8</code>, <code>utf-16</code></td></tr>
<tr><td><code>codecs.chinese</code></td><td><code>big5</code>, <code>cp936</code>, <code>cp950</code>, <code>gb2312</code></td></tr>
<tr><td><code>codecs.iso8859</code></td><td><code>iso8859-1</code>, .. <code>iso8859-16</code></td></tr>
<tr><td><code>codecs.japanese</code></td><td><code>cp932</code>, <code>euc-jp</code>, <code>iso-2022-jp</code>, <code>jis</code>, <code>ms_kanji</code>, <code>shift_jis</code></td></tr>
<tr><td><code>codecs.korean</code></td><td><code>cp949</code>, <code>euc-kr</code></td></tr>
</table>

Codecs only have effect on methods to read/write text data that are summarized below:

    stream#print(), stream#println(), stream#printf()
    stream#readline(), stream#readlines(), stream#readtext()

### {{ page.chapter }}.3.6. Stream with Binary Data

`stream#read()`

`stream#write()`

`stream#seek()`

`stream#tell()`

`stream.copy()`

`stream#copyto()`

`stream#copyfrom()`

`stream#compare()`


### {{ page.chapter }}.3.7. Compressor and Decompressor

`gzip` module

`gzipreader`

`gzipwriter`

`bzip2` module

`bzip2reader`

`bzip2writer`



### {{ page.chapter }}.3.8. Base-64 Encoder/Decoder

`base64reader`

`base64writer`



## {{ page.chapter }}.4. Directory

    path.dir
    path.glob
    path.walk


    path.exists

## {{ page.chapter }}.5. Archive File

    tar
    tar.gz
    tar.bz2
    zip

    gz
    bz2

## {{ page.chapter }}.6. OS-specific Operations

`os.stdin`, `os.stdout`, `os.stderr`

`os.exec()`


