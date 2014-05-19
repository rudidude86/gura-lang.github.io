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

### {{ page.chapter }}.2.1. Acceptable Format of Pathname

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


### {{ page.chapter }}.2.2. Utility Functions to Parse Pathname

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

A Stream is a data object to read and write content of a file
and represented by a `stream` instance created by a constructor function named `stream()`.
Below shows a declaration of the constructor function:

    stream(pathname:string, mode?:string, codec?:codec):map {block?}

In many platforms and languages, people are accustom to using a term `open`
as a function name for opening a file, or a stream.
So, function `open()` is provided as a complete synonym for `stream()`,
which has the same declaration with it.

    open(pathname:string, mode?:string, codec?:codec):map {block?}

In many cases, this document uses function `open()` instead of `stream()` to create a `stream` instance.

Function `open()` takes a pathname string as its argument and returns a `stream` instance.

    fd = open('foo.txt')
    // fd is a stream to read data from "foo.txt"

When it is called with its second argument `mode` set to `'w'`,
the function would create a new file and returns a `stream` instance to write data into it.

    fd = open('foo.txt', 'w')
    // fd is a stream to write data into "foo.txt"

A `stream` instance will be closed when method `stream#close()` is called on it.

    fd.close()

When a stream for writing is closed, all the data stored in some buffer would be flushed out
before the instance is invalidated.

Method `stream#close()` would also be called automatically when the instance is destroyed
after its reference count decreases to zero.
At times, it may be ambiguous about when the instance is destroyed,
so it may be better to use `stream#close()` explicitly
when you want to control the closing timing.

Another way to create and utilize a `stream` instance is to call `open()` function with a block procedure
that will take a `stream` instance through its block parameter.

    open('foo.txt') {|fd|
        // any jobs here
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
        // any jobs here
    }
    f('foo.txt')   // same as f(open('foo.txt'))

If the argument is declared with `:w` attribute,
the `stream` instance would be created for writing.

    f(fd:stream:w) = {
        // fd is a stream instance for writing
        // any jobs here
    }
    f('foo.txt')   // same as f(open('foo.txt', 'w'))

Attribute `:r` is also prepared
to explicitly declara that the stream is to be opened for reading.


### {{ page.chapter }}.3.3. Stream Instance for Standard Input/Output

There are three `stream` instances for the access to standard input and output,
which are assigned to variables in `sys` module.

* `sys.stdin` &hellip; Standard input that retrieves data from key board.
* `sys.stdout` &hellip; Standard output that outputs texts to console screen.
* `sys.stderr` &hellip; Standard error output that outputs texts to console screen without interference of pipe redirection.

Functions `print()`, `printf()` and `println()` output texts to the stream `sys.stdout`.
This means that the following two codes would cause the same result.

    println('Hello world')
    sys.stdout.println('Hello world')

You can also assign a `stream` instance you create to these variables.
Assignment to `sys.stdout` would affect the behavior of functions such as `println()`.

    sys.stdout = open('foo.txt', 'w')
    println('Hello world')   // result will be written into 'foo.txt'.


### {{ page.chapter }}.3.4. Stream with Text Data

There are fundamental functions that print texts out to standard output stream.

* Function `print()` takes multiple values that are to be printed out to `sys.stdout` in a proper format.
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
that correspond to functions `print()`, `println()` and `printf()` respectively,
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

Regarding that you often need to read multiple lines from a stream,
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

An iterator created by method `stream#readlines()` and function `readlines()` owns a reference to the `stream` instance
because they're designed to read data from it while iteration.
This means that the stream instance won't be released while such iterator is running.

Consider the following code that is expected to read text from `foo.txt` and
write text back to the same file after converting alphabet characters to upper case.

    lines = readlines('foo.txt')
    open('foo.txt', 'w').print(lines:*upper())

Unfortunately, this program doesn't work correctly.
The iterator `lines` owns a stream to read content from the file `foo.txt`,
which conflicts with the attempt to open `foo.txt` for writing.
To avoid this, you need to call `readlines()` function with `:list` attribute
that reads whole the lines from the stream before storing them to a `list` instance.
The function would release the stream and then return the `list` instance as its result.

    lines = readlines('foo.txt'):list
    open('foo.txt', 'w').print(lines:*upper())

Method `stream#readtext()` returns a string containing the whole content of the stream.

    txt = fd.readtext()

As for the character sequence existing at each end of line in a file,
two types of sequence are acceptable: LF (0x0a) and CR(0x0d)-LF(0x0a).
Some systems like Linux that have inherited from UNIX uses LF code at line end
while Windows uses CR-LF sequence.
By default, the following policies are applied
so that the string read from a file would only contain LF code.

