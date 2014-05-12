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

Each of Streams and Directories is associated with a uniquely identifiable string called **Pathname**.
A framework called **Path Manager** is responsible of recognizing Pathname for Stream and Directory
and dispatching jobs to an appropriate process
that has been registered by embedded and imported Modules.


## {{ page.chapter }}.2. Pathname

## {{ page.chapter }}.2.1. Format of Pathname

Pathname is a string that identifies Stream and Directory, which should be handled by Path Manager.

In default, Path Manager tries to recognize a Pathname as what is for ones stored in a file system.
Below are some of such examples:

    /home/foo/work/example.txt
    C:\Users\foo\source\main.cpp

You can use both a slash or a backslash as a directory separator for a file in file systems,
which is to be converted by `fs` module to what the current OS can accept.
You can see variable `path.sep_file` to check what character is favorable to the OS.

Importing `curl` module, which provides features to access network using [curl](http://curl.haxx.se/) library,
would make Path Manager able to recognize URIs that begin with protocol names like "http" and "ftp".

    http://www.example.com/doc/index.html

After importing `zip` module, you can specify a Pathname that represents entries in a ZIP archive file.
The example below indicates an entry named `src/main.cpp` in a ZIP file `/home/foo/example.zip`.

    /home/foo/example.zip/src/main.cpp


## {{ page.chapter }}.2.2. Parsing Pathname

Function `path.dirname()` extracts a directory part from a Pathanme.

Function `path.filename()` extracts a file part from a Pathname.

Function `path.split()` splits a Pathname by a directory separator
and returns a list containing its directory part and file part.

Function `path.splitext()`

Function `path.bottom()`

Function `path.cutbottom()`

Function `path.absname()` takes a relative path name in a file system
and returns an absolute name based on the current directory.


## {{ page.chapter }}.3. Stream

### {{ page.chapter }}.3.1. Creation of Stream Instance

A Stream is represented by an instance of `stream` class.
One way to create a `stream` instance is to call `open()` function
with an argument specifying a Pathname to open.

    fd = open('foo.txt')
    // fd is a stream instance to read data from "foo.txt"

If a function has an argument that expects a `stream` instance,
you can pass it a string of a Pathname,
which will automatically be converted to a `stream` instance by a casting mechanism.

    f(fd:stream) = {
        // fd is a stream instance for reading
        // (any jobs)
    }
    f('foo.txt')

`:w` attribute

    f(fd:stream:w) = {
        // fd is a stream instance for writing
        // (any jobs)
    }


### {{ page.chapter }}.3.2. Stream Manipulation

### {{ page.chapter }}.3.3. Character Codecs




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

