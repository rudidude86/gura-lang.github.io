---
layout: page
lang: en
title: Mapping Process
chapter: 10
---

# Chapter {{ page.chapter }}. {{ page.title }}


## {{ page.chapter }}.1. Implicit Mapping


### {{ page.chapter }}.1.1. Mapping Rule

Implicit Mapping with operators

    scholar + scholar ... scholar
    scholar + list ... list
    scholar + iterator ... iterator
    list + scholar ... list
    list + list ... list
    list + iterator ... iterator
    iterator + scholar ... iterator
    iterator + list ... iterator
    iterator + iterator ... iterator

Implicit Mapping with function call

    f(scholar) ... scholar
    f(list) ... list
    f(iterator) ... iterator

    f(list):iterator
    
    f(iterator):list


    f(x:nomap, y:nomap) = {}

### {{ page.chapter }}.1.2. Disable Implicit Mapping

    f():nomap

### {{ page.chapter }}.1.3. Function Capable of Implicit Mapping

    f():map = { /* body */ }

## {{ page.chapter }}.2. Member Mapping

Member Mapping

    iterable::variable
    iterable:*variable
    iterable:&variable
    iterable::func()
    iterable:*func()
    iterable:&func()
    
    
