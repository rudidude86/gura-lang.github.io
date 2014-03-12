---
layout: page
lang: en
title: HTTP Access
---

# {{ page.title }}

## Downlad Files via HTTP

You can download files via HTTP protocol using a generic stream-copy function copy.
Below is the example.

    import(http)
    copy('http://sourceforge.jp/', 'sf.html')

If you want to use a proxy server, you need to specify a server setting
using http.addproxy like follows.

    import(http)
    http.addproxy('xx.xx.xx.xx', 8080, 'username', 'password')
    copy('http://sourceforge.jp/', 'sf.html')


## Read CSV File via HTTP

The following example reads a CSV file in the SVN repository via HTTP protocol
and prints contents of it.

    import(csv)
    import(http)
    uri = 'http://sourceforge.jp/projects/gura/svn/view/trunk/' \
          'test/50records-en.csv?view=co&root=gura'
    Person = struct(name:string, email:string, gender:string, age:number, rest*)
    people = Person * csv.reader(uri):iter
    println(people)

The method `csv#read()`, which reads contents of a CSV file, doesn't have
any idea about HTTP by itself. Gura language engine analyzes the path name,
calls a stream-creating function of an appropriate module depending on it,
http for the above case, and then passes the stream instance to `csv#read()` method.
If you implement a function to receive a stream as its argument,
it's automatically being capable of handling protocols like HTTP and accessing
various type of data structures.

