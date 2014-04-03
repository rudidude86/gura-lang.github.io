---
layout: page
lang: en
title: Object Oriented Programming
chapter: 9
---

# Chapter {{ page.chapter }}. {{ page.title }}

## {{ page.chapter }}.1. Class and Instance

A **class** is a kind of environment that contains properties such as functions and variables,
and has an ability to create **instances** that share these properties.
A class is associated with a data type one by one,
which means that all the values in a script are bound to certain classes.
For example, a value `3.14` is associated with `number` class,
and `'hello world'` with `string` class.

A class contains functions called **method** that operate with a class or an instance.
A method that belongs to a class is called **class method** and is described as below,
where `Foo` and `func` are names of the class and the class method respectively.

    Foo.func()

A method that works on an instance is called **instance method** and is described as below,
where `Foo` and `func` are names of the class and the instance method respectively.

    Foo#func()

The symbol `#` doesn't exist in an actual script
and only appears in documentation for instance methods.
You can call an instance method like below where `x` is an instance of class `Foo`.

    x.func()

A class also contains variables in it.
A variable that belongs to a class is called **class variable**
and a variable owned by an instance is called **instance variable**.

A class variable is described as below,
where `Foo` and `value` are names of the class the class variable respectively:

    Foo.value

An instance variable is described as below,
where `Foo` and `value` are names of the class the instance variable respectively:

    Foo#value

You can use `dir()` function to see what methods and variables are available with a value.

    >>> x = 3.14
    3.14
    >>> dir(x)
    [`__call__, `__iter__, `clone, `getprop!, `is, `isinstance, `isnil, `istype, `nomap, `roundoff, `setprop!, `tonumber, `tostring]


## {{ page.chapter }}.2. Where A Class Comes From?

    classref()

## {{ page.chapter }}.3. User Class


    A = class {}

    a = A()


## {{ page.chapter }}.4. Inheritance


## {{ page.chapter }}.5. Member Access Control


