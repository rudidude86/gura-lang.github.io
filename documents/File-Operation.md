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
You can use Stream and Directory to access files through networks
and even ones stored in an archive files.
Gura provides a generic framework to handle these resources
so that you can expand the capabilities by importing Modules.

Each of Streams and Directories is associated with a uniquely identifiable string called **Pathname**.
A Pathname may be a filename that can be recognized in a file system,
a URI on Internet or a structured identifier in an archive file.
The framework for Stream and Directory recognizes the Pathname
and dispatches jobs to an appropriate process
that has been registered by the interpreter and imported Modules.


## {{ page.chapter }}.2. Pathname

## {{ page.chapter }}.2.1. Format of Pathname

Pathname is a string that identifies Stream and Directory.
Below is an example of a Pathname that represents a file in a file system.

                            +-- suffix part
                            |
                          ----
    /home/foo/work/example.txt
    -------------- -----------
          |             |
          |             +-- file part
          +-- directory part

A separator character should be a slash for Linux system and a back slash for Windows.
You can see variable `path.sep_file` to check which character is used in the current system.


    C:\Users\foo\source\main.cpp

Importing `curl`

    http://www.example.com/doc/index.html

Importing `zip`

    /home/foo/work/example.zip/


## {{ page.chapter }}.2.2. Parsing Pathname

Function `path.absname()`

Function `path.dirname()`

Function `path.filename()`

Function `path.split()`

Function `path.splitext()`

Function `path.bottom()`

Function `path.cutbottom()`



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

