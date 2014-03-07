---
layout: page
lang: en
title: Object Oriented Programming
---

{{ page.title }}
----------------

Gura provides class mechanism for object oriented programming.
Take a look at a simple example below.

    Person = class {
        __init__(first:string, last:string, age:number) = {
            this.first = first
            this.last = last
            this.age = age
        }
        Hello() = {
            printf('Hello, my name is %s %s.\n', this.first, this.last)
        }
    }
    
    person = Person('Taro', 'Yamada')
    person.Hello()

`this`
`__init__`

