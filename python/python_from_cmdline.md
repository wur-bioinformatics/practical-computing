---
title: Python from the Command Line
label: python_from_cmdline
abbreviations:
    
bibliography:
    python_from_cmdline.bib
---

```{important} Learning outcomes
After completing this section you should be able to:
- learning_outcome1
- learning_outcome2
```

## Introduction



:::{caution} Do not export the Jupyter Notebook as Python
The book advises to "export" the Jupyter notebook "as Python" (p135). However, this is a bad idea: a Jupyter Notebook contains more than just code (e.g. markdown and output cells). 

It is better to copy the whole program/script into a cell, then copy the content of that cell into a Python file (`.py`).
:::


## Python Script as Part of a Pipeline
[Previously](#section_alcap_pipelines), we have seen that we can build pipelines using command line tools. We can also use a Python script within a Bash pipeline:

```{code-block} bash
:class: no-copybutton
tool1 | python3 script.py | tool2
```
```{code-block} bash
:class: no-copybutton
cat in.txt | python3 script.py > out.txt
```
```{code-block} bash
:class: no-copybutton
python3 script.py < in.txt > out.txt
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
In [](#section_alcap_stdin_stdout_stderr), we saw that on the command line we have three data streams. This is similar when running a Python script from the command line. We can access {term}`stdin`, {term}`stdout`, and {term}`stderr` in our Python script with `sys.stdin`, `sys.stdout`, and `sys.stderr`, respectively [@geeksforgeeks_pythonsysmodule_2025]. They are file-like objects, and we can use [](#section_wwf_file_methods) on them.

`sys.stdin` reads input from the {term}`stdin` data stream. When using `input()`, the result (what is typed by the user) is actually stored in `sys.stdin`.

`sys.stdout` writes output to the {term}`stdout` data stream. We can do so by using `sys.stdout.write()` which works as if writing to a file. Namely, we can only write strings and we need to include newline characters explicitly. Additionally, we can write to the {term}`stdout` data stream by using [`print()`](#section_gswp_print). The advantages of `print()` are that it can take any data type, it prints arguments separated by spaces by default, and, when using multiple `print()` statements, the output is separated by newline characters. 

If the goal is to print something to screen, we must note that using `sys.stdout` only works when the Python script is singly run and not part of a pipeline. Namely, when we use a Python script in a pipeline, the output of `print()` is redirected to the next step or to a file. 


Alternatively, we can use `print()` and specify the file as `sys.stderr` to utilise that data stream:
```{code-block} python
:class: no-copybutton
print('Hello', 'World', file=sys.stderr)
```
`sys.stderr` writes to the {term}`stderr` data stream, thereby separating (error) messages from regular output. We can write to {term}`stderr` using `sys.stderr.write()`, which has similar constraints as `sys.stdout.write()` mentioned before. Whatever is written to `sys.stderr` goes to the console, i.e. it is written to screen/shown to the user. It is **not** sent to the next step in the pipeline.


## Usage String
When writing a script that takes command line arguments, it is best practice to include a usage string. This makes it clear to the user what is expected for each argument. 

For the usage string, we can use triple quotes (`"""`) to ensure the string can span multiple lines:
```{code-block} python
:filename: my_script.py
usage = """
Usage: my_script.py [options] <filename>
   or: my_script.py --help
   or: my_script.py ...
"""
```

It is possible to integrate this in such a way, that when retrieving the command line arguments goes wrong, the usage string is written to {term}`stderr`. 

## Special Variable `__name__`
A Python source file (script) has a special variable called `__name__` (with double underscores) which is assigned the name of the Python module by the interpreter [@geeksforgeeks___name___2022]. If the source file is executed as the main program, i.e. it is run from the command line, the `__name__` variable will have the value `'__main__'`. If the file is being imported in another module, the `__name__` variable will have the name of the module as value.

Because the `__name__` variable is a built-in variable, we can use it check whether the current script is being run on its own:
```{code-block} python
:filename: my_script.py
if __name__ == '__main__':
    # main code
```
This construction can be used to include code in the program that lives outside the function, class, and variable definitions. This code is then not executed when importing the module (because then the `__name__` variable does not equal `'__main__'`). It can also be used to run tests on the module. 

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 4.4 Python from the Command Line
```

## Exercises
The first exercise of today focuses on preparing a Python program to be part of a shell pipeline. This means that some outputs must go to {term}`standard output <stdout>` (function `print()`) for the next step in the pipeline, while other (typically diagnostic) outputs must still go to console. It also means that some inputs cannot be supplied by {term}`standard input <stdin>` (function `input()`). We will need command line arguments for that purpose.

In the second exercise, we make a program more flexible by replacing hard-coded filenames by names asked from the user. The actual input and output are
read from one file and written to another file.

The further assignments combine the aspects of the first two assignments. The last assignment is open-ended by design.

This time, we do not supply a Jupyter Notebook. For really working with files a notebook has its shortcomings, as you might have noticed with the first exercises on files. Working with command line arguments from a notebook is not possible at all (well, not reasonably).

::::{tip} For trying code fragments, you can create your own notebook
For testing command line arguments, `sys.argv` will only give the command line arguments of the Python system running in the notebook; not very usefull. For experimenting, you can create a variable `sys_argv`, like we did for line yesterday. Note that command line arguments are passed as a list of strings, and that the name of the script is in position 0 of the list.

::::

For testing the new aspects of today, you will have to write scripts in their own files, and execute those from the terminal window. Although it is possible to run programs with command line arguments inside PyCharm, it is far easier using the terminal when experimenting with command line arguments.


### Multiplication on the Console
``````{exercise} Multiplication on the console
**Write program `multiply.py` that takes one or more numbers as command line arguments, multiply all those numbers, and print the answer to console.** If the user does not supply any arguments, the program prints a usage message.

The program that you have to write for this exercise must take its inputs from the command line and print its output to the console. 

:::{tip}
Import `sys` and use `sys.argv` for accepting inputs. Remember that command line arguments are always supplied as strings.
:::

:::{tip}
For the multiplication, use a result variable that the program initializes to `1` – not `0` – before processing the numbers.
:::

:::{tip}
Output of `print()` goes to {term}`standard output <stdout>`. That is not what we want in this case. Instead, the output should go to `sys.stderr`.
:::

Some examples of how the program should run with its expected outputs:
```{code-block} bash
:class: no-copybutton
python3 multiply.py 2 3 4
24.0
```
```{code-block} bash
:class: no-copybutton
python3 multiply.py 4
4.0
```
The program should print the usage if no numbers are supplied as arguments:
```{code-block} bash
:class: no-copybutton
python3 multiply.py
usage: (<your text>)
```
Output should still go to the console if {term}`standard output <stdout>` is redirected (`>` or `>>`) or sent to another program by a pipe (`|`):
```{code-block} bash
:class: no-copybutton
python3 multiply.py 2 3 4 > data.out
24.0
```
```{code-block} bash
:class: no-copybutton
python3 multiply.py 4 5 < data.out
20.0
```
*nothing should be written in `data.out`*


What happens as a result of the following call depends on how intelligent you make your program. For a first version it is acceptable if the program just crashes.
```{code-block} bash
:class: no-copybutton
python3 multiply.py a b c
```

Optional: What happens if the user types non-numbers at the command-line? \
If you want the program to behave nicely in that case, put the part of the program that causes an error into a `try`-`except` block:
```{code-block} python
:filename: multiply.py
try:
    <statements causing the problem>
except:
    <alternative action; e.g. print usage>

```


``````


### File-based Version of Rosalind's RNA

Rosalind's RNA with Command Line Arguments

Rosalind’s RNA with advanced Command Line Arguments