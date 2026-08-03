---
title: Writing Functions
label: writing_fuctions
abbreviations:
    
bibliography:
    writing_functions.bib
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
Applying, or calling, a self-defined function is exactly as for standard functions. The whole call is a (sub-)formula: we can assign the result to a variable, or use it in a larger formula. The previously defined `sum_of_two_numbers` can be called as follows:

```{code-block} python
:class: no-copybutton
sum_of_two_numbers(3,6)
```
The function call contains the elements:
- the function name (here: `sum_of_two_numbers`)
- parentheses `()`
- between the parentheses: arguments, one per parameter (here: `3,6`), separated with commas, can be any formula

We can apply the function in [](#example_defining_a_function_subs) in [](#example_applying_a_function_subs). We can also rewrite the conversion to a string in [](#example_applying_a_function_subs) into a function ([](#example_define_apply_str_locs)).

(example_applying_a_function_subs)=
``````{prf:example} Apply function for SUBS
First, let's ask the user for input for the DNA and the motif:
```{code-block} python
dna = input('dna = ')
motif = input('motif = ')
```
Then, let's apply the function `solve_subs()` defined before:
```{code-block} python
locations = solve_subs(dna, motif)
```
Last, let's create the desired output by printing:
```{code-block} python
str_locs = [str(loc) for loc in locations]
print(' '.join(str_locs))
```
``````

(example_define_apply_str_locs)=
``````{prf:example} Turn the string conversion into a function for SUBS
The first part is the same as in [](#example_applying_a_function_subs), we ask the user for input DNA and motif:
```{code-block} python
dna = input('dna = ')
motif = input('motif = ')
```
Then, we call `solve_subs()`:
```{code-block} python
locations = solve_subs(dna, motif)
```

Now, let's define `str_locs()`, a function to turn the locations into strings:
```{code-block} python
def str_locs(locs):
    locations = []
    for loc in locs:
        locations += [str(loc)]
    return locations

```
Last, let's call `str_locs()` and print the output:
```{code-block} python
print(' '.join(str_locs(locations)))
```
``````

Not all functions create a result, meaning they do not contain a `return` statement. By default the function then returns `None`. The function call can be seen as a command on its own. This is useful for complicated printing routines ([](#example_function_without_return)). The print statements are then inside the function instead of returning something and then printing that. Alternatively, this is used for filling data into a list or dictionary. The list or dictionary is one of the parameters and is edited in-place instead of returning. *#! is this correct?*

(example_function_without_return)=
``````{prf:example} Write a printing function for SUBS
Let's define a function that prints numbers:
```{code-block} python
def print_numbers(numbers):
    str_numbers = [str(n) for n in numbers]
    print(' '.join(str_numbers)
```
Again, ask the user for input:
```{code-block} python
dna = input('dna = ')
motif = input('motif = ')
```
Then, we call `solve_subs()`:
```{code-block} python
locations = solve_subs(dna, motif)
```

Last, we call `print_numbers()` to print the output:
```{code-block} python
print_numbers(locations)
```
``````

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 4.2.1 Writing Functions
```

## Modules, Libraries, and Importing
A module is a Python source file (meaning it is executable) containing definitions and statements. It is used to define functions (e.g. `re.search()`), classes (e.g. `re.Match`), and variables (e.g. `math.pi`) [@geeksforgeeks_pythonmodules_2026]. In Python: module ≈ library. Some "libraries" consist of multiple modules. 

There are multiple ways to import a module, some are:
```{code-block} python
:class: no-copybutton
import module_name
```
```{code-block} python
:class: no-copybutton
from module_name import feature
```


```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 4.2.2 Importing Packages and Modules
```

### Making Your Own Modules
You can create your own module by creating a Python source file ([](#example_define_module_subs)). Inside the module, only include definitions for functions, classes, and variables. Do not write code outside these definitions and do not include a 'main' program, this will be executed when importing which is undesirable. 

Creating your own modules can help organize your code and make it reusable.

You can use your created module similarly to standard and third-party modules by importing it ([](#example_import_module_subs_1), [](#example_import_module_subs_2)). 

If your module is called `my_utils.py`, use it by:
```{code-block} python
:class: no-copybutton
import my_utils
```

:::{note} When importing a module, do not include the `.py` extension.
:::

:::{note} When importing a module, write the path to the Python source file when it is not in the same directory as the script you are importing it into.
:::

(example_define_module_subs)=
``````{prf:example} Define a module for SUBS
Let's turn the `solve_subs()` function from [](#example_defining_a_function_subs) into a module:

```{code-block} python
:filename: rosalind_subs_solver.py
def solve_subs(s, t):
    n = len(t)
    locs = []
    for i in range(len(s)-n+1):
        if s[i:i+n] == t:
            locs += [i+1]
    return locs
```
``````

(example_import_module_subs_1)=
``````{prf:example} Import a module for SUBS 1
To use the SUBS module ([](#example_define_module_subs)), we can import it as a whole:
```{code-block} python
import rosalind_subs_solver
```
Ask the user for input:
```{code-block} python
dna = input('dna = ')
motif = input('motif = ')
```
Then, we can call `solve_subs()` by first specifing the module and then a dot (`.`) and the function name:
```{code-block} python
locs = rosalind_subs_solver.solve_subs(dna, motif)
```
Last, we print the output:
```{code-block} python
str_locs = [str(loc) for loc in locs]
print(' '.join(str_locs))
```
``````


(example_import_module_subs_2)=
``````{prf:example} Import a module for SUBS 2
To use the `solve_subs()` function from the SUBS module ([](#example_define_module_subs)), we can import it directly:
```{code-block} python
from rosalind_subs_solver import solve_subs
```
Ask the user for input:
```{code-block} python
dna = input('dna = ')
motif = input('motif = ')
```
Then, we can call `solve_subs()` as is:
```{code-block} python
locs = solve_subs(dna, motif)
```
Last, we print the output:
```{code-block} python
str_locs = [str(loc) for loc in locs]
print(' '.join(str_locs))
``````


## Standard Libraries

## Exercises

### Defining a Function

### Turning a Script into a Module

### Generating Random DNA Sequences

### Modules as Building Blocks