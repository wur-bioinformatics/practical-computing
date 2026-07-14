---
title: Regular Expressions
label: regular_expressions
abbreviations:
    BLAST: Basic Local Alignment Search Tool
    RAM: Random Access Memory
bibliography:
    regular_expressions.bib
---

```{important} Learning outcomes
After completing this section you should be able to:
- be proficient in command line (shell) usage *#!this should be more specified I think*
```

## Introduction
In this section, you will learn about and practice with regular expressions, a powerful tool to find patterns in text.
*#! needs better introduction imo, also that it can be used on the cmdline and using python modules and that syntax can differ between languages*

## What are Regular Expressions and why use them?
```{seealso} Computing Skills for Biologists - a Tool box
- Chapter 5.1 What Are Regular Expressions?
- Chapter 5.2 Why Use Regular Expressions?
```

{term}`Regular Expressions <Regular Expression>` are a sequence of characters that define a search pattern, mainly for use in pattern matching with strings, or string matching, i.e. 'find and replace'-like operations [@wikipedia_regular_2026]. {term}`Regular Expressions <Regular Expression>` are often used to find (and replace) patterns in text, as can be seen in {numref}`Example %s <pattern_example>`.

``````{admonition} Patterns in text
:name: pattern_example
:numbered: true
:class: simple myst-example
:icon: false

In the following -omics fields notice the pattern in the text:

<span style="color: #17cc4d;"> Gen</span><span style="color: #fb0c0c;">omics</span>\
<span style="color: #17cc4d;"> Transcript</span><span style="color: #fb0c0c;">omics</span>\
<span style="color: #17cc4d;"> Prote</span><span style="color: #fb0c0c;">omics</span>

This pattern can be captured by the following {term}`Regular Expression`: \
<span style="color: #17cc4d;"> \\w+</span><span style="color: #fb0c0c;">omics</span>
``````

*#! Could be more about the "why"*


## Metacharacters
{term}`Regular Expressions <Regular Expression>` make use of a syntax that describes the search pattern. The syntax is made up of literal characters ({numref}`Example %s <normal_char_example>`) and {term}`metacharacters <metacharacter>`. A {term}`metacharacter` is a symbol with a special, non-literal meaning. Here, we will discuss the most important {term}`metacharacters <metacharacter>`: {term}`wildcards <wildcard>`, boundaries, and quantifiers, and how to make them literal (by escaping). 

``````{admonition} Normal characters match themselves
:name: normal_char_example
:numbered: true
:class: simple myst-example
:icon: false
A normal, or literal, character matches itself:

`a` matches 'a'

``````

### Wildcards
```{seealso} Computing Skills for Biologists - a Tool box
- Chapter 5.4.2 Metacharacters\*

\* Note: The book calls {term}`wildcards <wildcard>` "metacharacters", but we hold the definition that a {term}`metacharacter` is any symbol with a special, non-literal meaning and a {term}`wildcard` is a specific symbol that represents unknown or unimportant data.
```

{term}`Wildcards <wildcard>` match a range of different characters. An example of a {term}`wildcard` and what characters it matches is shown in {numref}`Example %s <word_char_example>`. 

``````{admonition} Wildcard that matches any 'word' character
:name: word_char_example
:numbered: true
:class: simple myst-example
:icon: false
The {term}`wildcard` `\w` matches any 'word' character:
- `\w` matches 'a'
- `\w` matches 'b'
- `\w` matches 'A'
- `\w` matches '5'

``````

The various {term}`wildcards <wildcard>` and the characters they match are listed in {numref}`wildcards_table`.

```{list-table} Wildcards
:header-rows: 1
:label: wildcards_table
* - Wildcard
  - Matches ...
  - Further information
* - `\n`
  - newline 
  - Line Feed or hexadecimal code: X0A
* - `\r`
  - carriage return
  - hexadecimal code: X0D
* - `\t`
  - TAB character
  - as in tab-delimited files (.tsv), in some editors visualised as '→'
* - `\s`
  - any whitespace
  - tabs and spaces
* - `\w`
  - any 'word' character 
  - alphabet + digits
* - `\d`
  - any digits
  - [0-9] *#! in slide says [1-9] but is zero not also a digit?*
* - `.`
  - any character
  - not `\n` or `\r` unless RE modified
* - `\W`
  - any non-word character
  - 
* - `\D`
  - any non-digit character
  - 
* - `\S`
  - any non-white space character
  - 
```

When we combine normal characters and {term}`wildcards <wildcard>`, we can create complex search patterns. Some examples are shown in {numref}`Example %s <pattern_matching_example_1>` and {numref}`Example %s <pattern_matching_example_2>`.

``````{admonition} The bear likes blueberries
:name: pattern_matching_example_1
:numbered: true
:class: simple myst-example
:icon: false

For the text:\
The bear likes blueberries

The pattern `b\w\wr` finds the following matches:\
The <span class="regex-match">bear</span> likes blue<span class="regex-match">berr</span>ies 

The pattern `\sb\w\wr\s` finds the following match:\
The<span class="regex-match">{sub}`_`bear{sub}`_`</span>likes blueberries

``````
``````{admonition} The bear likes to be rewarded with honey
:name: pattern_matching_example_2
:numbered: true
:class: simple myst-example
:icon: false

For the text:\
The bear likes to be rewarded with honey

The pattern `b\w\wr` finds the following match:\
The <span class="regex-match">bear</span> likes to be rewarded with honey

The pattern `b..r` finds the following matches:\
The <span class="regex-match">bear</span> likes to <span class="regex-match">be{sub}`_`r</span>ewarded with honey
``````

But what if you want to explicitly match a {term}`wildcard`? In {numref}`Example %s <escaping_wrong_example>` it is shown what happens if we don't alter the search pattern to account for the {term}`wildcard`. 


```{admonition} The blueberries are eaten by the bear. -- incorrect
:name: escaping_wrong_example
:numbered: true
:class: simple myst-example
:icon: false

For the following text, match `b\w\wr` but only if it occurs at the end of a sentence.\
The blueberries are eaten by the bear.

The pattern `b\w\wr.` finds the following match:\
The blue<span class="regex-match">berri</span>es are eaten by the <span class="regex-match">bear.</span>

This does not work as intended... 

**Can you think why this did not work?**
```





### Boundaries

### Quantifiers

## Capturing (and Replacing)



## Glossary
```{glossary}
Regular Expression
: a sequence of characters that define a search pattern, mainly for use in pattern matching with strings, or string matching, i.e. 'find and replace'-like operations.

metacharacter
: a symbol with a special, non-literal meaning.

wildcard
: a specific symbol that represents unknown or unimportant data.
```
