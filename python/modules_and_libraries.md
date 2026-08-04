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
:::{list-table}
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
Still, many more modules are included in the Anaconda distribution that we use in this course. Next week, we will be using modules (e.g. `numpy` and `pandas`) that are not strictly 'standard' but they are so commonly that Anaconda provides them without further preparations.


## Module `re`

### Functions

### Classes



## Exercises

### Introduction to Module `re`

### Pattern Matching
refining ORF

### Reading FASTA files - Revisited

### Combining FASTA and ORF

### Parsing Command Line Options and Arguments