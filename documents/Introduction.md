---
layout: page
lang: en
title: Introduction
---

Introduction
------------

We often see a process that applies some operation or transformation
on multiple data stored in lists and then put the results into another list.
Among them are includes plotting results of a mathematical function fed with sequence of numbers as its parameter
and tansforming multiple records extracted from some database into a specific format.

For such a process, many programming language provides sequence control syntax for repeating,
with which you can pick up elements from a list subsequently
and then create another list that contains result values.
Or, if you're a programmer of a functional language,
it might be a familiar approach that you prepare a higher-order function
with which you apply a certain function on elements in a list.

Either way, you've had to explicitly program "repeat" operation with existing languages.
However, when you provide *n* number of values to a function taking one argument and returning one result,
it's obvious that you want *n* number of answers from it.
If a programming language itself has a feature to repeat a function automatically
when it's given with a list or an iterator as its arguments,
there's no need to explicitly describe repeating syntax any more.

I calls this feature **Implicit Mapping** since it *implicitly* does mapping process.

In order to make this idea come true,
I considered extending an existing script language to be capable of
repeating evaluation of a function under a very limited condition.

But I found out Implicit Mapping could allow much elegant programming
when it could be applied to all the operators as well as many of the functions the language provides.
The idea of Implicit Mapping is so simple, but it's actually a paradigm shift.
I've decided to create a new script language from scratch.

Before the creation of a new script language, I made the following guidelines:

* __Inherit a Familiar Syntax__

  I don't think it's a good idea to bother creating an original syntax
  as long as it has same effects as that in exsting languages.
  I decided to follow other popular languages as much as possible
  when I need to make syntax or name variables and functions.
  In fact, as the new language uses a pair of curly brackets to embrace a block,
  an overwhole look of the code may be like one in C or Java.