* When reading, all the CR codes are removed.
* When writing, there's no modification about the sequence of end of line.
  This results in a file containing only LF code.

To change this behavior, use methods `stream#delcr()` and `stream#addcr()`.
If you want to keep CR code from the read text, call `stream#delcr()` method with an argument set to `false`.

    fd.delcr(false)

If you want to append CR code at each end of line in a file to write, call `stream#addcr()` method with an argument set to `true`.

    fd.addcr(true)


### {{ page.chapter }}.3.5. Character Codecs

While a `string` instance holds string data in UTF-8 format,
there are various character code sets to describe texts in files.
To be capable of handling them, a `stream` instance may contain an instance of `codec` class
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

The standard output/input streams, `sys.stdin`, `sys.stdout` and `sys.stderr`,
must be equipped with a codec of the character code set that the console device expects.
While the detection of a proper codec is done by a value of environment variable `LANG` or a result of some system API functions,
it may sometimes happen that you want to change codec in these.
In such a case, you can use `stream#setcodec()` like below:

    sys.stdout.setcodec('utf-8')


### {{ page.chapter }}.3.6. Stream with Binary Data

In addition to methods to handle text data,
class `stream` is equipped with methods to read/write binary data as well.

Method `stream#read()` reads specified size of data into a `binary` instance and returns it.
When the stream reaches its end, the method returns `nil`.

    open('foo.bin') {|fd|
        while (buff = fd.read(512)) {
            // some jobs with buff
        }
    }

Method `stream#write()` writes content of a `binary` instance to the stream.

    open('foo.bin', 'w') {|fd|
        fd.write(buff)
    }

Method `stream#seek()` moves the current offset at which read/write operations are applied.

Method `stream#tell()` returns the current offset.

Methods `stream.copy()`, `stream#copyto()` and `stream#copyfrom()`
are responsible of copying data from a stream to another stream.
They have the same result each other but take `stream` instances in different ways.
Below shows how they are called where `src` means a source stream and `dst` a destination.

    stream.copy(src, dst)
    src.copyto(dst)
    dst.copyfrom(src)

These methods can take a block procedure that takes `binary` instance containing
a data segment during the copy process. The size of a data segment can be specified by an argument named `bytesunit`.

    stream.copy(src, dst) {|buff:binary|
        // any job during copying process
    }

You can use the block procedure with the copying method
to realize a indicator that shows how much process the methods have done.

Method `stream#compare()` compares contents between two streams
and returns `true` if there's no difference and `false` otherwise.


### {{ page.chapter }}.3.7. Filter Stream

A Filter Stream is what is attached to other `stream` instance
and applies data modification while reading or writing operation.

There are two types of Filter Stream: reader and writer.

A Filter Stream of reader type applies operation on methods for reading data
including `stream#read()`, `stream#readline()`, `stream#readlines()` and `stream#readtext()`.

    +--------+    +---------------+
    | stream |--->| filter stream |---> (reading data)
    |        |    |   (reader)    |
    +--------+    +---------------+

A Filter Stream of writer type applies operation on methods for writing data
including `stream#write()`, `stream#print()`, `stream#println()` and `stream#printf()`.

    +--------+    +---------------+
    | stream |<---| filter stream |<--- (writing data)
    |        |    |   (writer)    |
    +--------+    +---------------+

Module `gzip` provides functions to read and write files in gzip format,
which usually have a suffix `.gz`.
Importing the module would add following methods to `stream` class.

* `stream#gzipreader()` returns a stream from which you can read data
  after decompressing a sequence of gzip format from the attached stream.
* `stream#gzipwriter()` returns a stream to which you can write data
  that are to be compressed to a sequence of gzip format into the attached stream.

Module `bzip2` provides functions to read and write files in bzip2 format,
which usually have a suffix `.bz2`.
Importing the module would add following methods to `stream` class.

* `stream#bzip2reader()` returns a stream from which you can read data
  after decompressing a sequence of bzip2 format from the attached stream.
* `stream#bzip2writer()` returns a stream to which you can write data
  that are to be compressed to a sequence of bzip2 format into the attached stream.

Module `base64` provides functions to encode and decode files in Base64 format,
which often appear in protocols of network.
It's a build-in module that you can utilize without importing
and makes following methods available in `stream` class.

* `stream#base64reader()` returns a stream from which you can read data
  after decoding a sequence of Base64 format from the attached stream.
* `stream#base64writer()` returns a stream to which you can write data
  that are to be encoded to a sequence of Base64 format into the attached stream.

Following code is an example to read content of a file in gzip format:

    import(gzip)
    open('foo.gz') {|fd_gzip|
        fd = fd_gzip.gzipreader()
        // reading process from fd
        fd.close()
    }

