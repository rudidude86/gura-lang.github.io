---
layout: page
lang: en
title: Reading Text File
---

# {{ page.title }}

Reading text files may be one of the most common process in a program.


A function `readlines` creates an iterator that reads a content from a stream
and returns string of lines.



    for (line in readlines('foo.txt')) {
        print(line)
    }

    print(readlines('foo.txt'))

    open('foo2.txt', 'w').print(readlines('foo.txt'))

    open('foo.txt', 'w').print(readlines('foo.txt'):list)

declaration of `readlines` function:

    readlines(stream?:stream:r):[chop] {block?}


    readlines(open('foo.txt'))
