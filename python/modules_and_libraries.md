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


## Modules, Libraries, Importing
In [](#section_wf_modules), we have already seen what modules and libraries are in Python. Here, we will expand on that with more ways of importing, and elaborating on Python Standard Libraries and third-party libraries.

(section_mal_importing)=
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
:header-rows: 1
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

The {term}`regular expression<regular expression>` when using the `re` module can be written in a Python string. In a Python string, we need to {term}`escape` characters such as dot (`.`), square brackets (`[]`), and parentheses (`()`). In addition, the back slashes (and quotes) need to be {term}`escaped<escape>` ([](#example_re_python_string)). Because we need to {term}`escape` so many characters, the pattern can become quite cluttered. Instead, we can use "**r**aw" strings, denoted as `r''` ([](#example_re_raw_string)).

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


### Functions and Classes
#### `re.search()` and `re.Match`
The `re` module contains several functions for pattern matching. The most basic one is `re.search()`:
```{code-block} python
:class: no-copybutton
m = re.search(pattern, string)
```
where `pattern` is the pattern you want to match, and `string` is the target string that you want to **search**. The result of a search is an `re.Match` object of the first match found ([](#example_re_search_match)) or `None` when no match is found ([](#example_re_search_nomatch)).

(example_re_search_match)=
::::{prf:example} `re.search()` returns a `re.Match` object when a match is found
Define a string:
```{code-block} python
s = 'Bananas are yellow'
```
Define the pattern:
```{code-block} python
p = r'yellow'
```
Search for a match:
```{code-block} python
m = re.search(p, s)
```
See what is in `m`:
```{code-block} python
print(m)
```
Will give the output:
```{code-block} python
:class: no-copybutton
<re.Match object; span=(12, 18), match='yellow'>
```
::::

(example_re_search_nomatch)=
::::{prf:example} `re.search()` returns `None` when no match is found
Define a string:
```{code-block} python
s = 'Bananas are yellow'
```
Define the pattern:
```{code-block} python
p = r'green'
```
Search for a match:
```{code-block} python
m = re.search(p, s)
```
See what is in `m`:
```{code-block} python
print(m)
```
Will give the output:
```{code-block} python
:class: no-copybutton
None
```
::::


#### `.group()`
As can be seen in ([](#example_re_search_match)), printing the `re.Match` object gives us information about the location of the match in the target string (`span=(12, 18)`) and the identified match (`match='yellow'`). Instead of printing the `re.Match` object, we can retrieve the identified match using the `.group()` method on the `re.Match` object ([](#example_re_group)).

(example_re_group)=
::::{prf:example} `.group()` method returns the identified match stored in an `re.Match` object
Define a string:
```{code-block} python
s = 'Bananas are yellow'
```
Define the pattern:
```{code-block} python
p = r'yellow'
```
Search for a match:
```{code-block} python
m = re.search(p, s)
```
Retrieve the match in `m`:
```{code-block} python
m.group()
```
Will give the output:
```{code-block} python
:class: no-copybutton
'yellow'
```
::::

#### `re.match()`
To only search for a **match** at the beginning of a string, we can use `re.match()`:
```{code-block} python
:class: no-copybutton
m = re.match(pattern, string)
```
It returns an `re.Match` object if zero or more characters at the beginning of the `string` match the `pattern` and `None` when the `string`  does not match the `pattern` ([](#example_re_match)).

(example_re_match)=
::::{prf:example} `re.match()` function returns the identified match when it is at the beginning of a string
Define a string:
```{code-block} python
s = 'Bananas are yellow when ripe. Bananas are green when unripe'
```
Define the pattern:
```{code-block} python
p = r'Bananas'
```
Search for a match only at the beginning of the string:
```{code-block} python
m = re.match(p, s)
```
Retrieve the match in `m`:
```{code-block} python
m.group()
```
Will give the output:
```{code-block} python
:class: no-copybutton
'Bananas'
```

Suppose the following string (using the same pattern):
```{code-block} python
s = 'Ripe bananas are yellow. Bananas are green when unripe'
```
```{code-block} python
p = r'Bananas'
```
Search for a match only at the beginning of the string:
```{code-block} python
m = re.match(p, s)
```
```{code-block} python
print(m)
```
Will give the output:
```{code-block} python
:class: no-copybutton
None
```
::::

#### `.start()`, `.end()`, and `.span()`
We can check the **start**, **end**, or **span** of a match using the `re.Match` object methods `.start()`, `.end()`, and `.span()` ([](#example_re_span)), respectively.

(example_re_span)=
::::{prf:example} Check the span of a match with `.span()` method
Given the match from [](#example_re_match):
```{code-block} python
m.group()
```
Will give the output:
```{code-block} python
:class: no-copybutton
'Bananas'
```
Obtain the span of the match:
```{code-block} python
m.span()
```
Will give the output:
```{code-block} python
:class: no-copybutton
(0, 7)
```
::::

#### `re.findall()`
We can **find all** matches in a string using `re.findall()`:
```{code-block} python
:class: no-copybutton
m = re.findall(pattern, string)
```
Returns a list of all the matches for which the `pattern` matches the `string` ([](#example_re_findall)).

(example_re_findall)=
::::{prf:example} Find all matches with `re.findall()`
Define a string:
```{code-block} python
s = 'Bananas are yellow when ripe. Bananas are green when unripe'
```
Define the pattern:
```{code-block} python
p = r'Bananas'
```
Search for a match only at the beginning of the string:
```{code-block} python
m = re.findall(p, s)
```
Print the matches in `m`:
```{code-block} python
print(m)
```
Will give the output:
```{code-block} python
:class: no-copybutton
['Bananas', 'Bananas']
```
::::

#### `re.finditer()`
To get more information on all matches we **find**, it is better to use `re.finditer()`:
```{code-block} python
:class: no-copybutton
m = re.finditer(pattern, string)
```
It returns an **iter**ator object containing each `re.Match` object of all matches. The information of the matches can then be retrieved via a `for` loop ([](#example_re_finditer)).

(example_re_finditer)=
::::{prf:example} Retrieve information of all matches with `re.finditer()`
Define a string:
```{code-block} python
s = 'Bananas are yellow when ripe. Bananas are green when unripe'
```
Define the pattern:
```{code-block} python
p = r'Bananas'
```
Search for all matches, obtaining all information:
```{code-block} python
m = re.finditer(p, s)
```
Print `m`:
```{code-block} python
print(m)
```
Will give the output:
```{code-block} python
:class: no-copybutton
<callable_iterator object at 0x76da1bf029e0>
```
Retrieve the matches in `m`:
```{code-block} python
for matches in m:
    matches.group()
```
Will give the output:
```{code-block} python
:class: no-copybutton
'Bananas'
'Bananas'
```
::::


#### `re.split()`
To **split** a string based on a character or pattern, we can use `re.split()`:
```{code-block} python
:class: no-copybutton
re.split(pattern, string)
```
Returns a list of the remaining characters ([](#example_re_split))

(example_re_split)=
::::{prf:example} Split a string on a character or pattern using `re.split()`
Define a string:
```{code-block} python
s = 'Bananas are yellow, oranges are orange'
```
Define the pattern:
```{code-block} python
p = r'\W+'
```
Split on the matches:
```{code-block} python
re.split(p, s)
```
Will give the output:
```{code-block} python
:class: no-copybutton
['Bananas', 'are', 'yellow', 'oranges', 'are', 'orange']
```
::::


#### `re.sub()`
To **sub**stitute all occurrences of a character or pattern with a replacement string, we can use `re.sub()`:
```{code-block} python
:class: no-copybutton
re.sub(pattern, replacement, string)
```
where `replacement` is the string to replace the matches with. It returns the processed string ([](#example_re_sub)).


(example_re_sub)=
::::{prf:example} Substitute a character or pattern using `re.sub()`
Define a string:
```{code-block} python
s = 'Bananas are yellow'
```
Define the pattern:
```{code-block} python
p = r'Bananas'
```
Define the replacement:
```{code-block} python
r = r'Lemons'
```
Substitute the matches:
```{code-block} python
re.sub(p, r, s)
```
Will give the output:
```{code-block} python
:class: no-copybutton
'Lemons are yellow'
```
::::


#### `re.compile()`
We can **compile** a {term}`regular expression` using `re.compile()`:
```{code-block} python
:class: no-copybutton
matcher = re.compile(pattern)
```
Then, the `pattern` is stored for repeated use into a pattern object. We can then use the `re` functions as methods on the pattern object ([](#example_re_compile)).

(example_re_compile)=
::::{prf:example} Compile a pattern in to a pattern object with `re.compile()`
Compile the pattern:
```{code-block} python
matcher = re.compile(r'Bananas')
```
Search for a match:
```{code-block} python
m = matcher.search('Bananas are yellow when ripe. Bananas are green when unripe')
```
```{code-block} python
print(m)
```
Will give the output:
```{code-block} python
:class: no-copybutton
<re.Match object; span=(0, 7), match='Bananas'>
```
::::


```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 5.3 Regular Expressions in Python
- Chapter 5.5 Functions of the `re` Module
```

### Groups
As explained [before](#section_re_capturing_and_replacing), {term}`groups <group (regex)>` can help structure the {term}`regular expression` or return part of the matched string ([](#example_re_groups)).


(example_re_groups)=
::::{prf:example} Group a part of the match to retrieve
Define a string:
```{code-block} python
s = 'Bananas are yellow, oranges are orange'
```
Define the pattern:
```{code-block} python
p = r'(\w+)\s\w+\syellow.+'
```
Search for the match:
```{code-block} python
m = re.search(p, s)
```
Print the whole match:
```{code-block} python
m.group(0)
```
Will give the output:
```{code-block} python
:class: no-copybutton
'Bananas are yellow, oranges are orange'
```
Print the group:
```{code-block} python
m.group(1)
```
Will give the output:
```{code-block} python
:class: no-copybutton
'Bananas'
```
::::


```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 5.6 Groups in Regular Expressions
``` 

## Exercises
``````{exercise} Start the W3D2 Jupyter Notebook
Download the W3D2 Jupyter Notebook from Brightspace.

Just like previous days, run the notebook with `jupyter notebook` in the terminal.
``````

Here, we define the assignments. The Jupyter notebook contains additional steps and hints.


### Introduction to Module `re`
``````{exercise} Cutting sites of the enzyme *Ava*II
Experiment with the `re` module by searching for the cutting sites of a specific enzyme: *Ava*II. 

Import module `re`.

Define the regular expression for the cutting site; include the representation of W in parentheses (a group); for a technicality, also define the whole regular expression as a group (so start with `(` and end with `)`).

Define some example DNA to cut.

We will look at a number of functions of module `re`: `findall`, `split`, `sub`, `search`, `finditer`, and `match`.
``````



### Pattern Matching
In the [previous ORF exercise](#exc_wd_orf), we had to find start codons and stop codons (or stop signs in the translation). This is typically a task that we can do with `regular expressions <regular expression>`.

``````{exercise} Refining ORF
First define a regular expression that matches an open reading frame, i.e it starts with a start codon (AUG) and ends at the first following stop codon (UAA, UAG, or UGA). 

The length of the result should be a multiple of 3.

Then use Python's module `re` for finding all open reading frames in a strand of RNA. Incorporate this into your ORF program.
``````

### Reading FASTA files - Revisited
In the [previous exercise on FASTA files](#exc_wwf_reading_fasta), we processed data immediately after reading it from file. For large files, this is often really necessary, because otherwise the data would not fit in memory.

The drawback of processing data immediately is that we often have to duplicate code or make complex control structures for processing data. Therefore, we look at an alternative now.


``````{exercise}  Reading FASTA files - Revisited
While reading the file, the program should create a dictionary with identifications as keys and sequences as associated values. So instead of printing or writing the counts immediately, the program stores the identification and sequence in a dictionary.

Then after reading the input file, and closing it, the program can process the data from the dictionary. Thus, reading and further processing become
independent parts of the program, making it easier to chance details of the processing part.

In particular, we postpone any writing to an output file until after the whole input file has been processed (and closed).

As an intermediate step in creating this program, after reading all indentifcations and sequences, you might print the identifications and sequences from the dictionary.

The process step for the previous version of this exercise consisted of computing nucleotide counts and writing these with the identification to an output file. For [Rosalind](https://rosalind.info/problems/locations/)'s problem GC, the program has to compute GC content for each sequence (and has keep track of the largest GC content as well, but we leave that out for now).

As an additional exercise in dictionaries, create a new dictionary with identifications as keys again and now GC content as associated values. This part
of the program should go after closing the input file.

Finish this program to produce an output file consisting of identifications and corresponding GC contents.
``````

### Combining FASTA and ORF
``````{exercise} ORF from a FASTA file
Doing the ORF exercise from FASTA files is now rather straightforward. 

We already have code for finding proteins from one DNA sequence (even in multiple variants). 

If we plug in that code – using functions – instead of computing GC content, we can leave the rest of the code as it is
``````


### Parsing Command Line Options and Arguments
As noted during one of the lectures, many programmers use their own conventions for command line arguments and especially command line options.
There is a standard for the format of command line options. However, it is hard to keep to that a standard like that, if you have to write new code for parsing options in every new program. (Remember that parsing is the process of recognizing structure and extracting meaningful elements from textual data.)

Fortunately, many programming languages and programming environments come with tools that can be reused for defining and parsing command line
options and command line arguments.

Python has a standard module `argparse` for defining which options and arguments a program accepts. That module then also takes care of parsing of
options and arguments, and even creates appropriate error messages when things go wrong.

The documentation of many modules is quite technical and hard to understand until you know how to use the module. Often, you have to see examples and
explanations before you can really start. Module `argparse` is no exception. 

::::{exercise} Walk through the `argparse` tutorial
Walk through a part of the [`argparse` tutorial](https://docs.python.org/3/howto/argparse.html) and try the examples!
::::