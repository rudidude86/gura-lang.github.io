---
layout: page
lang: en
title: Operator
---

# {{ page.title }}

Operation **`+x`** returns the value of `x` itself.

<table>
<tr><th>Operation</th><th>Result Data Type</th></tr>
<tr><td><code>+number</code></td><td><code>number</code></td></tr>
<tr><td><code>+complex</code></td><td><code>complex</code></td></tr>
<tr><td><code>+matrix</code></td><td><code>matrix</code></td></tr>
</table>


Operation **`-x`** returns a negaive value of `x`.

<table>
<tr><th>Operation</th><th>Result Data Type</th></tr>
<tr><td><code>-number</code></td><td><code>number</code></td></tr>
<tr><td><code>-complex</code></td><td><code>complex</code></td></tr>
<tr><td><code>-matrix</code></td><td><code>matrix</code></td></tr>
</table>


Operation **`~x`** returns a bit-inverted value of `x`.

<table>
<tr><th>Operation</th><th>Result Data Type</th></tr>
<tr><td><code>~number</code></td><td><code>number</code></td></tr>
</table>


Operation **`!x`** returns a logically inverted value of `x`
after evaluating it as a boolean value.

<table>
<tr><th>Operation</th><th>Result Data Type</th></tr>
<tr><td><code>!any</code></td><td><code>boolean</code></td></tr>
</table>


Operation **`x..`** returns an infinite iterator
that starts from `x` and is increased by one.

<table>
<tr><th>Operation</th><th>Result Data Type</th></tr>
<tr><td><code>number..</code></td><td><code>iterator</code></td></tr>
</table>


Operation **`x?`** returns `false` if `x` is `false` or `nil`, and `true` otherwise.
This operator is not affected by Implicit Mapping
and returns `true` if `x` is of `list` or `iterator` type.

<table>
<tr><th>Operation</th><th>Result Data Type</th></tr>
<tr><td><code>any?</code></td><td><code>boolean</code></td></tr>
</table>


Operation **`x + y`** returns an added result of `x` and `y`.

<table>
<tr><th>Operation</th><th>Result Data Type</th></tr>
<tr><td><code>number + number</code></td><td><code>number</code></td></tr>
<tr><td><code>number + complex</code></td><td><code>number</code></td></tr>
<tr><td><code>number + rational</code></td><td><code>number</code></td></tr>
<tr><td><code>complex + number</code></td><td><code>complex</code></td></tr>
<tr><td><code>complex + complex</code></td><td><code>complex</code></td></tr>
<tr><td><code>complex + rational</code></td><td>(error)</td></tr>
<tr><td><code>rational + number</code></td><td><code>rational</code></td></tr>
<tr><td><code>rational + complex</code></td><td>(error)</code></td></tr>
<tr><td><code>rational + rational</code></td><td><code>rational</code></td></tr>
<tr><td><code>matrix + matrix</code></td><td><code>matrix</code></td></tr>
<tr><td><code>datetime + timedelta</code></td><td><code>datetime</code></td></tr>
<tr><td><code>timedelta + datetime</code></td><td><code>datetime</code></td></tr>
<tr><td><code>timedelta + timedelta</code></td><td><code>timedelta</code></td></tr>
</table>

If `x` and `y` are of `string` or `binary` type,
operation `x + y` returns concatenated result of `x` and `y`.

<table>
<tr><th>Operation</th><th>Result Data Type</th></tr>
<tr><td><code>string + string</code></td><td><code>string</code></td></tr>
<tr><td><code>binary + binary</code></td><td><code>binary</code></td></tr>
<tr><td><code>string + binary</code></td><td><code>binary</code></td></tr>
<tr><td><code>binary + string</code></td><td><code>binary</code></td></tr>
<tr><td><code>string + any</code></td><td><code>string</code> (`any` will be converted to `string` before concatenation)</td></tr>
<tr><td><code>any + string</code></td><td><code>string</code> (`any` will be converted to `string` before concatenation)</td></tr>
</table>

Operation **`x - y`** returns a subtracted result of `x` and `y`.

<table>
<tr><th>Operation</th><th>Result Data Type</th></tr>
<tr><td><code>number - number</code></td><td><code>number</code></td></tr>
<tr><td><code>number - complex</code></td><td><code>number</code></td></tr>
<tr><td><code>number - rational</code></td><td><code>number</code></td></tr>
<tr><td><code>complex - number</code></td><td><code>complex</code></td></tr>
<tr><td><code>complex - complex</code></td><td><code>complex</code></td></tr>
<tr><td><code>complex - rational</code></td><td>(error)</td></tr>
<tr><td><code>rational - number</code></td><td><code>rational</code></td></tr>
<tr><td><code>rational - complex</code></td><td>(error)</code></td></tr>
<tr><td><code>rational - rational</code></td><td><code>rational</code></td></tr>
<tr><td><code>matrix - matrix</code></td><td><code>matrix</code></td></tr>
<tr><td><code>datetime - timedelta</code></td><td><code>datetime</code></td></tr>
<tr><td><code>datetime - datetime</code></td><td><code>timedelta</code></td></tr>
<tr><td><code>timedelta - timedelta</code></td><td><code>timedelta</code></td></tr>
</table>

