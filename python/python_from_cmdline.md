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

### `sys.argv`
To access command line arguments supplied with a script, we can use `sys.argv`.

Imagine we use our script on the command line as follows:
```{code-block} bash
python3 my_script.py arg1 arg2 arg3
```
Where `arg1`, `arg2`, and `arg3` are command line arguments that will be used in our script.

`sys.argv` returns a list of strings. It contains the whole command that comes after `python3`, including the name of the script ([](#example_sys_argv_whole)).

(example_sys_argv_whole)=
``````{prf:example} Retrieve the whole command
In our script:
```{code-block} python
:filename: my_script.py
import sys
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
import sys
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

### `sys.stdin`, `sys.stdout`, and `sys.stderr`
In [](#section_alcap_stdin_stdout_stderr), we saw that on the command line we have three data streams. This is similar when running a Python script from the command line. We can access {term}`stdin`, {term}`stdout`, and {term}`stderr` in our Python script with `sys.stdin`, `sys.stdout`, and `sys.stderr`, respectively [@geeksforgeeks_pythonsysmodule_2025]. They are file-like objects, and we can use [](section_wwf_file_methods) on them.

`sys.stdin` reads input from the {term}`stdin` data stream. When using `input()`, the result (what is typed by the user) is actually stored in `sys.stdin`.

`sys.stdout` writes output to the {term}`stdout` data stream. We can do so by using `sys.stdout.write()` which works as if writing to a file. Namely, we can only write strings and we need to include newline characters explicitly. Additionally, we can write to the {term}`stdout` data stream by using `print()`. The advantages of [`print()`](#section_gswp_print) are that it can take any data type, it prints arguments separated by spaces by default, and, when using multiple `print()` statements, the output is separated by newline characters. 

If the goal is to print something to screen, we must note that using `sys.stdout` only works when the Python script is singly run and not part of a pipeline. Namely, when we use a Python script in a pipeline, the output of `print()` **is** redirected to the next step or to a file. 


Alternatively, we can use `print()` and specify the file as `sys.stderr` to utilise that data stream:
```{code-block} python
:class: no-copybutton
print('Hello', 'World', file=sys.stderr)
```
`sys.stderr` writes to the {term}`stderr` data stream, thereby separating (error) messages from regular output. We can write to {term}`stderr` using `sys.stderr.write()`, which has similar constraints as `sys.stdout.write()` mentioned before. Whatever is written to `sys.stderr` goes to the console, i.e. it is written to screen/shown to the user. It is **not** sent to the next step in the pipeline.



## Usage String
When writing a script that takes command line arguments, it is best practice to include a usage string. This makes it clear to the user what is expected for each argument. 

For the usage string, we can use triple quotes to ensure the string can span multiple lines:
```{code-block} python
:filename: my_script.py
usage = """
Usage: my_script.py [options] <filename>
   or: my_script.py --help
   or: my_script.py ...
"""
```

It is possible to integrate this that when retrieving the command line arguments goes wrong, the usage string is written to {term}`stderr`. 

## Testing 'name is main'

## Exercises


### Multiplication on the Console

### File-based Version of Rosalind's RNA

Rosalind's RNA with Command Line Arguments

Rosalind’s RNA with advanced Command Line Arguments