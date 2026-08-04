---
title: Modules and Libraries
label: modules_and_libraries
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
- Chapter 4.2.2 Importing Packages and Modules
- Chapter 5.3 Regular Expressions in Python
- Chapter 5.5 Functions of the `re` Module
```

## Modules, Libraries, Importing
In [](#section_wf_modules), we have already seen what modules and libraries are in Python. Here, we will expand on that with more ways of importing, and elaborating on Python Standard Libraries and third-party libraries.


### Importing
To be able to use the functionalities of modules and libraries, we first need to import them. For completeness, we have added the ones already discussed in [](#section_wf_importing_a_module):

```{code-block} python
:class: no-copybutton
import module_name
```
```{code-block} python
:class: no-copybutton
from module_name import feature
```

While importing, we can change the name of the module:
```{code-block} python
:class: no-copybutton
import module_name as my_name
```
There are many standard abbreviations. For example: `import numpy as np`.


We can also rename features while importing:
```{code-block} python
:class: no-copybutton
from module_name import feature as ftr
```
This is sometimes useful for redefining.


We can import a limited number of features:
```{code-block} python
:class: no-copybutton
from module_name import f1, f2, f3, f4
```

We can import all names from a module in the current name space:
```{code-block} python
:class: no-copybutton
from module_name import *
```
:::{caution} Do not import all names in the current name space
In general, it is advised against importing all names from a module in the current name space. If you have names already defined in your name space that are the same as some from the module, you will overwrite them.
:::


```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 4.2.2 Importing Packages and Modules
```


### Python Standard Libraries
In the design philosophy of Python, it was decided to keep the core of the language simple and lean. There are many advantages to this, which include transparency, ease of maintaining the language, and ease of learning the language.  

The list of built-in functions in Python is very limited, and the remainder of the functionality of the core language is built into its objects, by means of methods of strings, lists, dictionaries, and some more primary data structures.

But, obviously, sometimes we need a bigger toolbox. And Python does provide that too. Any basic installation of Python includes the so called 'standard library' - modules that are a standard part of Python but do not belong to the core of the language.  

A list of modules that are present in any Python installation by default can be found [here](https://docs.python.org/3/library/index.html).

Among these modules are tools to interact with the {term}`operating system`, with files and {term}`file systems <file system>`, do mathematical operations, {term}`regular expressions<regular expression>`, random number generation, and many, many more tools that may not be relevant right now, but could become indispensible tools for you at some later stage. Some of them are listed in [](#table_standard_libraries).


(table_standard_libraries)=
:::{list-table} Some useful Python standard libraries
* - Standard library
  - Description
* - `math`
  - Mathematical functions
* - `random` 
  - Generating pseudo-random numbers
* - `re`
  - Regular expression operations
* - `sys`
  - System-specific parameters and functions
* - `os`
  - Miscellaneous operating system interfaces
* - `urllib`
  - Open arbitrary resources by URL
* - `time`
  - Time access and conversions
* - `datetime`
  - Basic date and time types
* - `csv`
  - CSV file Reading and Writing
* - `argparse`
  - Parsing Command Line Options and Arguments
* - `json`
  - JSON encoder and decoder
:::


### Third-Party Libraries
There are many more modules and libraries available that are not included by default. They are external or third-party libraries and sometimes need to be installed separately by an installation manager (e.g. conda or pip). 

In this course, we use an Anaconda distribution that already provides some third-party libraries (e.g. `NumPy` and `Pandas`) because they are so commonly used. Some of the third-party libraries that we will use later in this course are listed in [](#table_third_party_libraries).

(table_third_party_libraries)=
:::{list-table} Some useful third-party libraries
* - Third-party library
  - Description
* - `NumPy`
  - Numerical and scientific computing (short for **Num**erical **Py**thon)
* - `Pandas` 
  - Data analysis and manipulation, built on top of NumPy, features data structures to handle spreadsheet-like data
* - `matplotlib`
  - Data visualization 
* - `Seaborn`
  - Data visualization 
* - `SciPy`
  - Extension of NumPy to perform advanced mathematical, scientific and engineering computing (short for **Sci**entific **Py**thon)
* - `BioPython`
  - Working with sequences, interfacing to standard bioinformatics tools
* - `MySQLdb`
  - Interfacing to relational databases
:::


## Module `re`
In [week 1](#regular_expressions), we have seen {term}`regular expressions<regular expression>` on the command line. The tools that can use {term}`regular expressions<regular expression>` are very powerful and efficient. However, when we want to do pattern matching in the middle of a Python program, calling these tools is not easily done. Instead, we can use {term}`**r**egular **e**xpressions<regular expression>` in Python with the standard module `re`. The `re` module offers functions and methods for performing pattern mathcing within the context of a Python program. 

The {term}`regular expression<regular expression>` syntax is the same as for the Linux tools. If you need a refresh head to: [](#regular_expressions). 

The {term}`regular expression<regular expression>` when using the `re` module can be written in a Python string. Here, we also need to {term}`escape` special characters. In the Python string, the back slashes (and quotes) need to be escaped ([](#example_re_python_string)). Instead, we can also use "**r**aw" strings, denoted as `r''` ([]#).

(example_re_python_string)=
``````{prf:example} Regular expression written in a Python string
```{code-block} python
pattern = '\\(\\w*\\[\\d+\\]\\)'
```

``````
(example_re_raw_string)=
``````{prf:example} Regular expression written in a raw string
```{code-block} python
pattern = r'\(\w*\[\d+\]\)'
```
``````


### Functions

### Classes



## Exercises

### Introduction to Module `re`

### Pattern Matching
refining ORF

### Reading FASTA files - Revisited

### Combining FASTA and ORF

### Parsing Command Line Options and Arguments