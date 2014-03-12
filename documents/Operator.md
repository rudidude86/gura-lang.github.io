---
layout: page
lang: en
title: Operator
---

# {{ page.title }}

Operator **`+x`** returns the value of `x` itself.

<table>
<tr><th>Operation</th><th>Result Data Type</th></tr>
<tr><td><code>+number</code></td><td><code>number</code></td></tr>
<tr><td><code>+complex</code></td><td><code>complex</code></td></tr>
<tr><td><code>+matrix</code></td><td><code>matrix</code></td></tr>
</table>

Operator **`-x`** returns a negaive value of `x`.

<table>
<tr><th>Operation</th><th>Result Data Type</th></tr>
<tr><td><code>-number</code></td><td><code>number</code></td></tr>
<tr><td><code>-complex</code></td><td><code>complex</code></td></tr>
<tr><td><code>-matrix</code></td><td><code>matrix</code></td></tr>
</table>

Operator **`~x`** returns a bit-inverted value of `x`.

<table>
<tr><th>Operation</th><th>Result Data Type</th></tr>
<tr><td><code>~number</code></td><td><code>number</code></td></tr>
</table>

Operator **`!x`** returns a logically inverted value of `x`
after evaluating it as a boolean value.

<table>
<tr><th>Operation</th><th>Result Data Type</th></tr>
<tr><td><code>!any</code></td><td><code>boolean</code></td></tr>
</table>

Operator **`x..`** returns an infinite iterator
that starts from `x` and is increased by one.

<table>
<tr><th>Operation</th><th>Result Data Type</th></tr>
<tr><td><code>number..</code></td><td><code>iterator</code></td></tr>
</table>

Operator **`x?`** returns `false` if `x` is `false` or `nil`, and `true` otherwise.
This operator is not affected by Implicit Mapping
and returns `true` if `x` is of `list` or `iterator` type.

<table>
<tr><th>Operation</th><th>Result Data Type</th></tr>
<tr><td><code>any?</code></td><td><code>boolean</code></td></tr>
</table>
