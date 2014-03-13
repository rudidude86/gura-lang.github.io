---
layout: page
lang: en
title: Operator
---

# {{ page.title }}

## About Operator

There are three types of Operators.

* **Prefixed Unary Operator** takes an input value specified after it.
* **Suffixed Unary Operator** takes an input value specified before it.
* **Binary Operator** takes two input values specified on both sides of them.

Users can define Operator's function through `operator` class.


## Standard Operators

This section describes about operators that are predefined.

Operation `+x` returns the value of `x` itself.

<table>
<tr><th>Operation</th><th>Result Data Type</th></tr>
<tr><td><code>+number</code></td><td><code>number</code></td></tr>
<tr><td><code>+complex</code></td><td><code>complex</code></td></tr>
<tr><td><code>+matrix</code></td><td><code>matrix</code></td></tr>
</table>


Operation `-x` returns a negaive value of `x`.

<table>
<tr><th>Operation</th><th>Result Data Type</th></tr>
<tr><td><code>-number</code></td><td><code>number</code></td></tr>
<tr><td><code>-complex</code></td><td><code>complex</code></td></tr>
<tr><td><code>-matrix</code></td><td><code>matrix</code></td></tr>
</table>


Operation `~x` returns a bit-inverted value of `x`.

<table>
<tr><th>Operation</th><th>Result Data Type</th></tr>
<tr><td><code>~number</code></td><td><code>number</code></td></tr>
</table>


Operation `!x` returns a logically inverted value of `x`
after evaluating it as a boolean value.

<table>
<tr><th>Operation</th><th>Result Data Type</th></tr>
<tr><td><code>!any</code></td><td><code>boolean</code></td></tr>
</table>


Operation `x..` returns an infinite iterator
that starts from `x` and is increased by one.

<table>
<tr><th>Operation</th><th>Result Data Type</th></tr>
<tr><td><code>number..</code></td><td><code>iterator</code></td></tr>
</table>


Operation `x?` returns `false` if `x` is `false` or `nil`, and `true` otherwise.
This operator is not affected by Implicit Mapping
and returns `true` if `x` is of `list` or `iterator` type.

<table>
<tr><th>Operation</th><th>Result Data Type</th></tr>
<tr><td><code>any?</code></td><td><code>boolean</code></td></tr>
</table>


Operation `x + y` returns an added result of `x` and `y`.

<table>
<tr><th>Operation</th><th>Result Data Type</th></tr>
<tr><td><code>number + number</code></td><td><code>number</code></td></tr>
<tr><td><code>number + complex</code></td><td><code>complex</code></td></tr>
<tr><td><code>number + rational</code></td><td><code>rational</code></td></tr>
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

Operation `x - y` returns a subtracted result of `x` and `y`.

<table>
<tr><th>Operation</th><th>Result Data Type</th></tr>
<tr><td><code>number - number</code></td><td><code>number</code></td></tr>
<tr><td><code>number - complex</code></td><td><code>complex</code></td></tr>
<tr><td><code>number - rational</code></td><td><code>rational</code></td></tr>
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

Operation `x * y` returns a multiplied result of `x` and `y`.

<table>
<tr><th>Operation</th><th>Result Data Type</th></tr>
<tr><td><code>number * number</code></td><td><code>number</code></td></tr>
<tr><td><code>number * complex</code></td><td><code>complex</code></td></tr>
<tr><td><code>number * rational</code></td><td><code>rational</code></td></tr>
<tr><td><code>complex * number</code></td><td><code>complex</code></td></tr>
<tr><td><code>complex * complex</code></td><td><code>complex</code></td></tr>
<tr><td><code>complex * rational</code></td><td>(error)</td></tr>
<tr><td><code>rational * number</code></td><td><code>rational</code></td></tr>
<tr><td><code>rational * complex</code></td><td>(error)</code></td></tr>
<tr><td><code>rational * rational</code></td><td><code>rational</code></td></tr>
<tr><td><code>matrix * matrix</code></td><td><code>matrix</code></td></tr>
<tr><td><code>matrix * list</code></td><td><code>list</code></td></tr>
<tr><td><code>list * matrix</code></td><td><code>list</code></td></tr>
<tr><td><code>timedelta * number</code></td><td><code>timedelta</code></td></tr>
<tr><td><code>number * timedelta</code></td><td><code>timedelta</code></td></tr>
</table>

Applying `*` operator between `string`/`binary` and `number`
will join the `string`/`binary` for `number` times.

<table>
<tr><th>Operation</th><th>Result Data Type</th></tr>
<tr><td><code>string * number</code></td><td><code>string</code></td></tr>
<tr><td><code>number * string</code></td><td><code>string</code></td></tr>
<tr><td><code>binary * number</code></td><td><code>binary</code></td></tr>
<tr><td><code>number * binary</code></td><td><code>binary</code></td></tr>
</table>

Operation `x / y` returns a divided result of `x` and `y`.

