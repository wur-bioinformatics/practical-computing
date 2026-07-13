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

## What are Regular Expressions and why use them?
```{seealso} Computing Skills for Biologists - a Tool box
- Chapter 5.1 What Are Regular Expressions?
- Chapter 5.2 Why Use Regular Expressions?
```

{term}`Regular Expression`s are a sequence of characters that define a search pattern, mainly for use in pattern matching with strings, or string matching, i.e. 'find and replace'-like operations [@wikipedia_regular_2026]. {term}`Regular Expression`s are often used to find (and replace) patterns in text.

``````{important} Example
:class: simple
:icon: false

In the following -omics fields notice the pattern in the text:

<span style="color: #17cc4d;"> Gen</span><span style="color: #fb0c0c;">omics</span>\
<span style="color: #17cc4d;"> Transcript</span><span style="color: #fb0c0c;">omics</span>\
<span style="color: #17cc4d;"> Prote</span><span style="color: #fb0c0c;">omics</span>

This pattern can be captured by the following {term}`Regular Expression`: \
<span style="color: #17cc4d;"> \\w+</span><span style="color: #fb0c0c;">omics</span>
``````

## Components
{term}`Regular Expression`s are made up of a syntax that describes the search pattern. Here, we will discuss the most important components. 

### Wildcards and Metacharacters


### Boundaries

### Quantifiers

### Capturing (and Replacing)



## Glossary
```{glossary}
Regular Expression
: a sequence of characters that define a search pattern, mainly for use in pattern matching with strings, or string matching, i.e. 'find and replace'-like operations.
```
