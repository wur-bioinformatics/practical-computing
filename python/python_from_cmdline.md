---
title: Python from the command-line
label: python_from_cmdline
abbreviations:
    
bibliography:
    python_from_cmdline.bib
---

```{important} Learning outcomes
After completing this section you should be able to:
- Run a Python script from the command-line and supply command-line arguments.
- Use sys.argv to access command-line arguments and convert them into appropriate data types
- Use standard input, standard output and standard error to make a Python script suitable for use in a shell pipeline
```

## Introduction



:::{caution} Important
The book advises to "export" the Jupyter notebook "as Python" (p135). However, this is a bad idea: a Jupyter Notebook contains more than just code (e.g. markdown and output cells). 

It is better to copy the whole program/script into a cell, then copy the content of that cell into a Python file (`.py`).
:::

## Python Scripts from the Command-Line
Until now we mostly ran Python code from a notebook, a Python script stored in a `.py` file can also directory be executed from the shell. This works simply by invoking the python3 program and telling it which script to run:

```{code-block} bash
python3 my_script.py
```


## Python Script as Part of a Pipeline
[Previously](#section_alcap_pipelines), we have seen that we can build pipelines using command-line tools. We can also use a Python script within a Bash pipeline:

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
The `sys` module contains **sys**tem-specific parameters and functions. The module is especially useful for handling command-line arguments, and reading input and writing output, but it has [more utilities](https://docs.python.org/3/library/sys.html) that we will not discuss here. 

We can import `sys` as seen [before](#section_mal_importing):
```{code-block} bash
import sys
```

### `sys.argv`
To access command-line arguments supplied with a script, we can use `sys.argv`.

Imagine we use our script on the command-line as follows:
```{code-block} bash
python3 my_script.py arg1 arg2 arg3
```
Where `arg1`, `arg2`, and `arg3` are command-line arguments that will be used in our script.

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
Suppose we run our script on the command-line:
```{code-block} bash
python3 my_script.py 2 "ATG"
```
Will give the output:
```{code-block} bash
:class: no-copybutton
['my_script.py', '2', 'ATG']
```
``````

We can also index `sys.argv`, with `sys.argv[0]` being the name of the script and the other elements the command-line arguments and options ([](#example_sys_argv_index)). As with any other [list indexing](#section_list_indexing_and_slicing) `sys.argv[-1]` represents the last argument.

(example_sys_argv_index)=
::::{prf:example} Index `sys.argv` to obtain separate command-line arguments
In our script:
```{code-block} python
:filename: my_script.py
import sys
n = sys.argv[1]
codon = sys.argv[2]

print(n)
print(codon)
```
Suppose we run our script on the command-line:
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
In [](#section_alcap_stdin_stdout_stderr), we saw that on the command-line we have three data streams. This is similar when running a Python script from the command-line. We can access {term}`stdin`, {term}`stdout`, and {term}`stderr` in our Python script with `sys.stdin`, `sys.stdout`, and `sys.stderr`, respectively [@geeksforgeeks_pythonsysmodule_2025]. They are file-like objects, and we can use [](#section_wwf_file_methods) on them.

`sys.stdin` reads input from the {term}`stdin` data stream. `input()` reads a line from standard input (`sys.stdin`), for instance typed by the user, and returns it as a string.

`sys.stdout` writes output to the {term}`stdout` data stream. We can do so by using `sys.stdout.write()` which works as if writing to a file. We can only write strings and we need to explicitly include newline characters. Additionally, we can write to the {term}`stdout` data stream by using [`print()`](#section_gswp_print). The advantages of `print()` are that it can take any data type, it prints arguments separated by spaces by default, and, when using multiple `print()` statements, the output is separated by newline characters. 

If the goal is to print something to screen, we must note that using `sys.stdout` only works when the Python script is run separately and not part of a pipeline. When we use a Python script in a pipeline, the output of `print()` is redirected to the next step or to a file. 


Alternatively, we can use `print()` and specify the file as `sys.stderr` to utilise that data stream:
```{code-block} python
:class: no-copybutton
print('Hello', 'World', file=sys.stderr)
```
`sys.stderr` writes to the {term}`stderr` data stream, thereby separating (error) messages from regular output. We can write to {term}`stderr` using `sys.stderr.write()`, which has similar constraints as `sys.stdout.write()` mentioned before. Whatever is written to `sys.stderr` is by default **not** sent to the next step in the pipeline.


## Usage String
When writing a script that takes command-line arguments, it is best practice to include a usage string. This makes it clear to the user what is expected for each argument. 

For the usage string, we can use triple quotes (`"""`) to ensure the string can span multiple lines:
```{code-block} python
:filename: my_script.py
usage = """
Usage: my_script.py [options] <filename>
   or: my_script.py --help
   or: my_script.py ...
"""
```

This usage string can be printed to {term}`stderr` when there are no command-line arguments, or retrieving the command-line arguments goes wrong. 

## Standard layout of a Python script
As you have seen before, you can use a `.py` file also as a module. Then you do not run it directly, but instead import (some of) its functions to be able to use them in your Python code. To make every Python script usable both as a script as well as a module, it is common to put the central logic of the script also in a function called `main()` and only run that function if the `.py` file is used as a script. To detect how the `.py` file is used, we can make use of a global variable calle `__name__` (with double underscores) which is assigned the name of the Python module [@geeksforgeeks___name___2022]. If the `.py` is used as script, the `__name__` variable will have the value `'__main__'`. If the file is being imported as a module, the `__name__` variable will have the name of the module as value.

In the code can check the value of `__name__` to decide whether the `main()` function should be run:
```{code-block} python
:filename: my_script.py
def main():
    print('the program starts here')

if __name__ == '__main__':
    main()
```
Even if the `.py` file is intented to only be used as a module, this kind of logic can be used to run test functions included in the module. 

In general it is a good idea to put all your Python code inside a function, to properly organize it.

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 4.4 Python from the command-line
```

## Exercises
The first exercise of today focuses on preparing a Python program to be part of a shell pipeline. A program in a pipeline should use {term}`standard input <stdin>` (function `input()`) and {term}`standard output <stdout>` (function `print()`)  for data. Other information, like filenames or options, can instead be supplied as command-line arguments. Diagnostic messages can be writting to {term}`standard error <stderr>` so that they do not become part of the data stream.

In the second exercise, we make a program more flexible by replacing hard-coded filenames by names asked from the user. The actual input and output are
read from one file and written to another file.

The further assignments combine the aspects of the first two assignments. The last assignment is open-ended by design.

This time, we do not supply a Jupyter Notebook. For really working with files a notebook has its shortcomings, as you might have noticed with the first exercises on files. Working with command-line arguments from a notebook is not possible at all (well, not reasonably).

::::{tip} Tip
For trying code fragments, you can create your own notebook.

For testing command-line arguments, `sys.argv` will only give the command-line arguments of the Python system running in the notebook; not very useful. For experimenting, you can create a variable `sys_argv`, like we did for line yesterday. Note that command-line arguments are passed as a list of strings, and that the name of the script is in position 0 of the list.
::::

For testing the new aspects of today, you will have to write scripts in their own files, and execute those from the terminal window. You can write the scripts using PyCharm, which also includes a terminal view that you can use to experiment with command-line arguments.


### Multiplication on the Console
``````{exercise} Multiplication on the console
**Write program `multiply.py` that takes one or more numbers as command-line arguments, multiplies all those numbers, and print the answer to console.** If the user does not supply any arguments, the program prints a usage message.

The program that you have to write for this exercise should take its inputs from the command-line and print its output to the standard output. 

:::{tip} Tip
Import `sys` and use `sys.argv` for accepting inputs. Remember that command-line arguments are always supplied as strings.
:::

:::{tip} Tip
For the multiplication, use a result variable that the program initializes to `1` – not `0` – before processing the numbers.
:::

:::{tip} Tip
Output of `print()` goes to {term}`standard output <stdout>`. For errors and the usage message the output should go to `sys.stderr` which is not redirected by **>**.
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
```
```{code-block} bash
:class: no-copybutton
python3 multiply.py > data.out
usage: (<your text>)
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
    <statements that could cause an error>
except:
    <what to do if the error occurs; e.g. print usage>
```
``````


### File-based Version of Rosalind's RNA
[Rosalind](https://rosalind.info/problems/locations/) supplies its data as a text file that you have to download.

For results it has two options: typing/copying the answer into a text box or uploading a text file again.

Now that we know [how to process text files](#working_with_files), we can write our programs for solving Rosalind problems to read directly from the downloaded file and write its answer to an uploadable file.

``````{exercise} (RNA) Transcribing DNA to RNA - Python script
Take a solution for problem RNA (Transcribing DNA to RNA) and turn it into a file-based version. You can use your own solution or our file `rosalind_rna.py`.

The program should ask the user for the names of input file and output file (include suitable prompts). Then, the program reads the DNA string from the
input file specified, and it writes the corresponding RNA to the output file specified.
``````

``````{exercise} (RNA) Transcribing DNA to RNA - Python script using command-line arguments
*[extension of previous exercise]*\
Let the program take names of input file and output file from two command-line arguments. If the number of command-line arguments is not two, give a usage
message instead.
``````


``````{exercise} [optional] (RNA) Transcribing DNA to RNA - Python script using advanced command-line arguments
*[extension of previous exercise]*\
Further extend the script:
- If there are no command-line arguments, the program reads from {term}`standard input <stdin>` and writes to {term}`standard output <stdout>`.
- If the first command-line argument is `-f` (actually an {term}`option`), the program reads from file and writes to file;
  - If the user supplied the `-f` option but no filenames, the input filename should be `rosalind_rna.txt` and the output filename should be `rosalind_rna_out.txt`.
  - If there is a command-line argument after `-f`, it is the name of the input file. The output filename should be derived from the input file name by appending `_out` to the main part of the file name, i.e. before any file extension.
  - If there is another command-line argument after `-f` and the input filename, it is the name of the output file;
- In all other cases, the program should give a usage message.
``````
