---
layout: default
lang: en
title: Top
---

# Latest News

<table>
<tr><td>2014-02-25</td><td><a href="Download.html">Gura v0.4.2</a> was released.</td></tr>
<tr><td>2014-02-14</td><td>Gura v0.4.1 was released.</td></tr>
<tr><td>2014-02-06</td><td>Gura v0.4.0 was released.</td></tr>
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
But a new feature called [Implicit Mapping](features/ImplicitMapping.html) is working internally,
which automatically repeats evaluation of `printf` function
after it's given with iterators, `1..` and `readlines('foo.txt')`, as its arguments.

<div id="box-left">

<h1>Language Features</h1>

<p>
<div><a href="features/Implicit-Mapping.html">Implicit Mapping</a></div>
<div><a href="features/Member-Mapping.html">Member Mapping</a></div>
<div><a href="features/Object-Oriented-Programming.html">Object Oriented Programming</a></div>
</p>

<h1>Enjoy Programming</h1>

<p>
<div><a href="extensions/Create-Animation-GIF.html">Create Animation GIF</a></div>
<!--
<div><a href="extensions/Reading-Text-File.html">Reading Text File</a></div>
-->
<div><a href="extensions/Graphic-Image-Handling.html">Graphic Image Handling</a></div>
<div><a href="extensions/GUI-Programming-with-wxWidgets.html">GUI Programming with wxWidgets</a></div>
<div><a href="extensions/GUI-Programming-with-Tk.html">GUI Programming with Tk</a></div>
<div><a href="extensions/GUI-Programming-with-SDL.html">GUI Programming with SDL</a></div>
<div><a href="extensions/Programming-with-OpenGL.html">Programming with OpenGL</a></div>
<div><a href="extensions/Programming-with-Cairo.html">Programming with Cairo</a></div>
<div><a href="extensions/Http-Access.html">HTTP Access</a></div>
<div><a href="extensions/Http-Server.html">HTTP Server</a></div>
<div><a href="extensions/Database-Access.html">Database Access</a></div>
<div><a href="extensions/Create-Your-Own-Binary-Module.html">Create Your Own Binary Module</a></div>
</p>

<h1>Articles</h1>

<p>
<div><a href="articles/Comparison-between-Java8-and-Gura.html">Comparison between Java 8 and Gura</a></div>
<div><a href="articles/Script-to-Generate-Prime-Numbers.html">Script to Generate Prime Numbers</a></div>
</p>

<h1>Sample Code</h1>

<p>Sample codes of Gura are stored in
<a href="https://github.com/gura-lang/gura/tree/master/sample"
 onClick="_gaq.push(['_trackEvent','repository','click','sample']);">Repository</a>.
</p>

<h1>Contacts</h1>

<p>Any opinions and suggestions are welcome via <a href="mailto:ypsitau@nifty.com">E-mail</a>.</p>

</div>

<div id="box-right">

<h1>Documents</h1>

<h2>Japanese</h2>

Sorry! Only Japanese version is available so far.

<p>
<div><img src="images/pdf.png" alt="pdf-icon" /> Gura Language Manual
(<a href="https://github.com/gura-lang/gura-doc/blob/master/gura-lang-j.pdf?raw=true"
  onClick="_gaq.push(['_trackEvent','document','click','gura-lang-j.pdf']);">Japanese</a>)</div>
<div><img src="images/pdf.png" alt="pdf-icon" /> Gura Library Reference
(<a href="https://github.com/gura-lang/gura-doc/blob/master/gura-lib-j.pdf?raw=true"
  onClick="_gaq.push(['_trackEvent','document','click','gura-lib-j.pdf']);">Japanese</a>)</div>
<div><img src="images/pdf.png" alt="pdf-icon" /> Gura Developer's Manual
(<a href="https://github.com/gura-lang/gura-doc/blob/master/gura-dev-j.pdf?raw=true"
  onClick="_gaq.push(['_trackEvent','document','click','gura-dev-j.pdf']);">Japanese</a>)</div>
</p>

<h2>English</h2>

<em>I've decided to publish documents in English that I'm currently writing,
which is far from complete and being updated day by day.
I hope the publication will inspire me to carry on this tough work :-)</em>

<p>
<div><a href="documents/Introduction.html">Introduction</a></div>
<div>Chapter 1. <a href="documents/Launch-Program.html">Launch Program</a></div>
<div>Chapter 2. <a href="documents/Syntax.html">Syntax</a></div>
<div>Chapter 3. <a href="documents/Data-Type.html">Data Type</a></div>
<div>Chapter 4. <a href="documents/Operator.html">Operator</a></div>
<div>Chapter 5. <a href="documents/Environment.html">Environment</a></div>
<div>Chapter 6. <a href="documents/Interpreter.html">Interpreter</a></div>
<div>Chapter 7. <a href="documents/Function.html">Function</a></div>
<div>Chapter 8. <a href="documents/Flow-Control.html">Flow Control</a></div>
<div>Chapter 9. <a href="documents/Object-Oriented-Programming.html">Object Oriented Programming</a></div>
<div>Chapter 10. <a href="documents/Mapping-Process.html">Mapping Process</a></div>
<div>Chapter 11. <a href="documents/Module.html">Module</a></div>
<div>Chapter 12. String Operation</div>
<div>Chapter 13. File Operation</div>
<div>Chapter 14. Network Operation</div>
<div>Chapter 15. Image Operation</div>
<div>Chapter 16. Graphical User Interface</div>
<div>Chapter 17. Mathematic Functions</div>
<div>Chapter 18. Template Engine</div>
</p>

</div>

<div id="box-bottom">

</div>
