---
layout: page
lang: en
title: Comparison between Java8 and Gura
---

# {{ page.title }}

I've learned that Java 8, Java's new version, has come with features like
filter() and map() methods that can handle collections more effectively.
I tried writing Gura code equivalent to some Java programs with these functions
to see how simple the Gura code can be than Java's ones.

## Case 1

Assume that `Student` is a class that has methods named `getGradYear()` and `getScore()`,
which return a graduation year and an exam score respectively.

As for the program to get the maximum score of `students`, a list of instances of `Student`,
who graduate in the year 2012, codes of Java and Gura come as following.

**Java**

    students.filter((Students s) -> s.getGradYear() == 2012)
     .map((Students s) -> s.getScore())
     .max();

**Gura**

    students.filter(students:*getGradYear() == 2012):*getScore().max()


## Case 2

Assume that `Star` is a class that has member variable named `distance`.

When you use reduce() method to implement a code to get maximum `distance` from `stars`,
a list of instances of `Star`, the codes are as following.

**Java**

    stars.stream().map(p -> p.distance).reduce(0, (x, y) -> x > y ? x : y);

**Gura**

    stars:*distance.reduce(0) {|x, y| cond(x > y, x, y)}

Using max() method, the above codes become as following.

**Java**

    stars.stream().map(p -> p.distance).max().orElse(0);

**Gura**

    stars:*distance.max() || 0
