---
layout: page
lang: en
title: Member Mapping
---

{{ page.title }}
----------------

You might have faced cases that you have multiple instances of the same class
and you want to execute a same method on them or refer to member variables in them.
You can use Member-mapping for such a case.

To see how Member-mapping works, we prepare a simple structure Fruit.

    Fruit = struct(name:string, price:number) {
        Print() = printf('name:%s  price:%d\n', self.name, self.price)
    }

Function struct returns a constructor function of a structure
that has both of member variables specified by arguments and
member functions declared in the block expression.

When you call this constructor function like follows it would create
a instance of the structure.

    fruit = Fruit('apple', 100)

The following code shows an example of how to access members in an instance.

    printf('%s costs %d\n', fruit.name, fruit.price)
    fruit.Print()

Now, let's create a list of instances of Fruit structure.

    fruits = [
        Fruit('apple', 100), Fruit('orange', 80), Fruit('grape', 120)
    ]

Here's a question: How can we execute a method Print for each instance
in the list? The first idea may be to extract a instance by repeating
statement and then apply the method on each item.
This approach can be realized as follows that use Gura's function for.

    for (fruit in fruits) {
        fruit.Print()
    }

Using Member-mapping, the above process can be written like follows.

    fruits::Print()

Operator `::` shows an operation of Member-mapping.
In this case, it executes Print method for each item in the list fruits.

It may not enough to make you recognize an advantage of a power of Member-mapping.
Now then, the next question. Get a summation of prices of fruits.

Using repeating process, this may be described like follows.

    priceSum = 0
    for (fruit in fruits) {
        priceSum += fruit.price
    }

Using Member-mapping, this comes like follows.

    fruits::price.sum()

It's much simpler. After fruits::prices is evaluated, it returns a list
that contains evaluation result of price member variable in each instance.
The code above executes sum method for the list to get the summation.

The next problem may be a little bit more complicated.
How many characters are contained in the longest name among the Fruit instances?

A solution using repeating statement comes as follows.

    lenMax = -1
    for (fruit in fruits) {
        len = fruit.name.len()
        if (lenMax < len) {
            lenMax = len
        }
    }

Using Member-mapping, it can be described like follows.

    fruits::name::len().max()

An expression `fruits::name` means a list of names for the instances,
and you can get a list of name length by applying `len` method to them.
Then, evaluating `max` method to the whole list shall pick up the maximum
length among them.

It would be a big advantage that you can desribe such a process in a simple expression
when you need to build up more complicated program.
Using the process above, the following example shows how to print a list
of names and prices after aligning name strings to the longest one.

    printf('%-*s %d\n', fruits::name::len().max(), fruits::name, fruits::price)

By the way, as Member-mapping operator `::` creates a list at each process,
you would get a list at any time you evaluate name or len().
This increases the number of lists created during the process depending on
the number of Fruit instances, and causes a less performance
in speed and memory consumption.

To avoid the problem, there's another Member-mapping operator `:*`.
Using this operator, the result shall be an iterator that
delays the evaluation to the timing when the actual calculation is necessary.
The example above can be described as follows.

    printf('%-*s %d\n', fruits:*name:*len().max(), fruits:*name, fruits:*price)

Let's take a look at a little more complicated program using Member-mapping.
The following example performs some statistic calculation after reading
a CSV file that records names, ages and other fields.
Take notice that there's no repeating process any more,
which has been necessary for multiple data handling.

    import(csv)
    
    Person = struct(name:string, email:string, gender:string, age:number, rest*)
    people = Person * csv.reader(open('50records-en.csv'))
    
    familyNames = (people:*name:*split(' '):list)::get(0).sort()
    familyNameSet = set(familyNames)
    
    println('== occurance counting ==')
    Stat = struct(name:string, occurance:number):map
    stats = Stat(familyNameSet, familyNames.count(familyNameSet):map)
    printf('%s(%d), ', stats:*name, stats:*occurance)
    println()
    stats = stats.sort(&{-($stat1.occurance <=> $stat2.occurance)}):stable
    printf('%s(%d), ', stats:*name, stats:*occurance)
    println()
    
    println('== some statistical information ==')
    genders = people::gender
    printf('all=%d male=%d female=%d\n', people.len(), genders.count('male'), genders.count('female'))
    ages = people::age
    printf('age < 30        %d\n', ages.count(&{$age < 30}))
    printf('30 <= age < 40  %d\n', ages.count(&{30 <= $age && $age < 40}))
    printf('40 <= age < 50  %d\n', ages.count(&{40 <= $age && $age < 50}))
    printf('50 <= age < 60  %d\n', ages.count(&{50 <= $age && $age < 60}))
    printf('60 <= age < 70  %d\n', ages.count(&{60 <= $age && $age < 70}))
    printf('70 <= age       %d\n', ages.count(&{70 <= $age}))
