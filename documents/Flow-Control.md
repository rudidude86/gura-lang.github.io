---
layout: page
lang: en
title: Flow Control
chapter: 8
---

## {{ page.chapter }}. Flow Control


## {{ page.chapter }}.1. Branch

Branch may be the most common flow-control in a program.
Just like other programming language,
Gura also provides `if` - `elsif` - `else` sequence.
However, they're realized as functions, not as statements.

These elements are implemented by the following functions.

Function `if`:

    if (`cond):leader {block}

Function `elsif`:

    elsif (`cond):leader:trailer {block}

Function `else`:

    else():trailer {block}

They are concatenated with leader-trailer relationship,
which means that a closing curly bracket of the preceding function
must be in the same line as the top of the succceding one.

    if (x) { /* branch 1 */ } elsif (y) { /* branch 2 */ } else { /* branch 3 */ }

Of course, contents in the blocks may be written in multiple lines.
This enables you to write a program in a similar syntax as other languages.

    if (x) {
        
        /* branch 1 */
        
    } elsif (y) {
        
        /* branch 2 */
        
    } else {
        
        /* branch 3 */
        
    }




## {{ page.chapter }}.2. Repeat

## {{ page.chapter }}.2.1. `repeat`

    repeat (n?:number) {block}
    
## {{ page.chapter }}.2.2. `while`

    while (`cond) {block}
    
## {{ page.chapter }}.2.3. `for`

    for (`expr+) {block}

## {{ page.chapter }}.2.4. `cross`

    cross (`expr+) {block}

## {{ page.chapter }}.2.5. Flow Control in Repeat Sequence

    break
    
    continue
    

## {{ page.chapter }}.2.6. List Generation


## {{ page.chapter }}.2.7. Iterator Generation

    iterator#repeater()


## {{ page.chapter }}.3. Exception

    try - catch
    
    try():leader {block}
    catch(errors*:error):leader:trailer {block}
    
    raise(error:error, msg:string => 'error', value?)