<table>
<tr><th>Operation</th><th>Result Data Type</th></tr>
<tr><td><code>number / number</code></td><td><code>number</code></td></tr>
<tr><td><code>number / complex</code></td><td><code>complex</code></td></tr>
<tr><td><code>number / rational</code></td><td><code>rational</code></td></tr>
<tr><td><code>complex / number</code></td><td><code>complex</code></td></tr>
<tr><td><code>complex / complex</code></td><td><code>complex</code></td></tr>
<tr><td><code>complex / rational</code></td><td>(error)</td></tr>
<tr><td><code>rational / number</code></td><td><code>rational</code></td></tr>
<tr><td><code>rational / complex</code></td><td>(error)</code></td></tr>
<tr><td><code>rational / rational</code></td><td><code>rational</code></td></tr>
<tr><td><code>matrix / matrix</code></td><td><code>matrix</code></td></tr>
</table>

Operation `x % y` returns a remainder after dividing `x` by `y`.

<table>
<tr><th>Operation</th><th>Result Data Type</th></tr>
<tr><td><code>number % number</code></td><td><code>number</code></td></tr>
</table>

Operation `x ** y` returns a powered result of `x` and `y`.

<table>
<tr><th>Operation</th><th>Result Data Type</th></tr>
<tr><td><code>number ** number</code></td><td><code>number</code></td></tr>
<tr><td><code>number ** complex</code></td><td><code>complex</code></td></tr>
<tr><td><code>complex ** number</code></td><td><code>complex</code></td></tr>
<tr><td><code>complex ** complex</code></td><td><code>complex</code></td></tr>
</table>

Operation `x == y` returns `true` when `x` equals to `y`, and `false` otherwise.

<table>
<tr><th>Operation</th><th>Result Data Type</th></tr>
<tr><td><code>any == any</code></td><td><code>boolean</code></td></tr>
</table>

Operation `x < y` returns `true` when `x` is less than `y`, and `false` otherwise.

<table>
<tr><th>Operation</th><th>Result Data Type</th></tr>
<tr><td><code>any < any</code></td><td><code>boolean</code></td></tr>
</table>

Operation `x > y` returns `true` when `x` is greater than `y`, and `false` otherwise.

<table>
<tr><th>Operation</th><th>Result Data Type</th></tr>
<tr><td><code>any > any</code></td><td><code>boolean</code></td></tr>
</table>

Operation `x <= y` returns `true` when `x` is less than or equal to `y`, and `false` otherwise.

<table>
<tr><th>Operation</th><th>Result Data Type</th></tr>
<tr><td><code>any <= any</code></td><td><code>boolean</code></td></tr>
</table>

Operation `x >= y` returns `true` when `x` is greater than or equal to `y`, and `false` otherwise.

<table>
<tr><th>Operation</th><th>Result Data Type</th></tr>
<tr><td><code>any >= any</code></td><td><code>boolean</code></td></tr>
</table>

Operation `x <=> y` returns `0` when `x` is equal to `y`,
`-1` when `x` is less than `y` and `1` when `x` is greater than `y`.

<table>
<tr><th>Operation</th><th>Result Data Type</th></tr>
<tr><td><code>any <=> any</code></td><td><code>number</code></td></tr>
</table>

Operation `x in y` checks if `x` is contained in `y`.

When Operator `in` takes a value of any type other than `list` and `iterator` at its left,
it will check if the value is contained in the container specified at its right.
If the right value is not of `list` or `iterator`,
it would act in the same way as Operator `==`.

<table>
<tr><th>Operation</th><th>Result Data Type</th></tr>
<tr><td><code>any in list</code></td><td><code>boolean</code></td></tr>
<tr><td><code>any in iterator</code></td><td><code>boolean</code></td></tr>
<tr><td><code>any in any</code></td><td><code>boolean</code></td></tr>
</table>

When Operator `in` takes a value of `list` or `iterator` type at its left,
it will check if each value of the container's element is contained in the container
specified at its right,
and return a list of `boolean` indicating the result of each containing check.

<table>
<tr><th>Operation</th><th>Result Data Type</th></tr>
<tr><td><code>list in list</code></td><td><code>list</code></td></tr>
<tr><td><code>list in iterator</code></td><td><code>list</code></td></tr>
<tr><td><code>list in any</code></td><td><code>list</code></td></tr>
<tr><td><code>iterator in list</code></td><td><code>list</code></td></tr>
<tr><td><code>iterator in iterator</code></td><td><code>list</code></td></tr>
<tr><td><code>iterator in any</code></td><td><code>list</code></td></tr>
</table>


Operation `x & y` returns an AND calculation result of `x` and `y`.

Operation `x | y` returns an OR calculation result of `x` and `y`.

Operation `x ^ y` returns a XOR calculation result of `x` and `y`.


Operation `x << y` returns a value of `x` shifted left by `y` bits.

Operation `x >> y` returns a value of `x` shifted right by `y` bits.


Operation `x || y`


Operation `x && y`


Operation `x .. y`

Operation `x => y`


## User-defined Operator

You can define Operators' functions through `operator` class.

