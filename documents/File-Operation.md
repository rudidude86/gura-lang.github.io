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
and dispatching jobs related to file operation to appropriate processes
that have been registered by embedded and imported Modules.


## {{ page.chapter }}.2. Pathname

## {{ page.chapter }}.2.1. Format of Pathname

A pathname is a string that identifies Stream and Directory, which should be handled by Path Manager.

By default, Path Manager tries to recognize a pathname as what is for ones stored in a file system.
Below are some of such examples:

    /home/foo/work/example.txt
    C:\Users\foo\source\main.cpp

You can use both a slash or a backslash as a directory separator for a file in file systems,
which is to be converted by `fs` module to what the current OS can accept.
You can see variable `path.sep_file` to check what character is favorable to the OS.

Importing `curl` module, which provides features to access network using [curl](http://curl.haxx.se/) library,
or `http` module would make Path Manager able to recognize URIs that begin with protocol names like "http" and "ftp".

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

### {{ page.chapter }}.3.1. Creation of Stream Instance

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


### {{ page.chapter }}.3.3. Pre-created Stream Instance

`sys.stdin`, `sys.stdout`, `sys.stderr`


### {{ page.chapter }}.3.4. Stream Manipulation

binary data 

`stream#read()`

`stream#write()`

`stream#seek()`

`stream#tell()`

`stream.copy()`

`stream#copyto()`

`stream#copyfrom()`

`stream#compare()`

text data

`stream#print()`

`stream#println()`

`stream#printf()`

`stream#readtext()`

`stream#readline()`

`stream#readlines()`


### {{ page.chapter }}.3.5. Character Codecs

<table>
<tr><th>Module</th><th>Codec</th></tr>
<tr><td><code>codecs.basic</code></td><td>base64, us-ascii, utf-8, utf-16</td></tr>
<tr><td><code>codecs.chinese</code></td><td>big5, cp936, cp950, gb2312</td></tr>
<tr><td><code>codecs.iso8859</code></td><td>iso8859-1, .. iso8859-16</td></tr>
<tr><td><code>codecs.japanese</code></td><td>cp932, euc-jp, iso-2022-jp, jis, ms_kanji, shift_jis</td></tr>
<tr><td><code>codecs.korean</code></td><td>cp949, euc-kr</td></tr>
</table>


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


