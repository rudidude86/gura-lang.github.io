---
layout: page
lang: en
title: Reading Text File
---

# {{ page.title }}




    for (line in readlines('people.txt')) {
        print(line)
    }

    print(readlines('people.txt'))

    open('people2.txt', 'w').print(readlines('people.txt'))

    open('people.txt', 'w').print(readlines('people.txt'):list)

declaration of `readlines` function:

    readlines(stream?:stream:r):[chop] {block?}


    readlines(open('people.txt'))
