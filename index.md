---
layout: default
lang: en
title: Top
---

# Latest News

<table>
<tr><td valign="top">2014-08-11</td><td>
I'll make a presentation about Gura at <a href="http://ll.jus.or.jp/2014/">LL Diver</a>,
a conference concerning light-weight language, on Aug 23rd in Tokyo.
</td></tr>
<tr><td valign="top">2014-08-11</td><td>
8 月 23 日にお台場日本未来科学館で行われる軽量プログラミング言語カンファレンス
<a href="http://ll.jus.or.jp/2014/">LL Diver</a> にて
Gura のプレゼンテーションを行います。発表資料は
<a href="http://www.slideshare.net/ypsitau/gura-introduction-37974595">こちら</a>。
</td></tr>
<tr><td valign="top">2014-07-10</td><td><a href="Download.html">Gura v0.5.2</a> was released.</td></tr>
</table>


# What's This?

**Gura** is an **iterator-oriented** programming language
that focuses on iterators with improved functions for calculation and data processing.
It gives you a new possibility to write more elegant codes than ever,
but with a familiar appearance.

Take a look at a simple example.
The following code prints content of a text file along with line numbers.

    printf('%d %s', 1.., readlines('foo.txt'))

Apparently, there seems to be no special trick with this program.
But a new feature called **Implicit Mapping** is working internally,
which automatically repeats evaluation of `printf` function
after it's given with iterators, `1..` and `readlines('foo.txt')`, as its arguments.

# Summary of Features

* It provides a variety of iterator operations including [Mapping Process](documents/Mapping-Process.html)
  such as **Implicit Mapping** and **Member Mapping**.
* [Object Oriented Programming](documents/Object-Oriented-Programming.html):
  provides class and instance mechanism.
* Importing [Modules](documents/Module.html) would enhance the language's feature.
  A variety of modules such as image handler, network operations and GUI are shipped within the package.

# Contacts

Any opinions and suggestions are welcome via [E-mail](mailto:ypsitau@nifty.com).