These methods that generate a Filter Stream can accept a block procedure just like `open()` function,
in which you can take the instance of Filter Stream as a block parameter.

    import(gzip)
    open('foo.gz') {|fd_gzip|
        fd_gzip.gzipreader {|fd|
            // reading process from fd
        }
    }

Or simply, you can write it as below:

    import(gzip)
    open('foo.gz').gzipreader {|fd|
        // reading process from fd
    }

The same goes with a writing process.
In this case, the attached stream must have a writing attribute.

    import(gzip)
    open('foo.gz', 'w') {|fd_gzip|
        fd = fd.gzipwriter()
        // writing process to fd
        fd.close()
    }

You can also attach a Filter Stream on yet another Filter Stream,
which enables you to compose a chain of stream.
Following is a code to decode a sequence in Base64 and then decompress it with gzip algorithm:

    import(gzip)
    open('foo.gz.hex') {|fd_hex|
        fd_hex.base64reader().gzipreader {|fd|
            // reading process from fd
        }
    }

Below shows a diagram of the process:

    +--------+    +-----------------+    +---------------+
    | stream |--->|  filter stream  |--->| filter stream |---> (reading data)
    |        |    | (base64 reader) |    | (gzip reader) |
    +--------+    +-----------------+    +---------------+

You can construct a chain of stream for writing process, too.

    import(gzip)
    open('foo.gz.hex', 'w') {|fd_hex|
        fd_hex.base64writer().gzipwriter {|fd|
            // writing process to fd
        }
    }

Below shows a diagram of the process:

    +--------+    +-----------------+    +---------------+
    | stream |<---|  filter stream  |<---| filter stream |<--- (writing data)
    |        |    | (base64 writer) |    | (gzip writer) |
    +--------+    +-----------------+    +---------------+


## {{ page.chapter }}.4. Directory

### {{ page.chapter }}.4.1. Operations

A Directory is a data object to seek a list of files and sub directories and is represented by `directory` class.
But currently, there's few chance to utilize the `directory` instance explicitly
since it is usually built in other objects like iterators and hidden from users.
One thing you have to note about `directory` is that
you can cast a `string` containing a pathname to `directory` instance,
so you can pass a pathname to an argument declared with `directory` type.

There are three functions that searches files and sub directories:
`path.dir()`, `path.glob()` and `path.glob()`.
Consider the following directory structure to see how these functions work.

    tb
    |
    +--dir-A
    |  +--file-4.txt
    |  `--file-5.txt
    +--dir-B
    |  +--dir-C
    |  |  +--file-6.doc
    |  |  `--file-7.doc
    |  `--dir-D
    +--file-1.txt
    +--file-2.doc
    `--file-3.txt

Function `path.dir()` creates an iterator that returns pathname of files and sub directories
that exists in the specified directory.
For example, a call `path.dir('tb')` create an iterator that returns following strings.

    tb/dir-A/
    tb/dir-B/
    tb/file-1.txt
    tb/file-2.doc
    tb/file-3.txt


Function `path.glob()` creates an iterator that returns pathname of files and sub directories
matching the given pattern with wild cards.
For example, a call `path.glob('tb/*.txt')` create an iterator that returns following strings.

    tb/file-1.txt
    tb/file-3.txt

Function `path.walk()` creates an iterator that seeks directory structure recursively
and returns pathname of files and sub directories.
For example, a call `path.walk('tb')` create an iterator that returns following strings.

    tb/dir-A/
    tb/dir-B/
    tb/file-1.txt
    tb/file-2.doc
    tb/file-3.txt
    tb/dir-A/file-4.txt
    tb/dir-A/file-5.txt
    tb/dir-B/dir-C/
    tb/dir-B/dir-D/
    tb/dir-B/dir-C/file-6.doc
    tb/dir-B/dir-C/file-7.doc

### {{ page.chapter }}.4.2. Status Object

While an iterator created by functions `path.dir()`, `path.glob()` and `path.glob()`
returns a string of pathname,
specifying `:stat` attribute would make it return an object that contains more detail information.

`fs.stat`

`tar.stat`

`zip.stat`

`http.stat`



## {{ page.chapter }}.5. Archive File

`tar` module

    .tar
    .tar.gz
    .tar.bz2

`zip` module

    .zip


## {{ page.chapter }}.6. OS-specific Operations

### {{ page.chapter }}.6.1. Operation on File System

`fs.mkdir()`

`fs.rmdir()`

`fs.remove()`

`fs.rename()`

`fs.chmod()`

`fs.cpdir()`

### {{ page.chapter }}.6.2. Execute Other Process

`os.stdin`, `os.stdout`, `os.stderr`

`os.exec()`
