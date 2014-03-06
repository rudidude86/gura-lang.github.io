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

Before the creation of a new script language, I made the guidelines below:

* __Inherit Familiar Syntax__

  I don't think it's a good idea to bother creating an original syntax
  as long as it has same effects as that in exsting languages.
  I decided to follow other popular languages as much as possible
  when I need to make syntax or name variables and functions.
  In fact, as the new language uses a pair of curly brackets to embrace a block,
  an overwhole look of the code may be like one in C or Java.

* __Be Practical__

  Any programming languages are expected to solve problems that actually exist around us.
  For such purposes, capability of reading/writing files and handling text data is still quite important.
  But, these days, having such functions is far from enough
  because various data types and interaces like Internet, image data and graphical interfaces
  become common, which must be handled by many programs.
  To be a practical language, the new one should be shipped with these features as standard.

Following these guidelines, I've developed a script language Gura
that comes with functions and methods that are aware of Implicit Mapping policy,
and registered its first release in SourceForge.JP on March 15, 2011.

I found it amazing to develop a new programming language
since creating a language doesn't instantly mean that the creater is an expert programmer of it.
This may be similar to a situation that you try to come up with an idea of a new game:
even if you make its rule, you have to actually play it to know tricks and tactics
so that you get a victory on the rule.
I also had to create and try a lot of scripts for myself to know how to make programs of Gura.
Throughout the process, I've learned that Gura's various features like Implicit Mapping
are really practical in actual programming fields.

As one user, I can recommend this script language for you.

--------
Yutaka Saito
March 6th, 2014
