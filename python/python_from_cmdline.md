---
title: Python from the Command Line
label: python_from_cmdline
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

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 4.4 Python from the Command Line
```

:::{caution} Do not export the Jupyter Notebook as Python
The book advises to "export" the Jupyter notebook "as Python" (p135). However, this is a bad idea: a Jupyter Notebook contains more than just code (e.g. markdown and output cells). 

It is better to copy the whole program/script into a cell, then copy the content of that cell into a Python file (`.py`).
:::


## Python Script as Part of a Pipeline
We can run a Python script on the commandline as:
```{code-block} bash
:class: no-copybutton
python3 script.py
```




## Module `sys`
The `sys` module contains **sys**tem-specific parameters and functions. The module is especially useful for handling command line arguments, and reading input and writing output, but it has [more utilities](https://docs.python.org/3/library/sys.html) that we will not discuss here. 

We can import `sys` as seen [before](#section_mal_importing):
```{code-block} bash
import sys
```

### Command Line Arguments
To access command line arguments supplied with a script, we can use `sys.argv`.

Imagine we use our script on the command line as follows:
```{code-block} bash
python3 my_script.py arg1 arg2 arg3
```
Where `arg1`, `arg2`, and `arg3` are command line arguments that will be used in our script.

`sys.argv` returns a list of strings. It contains the whole command that comes after `python3` ([](#example_sys_argv_whole)).

(example_sys_argv_whole)=
``````{prf:example} Retrieve the whole command
In our script:
```{code-block} python
:filename: my_script.py
import argv
arguments = sys.argv
print(arguments)
```
Suppose we run our script on the command line:
```{code-block} bash
python3 my_script.py 2 "ATG"
```
Will give the output:
```{code-block} bash
:class: no-copybutton
['my_script.py', '2', 'ATG']
```
``````

We can also index `sys.argv`, with `sys.argv[0]` being the name of the script and the other elements the command line arguments and options ([](#example_sys_argv_index)). As with any other [list indexing](#section_list_indexing_and_slicing) `sys.argv[-1]` represents the last argument.

(example_sys_argv_index)=
::::{prf:example} Index `sys.argv` to obtain separate command line arguments
In our script:
```{code-block} python
:filename: my_script.py
import argv
n = sys.argv[1]
codon = sys.argv[2]

print(n)
print(codon)
```
Suppose we run our script on the command line:
```{code-block} bash
python3 my_script.py 2 "ATG"
```
Will give the output:
```{code-block} bash
:class: no-copybutton
2
ATG
```
::::

### Error Output

## Usage String

## Testing 'name is main'

## Exercises


### Multiplication on the Console

### File-based Version of Rosalind's RNA

Rosalind's RNA with Command Line Arguments

Rosalind’s RNA with advanced Command Line Arguments