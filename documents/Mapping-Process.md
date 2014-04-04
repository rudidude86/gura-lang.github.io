---
layout: page
lang: en
title: Mapping Process
chapter: 10
---

# Chapter {{ page.chapter }}. {{ page.title }}

Implicit Mapping with operators

    scholar X scholar ... scholar
    scholar X list ... list
    scholar X iterator ... iterator
    list X scholar ... list
    list X list ... list
    list X iterator ... iterator
    iterator X scholar ... iterator
    iterator X list ... iterator
    iterator X iterator ... iterator

Implicit Mapping with function call

    f(scholar) ... scholar
    f(list) ... list
    f(iterator) ... iterator

Member Mapping

    iterable::variable
    iterable:*variable
    iterable:&variable
    iterable::func()
    iterable:*func()
    iterable:&func()
    
    
