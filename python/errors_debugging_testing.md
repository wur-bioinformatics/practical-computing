---
title: Errors, Debugging, and Testing
label: errors_debugging_testing
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


### Preventing Errors

## Debugging

## Testing

## Efficiency

## Exercises
### Finding Known Errors (together)

### Finding Unknown Errors (together)

### Finding a Subtle Error in SUBS

### Finding Errors by Tracing Previous Versions
version management and checking differences