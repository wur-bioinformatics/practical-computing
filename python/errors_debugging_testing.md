---
title: Errors, Debugging, and Testing
label: errors_debugging_testing
abbreviations:
    IDE: Integrated Development Environment
bibliography:
    .bib
---

```{important} Learning outcomes
After completing this section you should be able to:
- learning_outcome1
- learning_outcome2
```

## Introduction

## Errors
Errors, or bugs, are mistakes made by the programmer that either result in an error being raised by the interpreter, or in wrong results. The former are in a way easier to solve, whereas the latter can propagate unknowningly.


### Types of Errors
Python distinguishes different types of errors and learning what they mean can give us clue on how we can fix our program. Errors can be divided into four categories: syntax errors, run-time errors, system-level errors, and logical errors. 

Syntax errors comprise of errors that occur due to invalid syntax, incorrect indentation or typos. These errors are raised before the code is actually executed by the interpreter parsing the code. 

Run-time errors are the errors that occur while the program is being executed. These are the errors that are raised for example by using incorrect names, when wrong parameters or data types are used, when an index is out of bounds, and when looking for a non-existing key value.

System-level errors are due to input/output issues, memory overflow or trouble with connecting to a network. 

Logical errors are when the program runs successfully, but the results are incorrect or unintended. This is usually due to incorrect functions, wrong dependencies, faulty calculations or inaccurate assumptions in the logic of your program. For example, when the unit of measurement is not what you expected (feet vs. meter). These errors are harder to uncover, because Python cannot raise an exception for them. 

Some common syntax and run-time errors are listed in [](#table_common_python_errors) and an exhaustive list of all errors can be found [here](https://realpython.com/ref/builtin-exceptions/). 

(table_common_python_errors)=
:::{list-table} Common Python Errors
* - Error type
  - Raised when
  - Usual culprit
* - `SyntaxError`
  - the syntax is incorrect
  - a missing colon after a conditional branch or loop, \
  missing quotes when defining a string, \
  using an assignment `=` instead of a `==` for comparison, \
  naming a variable a Python keyword (like raise, yield, etc.),\
  missing parentheses when using a function
* - `IndentationError`
  - there is an incorrect indentation
  - not the right amount of indentation when using conditional branching, loops or function definitions
* - `TypeError`
  - a function or operation is applied to an object of incorrect type
  - the variable type you used does not allow the operation you tried on it: check whether it is the correct type
* - `NameError`
  - a variable is not recognized in the local or global scope of your environment
  - a variable is not yet defined, \
  there is a typo in the variable name
* - `IndexError`
  - the index of a sequence is out of bounds
  - the item in the list you are trying to access does not exist
* - `KeyError`
  - a key is not found in a dictionary
  - the item in the dictionary you are trying to access does not exist
* - `AttributeError`
  - the attribute assignment fails
  - when trying to access an attribute or a method on an object that does not exist
:::

Other examples of code that will not necessarily raise an error, but are still wrong and can cause problems down the line:
- Writing a `return` statement before the last line of a function
- Not closing a file
- Off-by-one in indexing and slicing
- :::{code} python
  :class: no-copybutton
  if value in data_list == False: # or == True
  :::
  Should be:
  :::{code} python
  :class: no-copybutton
  if value not in data_list:
  :::


(section_edb_preventing_errors)=
### Preventing Errors
It is often better to prevent errors than needing to debug large amounts of code. Here, we will discuss some strategies that you can apply to prevent a part of the errors you will inevitably make. 

Before starting to code, write down what a piece of code is going to do, including assumptions. Even before starting writing a program you can make a [flow chart](#section_foap1_flow_charts) to help define the logic of your program. 

Use descriptive variable and function names. So not `variable1` and `variabe2`, but rather `dna_str` and `rna_str`.

Split your program up into parts. Use for each task a function and work on each function so it produces the desirable result of that task.

You can also let someone else read your code.

When there are certain problems you expect, you can use [`try`-`except`](https://docs.python.org/3/tutorial/errors.html#handling-exceptions) statements. However, it is less efficient than `if`-`else`. When possible, it is better to use `if`-`else`. Though, `try`-`except` can be useful for user input and file operations. When you use `try`-`except`, always use an exception type that is as specific as possible to your case. Do not use `except` without a type, because it may hide other problems. 

Before writing to files, it is better to first simulate the operation. For example by first only writing the filename to the console to ensure you are going to write to the correct file. 

While you are developing your program, run it on a copy of the data to ensure the original data remains uncompromised or on a smaller subset of the data if you are working with large data files. When you use a subset, make sure it is representative of the complete data set.

Test independent parts of your program separately to ensure the parts work as expected.

Keep previous versions of your program. Or better: use a version management system such as [Git](https://git-scm.com/). 

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 4.5 Errors and Exceptions
```

## Debugging
Debugging is the process of finding and removing the causes of your errors. It is best to isolate the problem by using small functions and testing them separately, then you can uncover which function is causing the problem. You can comment out code to see where your program still produces the expected result and where it goes wrong. Additionally, you can use `print()` statements to for example see what is stored in variables or whether your program actually enters conditional branches. However, this can be tricky if you are not explicit in what you are printing (printing `"here"` three times and only seeing it twice in the console does not hep you in finding out what goes wrong). You can also write to a log-file instead of printing. 

You can also debug using a debugger. A debugger is a tool that executes your program in an environment that allows for inspection and control. Debuggers are always part of IDEs. 

Main functionalities of debuggers are:
- Setting breakpoints: Pausing the program on a specific line
- Inspecting variables: Checking the content of variables in memory while the program runs
- Step-by-step execution: Run the code of the program line-by-line.
- Changing variables (not in all environments): Changing the content of variables in memory while the program runs

*#! command line debugger obsolete? add that or not?*

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 4.6 Debugging
```

## Testing
As mentioned [before](#section_edb_preventing_errors), one way to prevent errors is by performing tests. To do so, use small examples for which you can predict the output and the properties of the output (e.g. amount of lines) before running. Preferably, do this for each small part of your program, or function. Make sure to also include special cases, the so-called edge cases. These are cases that fall out of normal use, but can still happen, and should be accounted for. 

Too often, people say "Testing shows that the program works fine." But:

:::{blockquote}
Program testing can be used to show the presence of bugs, but never to show their absence!

-- Edsger Dijkstra, 1970
:::

There are also ways to automate tests. The simplest way is using `assert` statements in your Python code. Alternatively, `doctest` as described in the book, or use packages as `PyUnit` or `unittest` for more advanced unit testing. 


```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 4.7 Unit Testing
```

## Efficiency
Apart from writing correct code, it is also worth mentioning to write efficient code. To improve efficiency, we first need to ding out where time is spent by for examing using a profiler *#! explain what that is?*. 

Some general tips to improve efficiency:
- avoid re-opening files
- use dictionaries instead of lists (esp. Python)
- buy a faster computer (no joke)

However, never compromise correctness: a wrong answer fast is worse than the correct answer later. Additionally, be very very careful when condensing code, make sure it still operates as you want it to operate.

## Exercises
### Finding Known Errors (together)

### Finding Unknown Errors (together)

### Finding a Subtle Error in SUBS

### Finding Errors by Tracing Previous Versions
version management and checking differences