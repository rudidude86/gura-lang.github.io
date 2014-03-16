---
layout: page
lang: en
title: Interpreter
chapter: 5
---

# {{ page.chapter }}. {{ page.title }}

## {{ page.chapter }}.1. How Interpreter Works

The interpreter works with expressions and has two stages **evaluation** and **assignment**.


## {{ page.chapter }}.2. Evaluation Stage

### {{ page.chapter }}.2.1. Evaluation of Value

### {{ page.chapter }}.2.2. Evaluation of Identifier

### {{ page.chapter }}.2.3. Evaluation of Suffixed

### {{ page.chapter }}.2.4. Evaluation of UnaryOp

### {{ page.chapter }}.2.5. Evaluation of Quote

### {{ page.chapter }}.2.6. Evaluation of BinaryOp

### {{ page.chapter }}.2.7. Evaluation of Assign

### {{ page.chapter }}.2.8. Evaluation of Member

### {{ page.chapter }}.2.9. Evaluation of Lister

### {{ page.chapter }}.2.10. Evaluation of Iterer

### {{ page.chapter }}.2.11. Evaluation of Block

### {{ page.chapter }}.2.12. Evaluation of Root

### {{ page.chapter }}.2.13. Evaluation of Indexer

### {{ page.chapter }}.2.14. Evaluation of Caller


## {{ page.chapter }}.3. Assignment Stage

Operation `x = y` assigns the value of `y` to `x`.

The expression of `x` may be one of `Identifer`, `Lister`, `Member`, `Indexer` and `Caller`.

### {{ page.chapter }}.3.1. Assignment for Identifier

### {{ page.chapter }}.3.2. Assignment for Lister

### {{ page.chapter }}.3.3. Assignment for Member

### {{ page.chapter }}.3.4. Assignment for Indexer

### {{ page.chapter }}.3.5. Assignment for Caller




### {{ page.chapter }}.3.6. Operator before Assignment

An Assignment operator can be combined with one of several other operators.

<table>
<tr><th>Assignment Form</th><th>Equivalent Code</th></tr>
<tr><td><code>x += y</code></td><td><code>x = x + y</code></td></tr>
<tr><td><code>x -= y</code></td><td><code>x = x - y</code></td></tr>
<tr><td><code>x *= y</code></td><td><code>x = x * y</code></td></tr>
<tr><td><code>x /= y</code></td><td><code>x = x / y</code></td></tr>
<tr><td><code>x %= y</code></td><td><code>x = x % y</code></td></tr>
<tr><td><code>x **= y</code></td><td><code>x = x ** y</code></td></tr>
<tr><td><code>x &= y</code></td><td><code>x = x & y</code></td></tr>
<tr><td><code>x |= y</code></td><td><code>x = x | y</code></td></tr>
<tr><td><code>x ^= y</code></td><td><code>x = x ^ y</code></td></tr>
<tr><td><code>x <<= y</code></td><td><code>x = x << y</code></td></tr>
<tr><td><code>x >>= y</code></td><td><code>x = x >> y</code></td></tr>
</table>
