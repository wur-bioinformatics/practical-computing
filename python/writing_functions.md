---
title: Writing Functions and Modules
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
The function header in line **1** contains:
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
- in line **2**:
  - statements, indented relative to function header
  - parameters for values into function
- in line **3**:
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
Applying, or calling, a self-defined function is exactly as for standard functions. The whole call is a (sub-)formula: we can assign the result to a variable, or use it in a larger formula. The previously defined `sum_of_two_numbers()` can be called as follows:

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

(section_wf_modules)=
## Modules
A module is a Python source file (meaning it is executable) containing definitions and statements. It is used to define functions (e.g. `re.search()`), classes (e.g. `re.Match`), and variables (e.g. `math.pi`) [@geeksforgeeks_pythonmodules_2026]. In Python: module ≈ library. Some "libraries" consist of multiple modules. 

(section_wf_importing_a_module)=
### Importing a Module
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

### Writing a Module
You can create your own module by creating a Python source file ([](#example_define_module_subs)). Inside the module, only include definitions for functions, classes, and variables. Do not write code outside these definitions and do not include a 'main' program, this will be executed when importing which is undesirable. 

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

Creating your own modules can help organize your code and make it reusable. You can use your created module by importing it ([](#example_import_module_subs_1), [](#example_import_module_subs_2)). 

:::{note} Note
Keep in mind when importing your own module:
- Do not include the `.py` extension.
- Write the path to the Python source file (instead of the filename) when it is not in the same directory as the script you are importing it into.
:::


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


## Exercises
Like before, we use a Jupyter Notebook for these exercises. Here, we define the assignments. The Jupyter Notebook contains additional steps and hints. For some steps, you'll have to create code outside the Jupyter Notebook.

``````{exercise} Start the W2D4 Jupyter Notebook
Download the W2D4 Jupyter Notebook from Brightspace.

Just like previous days, run the notebook with `jupyter notebook` in the terminal.

The Jupyter Notebook contains all the instructions.
``````

In these exercises, we will use Python’s `import` statement for importing code from own scripts. If we make changes to the imported code, the Python
environment has to forget the previous version. 

In Jupyter Notebooks, the easiest way to do that is restarting the underlying system (the Kernel): \
{kbd}`Kernel` > {kbd}`Restart` \
In order to avoid confusion, better use:\
{kbd}`Kernel` > {kbd}`Restart & Clear Output`. 

After restarting the notebook, we can execute the `import` statement again. If you forget to restart, the notebook will still use
the old version of the imported code.

### Defining a Function
(exc_wf_gc_content_function)=
``````{exercise} (GC) GC Content - Defining a function
Create a Python function `gc_content` that takes a DNA sequence as its only argument and produces the GC content (as a percentage).

The code inside this function is essentially identical to the code written in the first session on Python ([](#exc_gswp_gc_content)). Only, the function does not do `input` and `print`. Instead, the function receives the DNA sequence in its parameter, and returns the result by a `return` statement.

After the function definition, the Python script can use `input` and `print` for communication with the user. That Python script will call function `gc_content` to
perform the computation.
``````

(exc_wf_gc_content)=
### Turning a Script into a Module
``````{exercise} (GC) GC Content - Turning a script into a module
In theory, once we made function `gc_content`, it can be re-used in other Python scripts. If we want to avoid copying the code into each Python script where we need it, we can put the function in a re-usable program unit, or module.

A module is a Python file that contains function definitions, class definitions (not in this course), and potentially names for constant values (like `math.pi`). The name of the file before `.py` should be valid as an identifier in Python; that name occurs in the `import` statement for using the module.

For this exercise, create a module `gc_computation` that contains just function `gc_content` and nothing more. 

Create another script that imports this function, uses `input` and `print` for communication with the user, and calls the imported function for computing GC content.
``````

### Generating Random DNA Sequences
``````{exercise} Generating random DNA sequences
Using Python's module `random` and your own module `gc_computation`, generate random DNA sequences of a given length and count how many of them have a
GC content above a given threshold. Put the code for generating one random DNA sequence in a function.
``````

``````{exercise} Optional: Generating random DNA sequences using base-specific frequencies
In real life, DNA sequences do not have equal amounts of As, Cs, Gs, and Ts. Often, you'll find a skew towards higher AT content in genomes, at least in plants and animals. 

Modify your function for generating a random sequence so that it produces a DNA sequence with 60% chance for As and Ts and 40% chance for Cs and Gs.
``````


### Modules as Building Blocks
Here, we will do the (ORF) Open Reading Frames assignment from [Rosalind](https://rosalind.info/problems/locations/). There, the assignment is described as:

:::{card}
:header: (ORF) Open Reading Frames
Given a DNA string, write every distinct candidate protein string that can be translated from ORFs (open reading frames) of that DNA string. Outputs can be written in any order.

A DNA string has six reading frames, three resulting from the string itself and three resulting from its reverse complement.

An open reading frame (ORF) is a substring that starts with a start codon (AUG) and ends by a stop codon (one of UAA, UAG, UGA). Thus, a candidate protein string is derived by translating an open reading frame into amino acids until a stop codon is reached.

Sample input (simplified relative to Rosalind):
```{code-block} python
AGCCATGTAGCTAACTCAGGTTACATGGGGATGACCCCGCGACTTGGATTAGAGTCTCTTTTGGAATAAGCCTGAATGATCCGAGTAGCATCTCAG
```

Sample output:
```{code-block} python
:class: no-copybutton
MLLGSFRLIPKETLIQVAGSSPCNLS
M
MGMTPRLGLESLLE
MTPRLGLESLLE
```
:::

In previous assignments, we have created programs for REVC (Complementing a Strand of DNA), RNA (Transcribing DNA to RNA), PROT (Translating RNA to Protein), and SUBS (Finding a Motif in DNA). These pieces of code form the major building blocks for ORF (Open Reading Frames). With the use of functions, we can turn the programs for the sub-problems into modules, and write the program for ORF in terms of those modules.

(exc_wf_create_functions)=
``````{exercise} Create functions for REVC, RNA, PROT, and SUBS
Turn the fragments of code for REVC, RNA, PROT, and SUBS into functions.
``````

(exc_wf_create_modules)=
``````{exercise} Create modules for REVC, RNA, PROT, and SUBS
Define the functions for REVC, RNA, PROT, and SUBS each in their own module file.

Test the modules separately with scripts like in [](#exc_wf_gc_content).
``````

(exc_wd_orf)=
``````{exercise} (ORF) Open Reading Frames
After doing [](#exc_wf_create_functions) and [](#exc_wf_create_modules), we now have the building blocks to solve ORF.

The main script should do the following:
- call the function for REVC; then we have two strands
- call the function for RNA on these two strands
- call the function for SUBS to find start codons in RNA strands
- call the function for PROT on each substring that starts at a start codon
- for each protein string thus obtained, cut it at the first stop sign (* in the translated string); 
    - alternatively, find the stop codons in the RNA strand as well before calling the function for PROT
    - another alternative is changing the function for PROT to stop at a stop codon, but that would mean changing the PROT problem

This gives all candidate proteins. 

As a first approach, the script can print each candidate protein immediately when finding it. 

For the real ORF problem on Rosalind, we have to remove duplicates, so then we have to store all candidate proteins in a set (or list or dictionary).
``````