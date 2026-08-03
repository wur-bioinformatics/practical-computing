---
title: Writing Functions
label: writing_fuctions
abbreviations:
    
bibliography:
    .bib
---

```{important} Learning outcomes
After completing this section you should be able to:
- learning_outcome1
- learning_outcome2
```

## Introduction

## Functions
Functions can be seen as building blocks of a program. They take some input, do something with the input, and produce some output. Functions help make programs gain a clear structure and make them modular. 

### Defining Functions
A function can be defined according to the function header and the function body. Let's illustrate this with a very simple function that returns the sum of two numbers.

First, let's write the function header:

```{code-block} python
:class: no-copybutton
:linenos:
:emphasize-lines: 1
def sum_of_two_numbers(number1, number2):
    ...
```
The function header in line 1 contains:
- the keyword `def` to indicate something is being **def**ined
- the `sum_of_two_numbers` which is the name of the function, this is what we use when we call the function
- parentheses `()` that enclose the function parameters (here: `number1` and `number2`), these are the input
- the colon `:`

Now, let's write the function body:

```{code-block} python
:class: no-copybutton
:linenos:
:emphasize-lines: 2,3
def function_name(number1, number2):
    sum12 = number1 + number2
    return sum12
```
The function body contains:
- in line 2:
  - statements, indented relative to function header
  - parameters for values into function
- in line 3:
  - a `return` statement that specifies what the output the function **return**s

The function body is self-contained, meaning the code will only be executed if the function is called.

In [](#example_defining_a_function_subs), we rewrite the code for solving the Rosalind SUBS problem into a function.


(example_defining_a_function_subs)=
``````{prf:example} Solving SUBS using code without or with a function
:::::{grid} 2 2 2 2

::::{grid-item}
Code without a function
:::{code} python
s = input('s:')
t = input('t:')
n = len(t)
locs = []
for i in range(len(s)-n+1):
    if s[i:i+n] == t:
locs += [i+1]
print(locs)
:::
::::

::::{grid-item}
Code with a function
:::{code} python
def solve_subs(s, t):
    n = len(t)
    locs = []
    for i in range(len(s)-n+1):
        if s[i:i+n] == t:
            locs += [i+1]
    return locs

:::
Note that here we do not use the `input()` and `print()` functions.
::::
:::::
``````



### Applying Functions

## Modules

### Making Your Own Modules

## Standard Libraries

## Exercises

### Defining a Function

### Turning a Script into a Module

### Generating Random DNA Sequences

### Modules as Building Blocks