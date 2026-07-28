---
title: Getting Started with Python
label: getting_started_with_python
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

## Why Python?

## Writing and Running Python

### Interactive Python Shell

### Text Editor for Creating a Program

### Using an IDE

### Jupyter Notebook

## Data Types
Python contains different data types to store values: {term}`integers <integer>`, {term}`floats<float>` (real numbers), {term}`Booleans <Boolean data type>` (True, False), and strings. These data types are automatically detected by the Python interpreter [@noauthor_python_nodate;@pythonsoftwarefoundation_built-types_2026;w3schools_pythonbooleans_nodate]. To find out the data type of a value, you can use function `type()` ([](#example_type_function)).

(example_type_function)=
``````{prf:example} Find out the data type of value 1.5
```{code-block} python
type(1.5)
```
```{code-block} python
:class: no-copybutton
<class 'float'>
```
``````


### Integers
An {term}`integer`, abbreviated as int, is a whole number ([](#example_int_whole_number)). An {term}`integer` can be positive or negative ([](#example_int_negative)), and can be of unlimited length. 

(example_int_whole_number)=
``````{prf:example} Integers are whole numbers
```{code-block} python
type(12345)
```
Will give the output:
```{code-block} python
:class: no-copybutton
<class 'int'>
```
``````

(example_int_negative)=
``````{prf:example} Integers can be positive or negative
```{code-block} python
type(-1)
```
Will give the output:
```{code-block} python
:class: no-copybutton
<class 'int'>
```
``````

### Floats
A {term}`float`, or floating point number, is a positive or negative number containing one or more decimals ([](#example_float_decimal_number), [](#example_float_negative)). {term}`Floats<float>` can also be scientific numbers. Then they use the `e` to represent the power of 10 ([](#example_float_scientific)).

(example_float_decimal_number)=
``````{prf:example} Floats are numbers containing one or more decimals
```{code-block} python
type(1.2345)
```
Will give the output:
```{code-block} python
:class: no-copybutton
<class 'float'>
```
``````

(example_float_negative)=
``````{prf:example} Floats can be positive or negative
```{code-block} python
type(-1.2345)
```
Will give the output:
```{code-block} python
:class: no-copybutton
<class 'float'>
```
``````

(example_float_scientific)=
``````{prf:example} Floats can be scientific numbers
```{code-block} python
12E4
```
Will give the output:
```{code-block} python
:class: no-copybutton
120000.0
```
Let's check the type:
```{code-block} python
type(12E4)
```
Will give the output:
```{code-block} python
:class: no-copybutton
<class 'float'>
```
``````

### Booleans
A {term}`Boolean <Boolean data type>`, or bool, represents truth values and can be one of two values: `True` or `False` ([](#example_bool_truth_values)). They are often the result for when evalutating an expression ([](#boolean_operators)). 

(example_bool_truth_values)=
``````{prf:example} Booleans can be either True or False
```{code-block} python
type(True)
```

```{code-block} python
:class: no-copybutton
<class 'bool'>
```
```{code-block} python
type(False)
```
Will give the output:
```{code-block} python
:class: no-copybutton
<class 'bool'>
```
``````


### Strings
{term}`Strings <string>` are how Python handles textual data. A {term}`string`, or str, is a sequences of characters ([](#example_str_basic)). They are written by surrounding text by either single (`'`) or double (`"`) quotes, so that if you want to include on or the other in your {term}`string`, you can ([](#example_str_quotes)). {term}`Strings <string>` can contain any type of character (defined in for example [](wiki:ASCII) or [](wiki:UTF-8) by [](wiki:Unicode)), such as, but not limited to: letters, numbers, and punctuation characters ([](#example_str_complex)).

(example_str_basic)=
``````{prf:example} Strings are a sequence of text 
```{code-block} python
type("Hello World")
```
Will give the output:
```{code-block} python
:class: no-copybutton
<class 'str'>
```
``````

(example_str_quotes)=
``````{prf:example} Strings can be defined with either single or double quotes
```{code-block} python
type("this is a single quote ' within a double quoted string")
```
Will give the output:
```{code-block} python
:class: no-copybutton
<class 'str'>
```

```{code-block} python
type('this is a double quote " within a single quoted string')
```
Will give the output:
```{code-block} python
:class: no-copybutton
<class 'str'>
```
``````

(example_str_complex)=
``````{prf:example} Strings can contain different characters
```{code-block} python
type("H3ll0 W0rld!")
```
Will give the output:
```{code-block} python
:class: no-copybutton
<class 'str'>
```
``````


### Conversions
Some values of data types can be converted between each other. This is especially useful when handling user input data or files. *#!cross reference?* 

If values are {term}`integer`-like but are currently stored in a different data type, they can be converted to an {term}`integer` using built-in function `int()` ([](#example_int_convert_str)). 

(example_int_convert_str)=
``````{prf:example} Convert the string "1" to integer 1 
Let's check the type of `"1"`:
```{code-block} python
type("1")
```
Will give the output:
```{code-block} python
:class: no-copybutton
<class 'str'>
```

It is a {term}`string`, but it could also be seen as a whole number. Let's convert it to an {term}`integer`:
```{code-block} python
int("1")
```
Will give the output:
```{code-block} python
:class: no-copybutton
1
```

To be sure, let's check the type:
```{code-block} python
type(int("1"))
```
Will give the output:
```{code-block} python
:class: no-copybutton
<class 'int'>
```
``````

Similarly, you can convert an {term}`integer` or {term}`string` to a float using `float()` ([](#example_float_convert_integer) [](#example_float_convert_string)).

(example_float_convert_integer)=
``````{prf:example} Convert the integer 1 to float 1.0
Let's check the type of `1`:
```{code-block} python
type(1)
```
Will give the output:
```{code-block} python
:class: no-copybutton
<class 'int'>
```

It is a {term}`integer`, but it could also be seen as a floating point number. Let's convert it to a {term}`float`:
```{code-block} python
float(1)
```
Will give the output:
```{code-block} python
:class: no-copybutton
1.0
```

To be sure, let's check the type:
```{code-block} python
type(float(1))
```
Will give the output:
```{code-block} python
:class: no-copybutton
<class 'float'>
```
``````


(example_float_convert_string)=
``````{prf:example} Convert the string "1.0" to float 1.0
Let's check the type of `"1.0"`:
```{code-block} python
type("1.0")
```
Will give the output:
```{code-block} python
:class: no-copybutton
<class 'str'>
```

It is a {term}`string`, but it could also be seen as a floating point number. Let's convert it to a {term}`float`:
```{code-block} python
float("1.0")
```
Will give the output:
```{code-block} python
:class: no-copybutton
1.0
```

To be sure, let's check the type:
```{code-block} python
type(float("1.0"))
```
Will give the output:
```{code-block} python
:class: no-copybutton
<class 'float'>
```
``````

You can convert any data type to a {term}`string` using `str()` ([](#example_string_convert_float), [](#example_string_convert_int), [](#example_string_convert_bool)).

(example_string_convert_float)=
``````{prf:example} Convert the float 1.0  to string "1.0"
Let's check the type of `1.0`:
```{code-block} python
type(1.0)
```
Will give the output:
```{code-block} python
:class: no-copybutton
<class 'float'>
```

It is a {term}`float`, but let's convert it to a {term}`string`:
```{code-block} python
str(1.0)
```
Will give the output:
```{code-block} python
:class: no-copybutton
'1.0'
```

To be sure, let's check the type:
```{code-block} python
type(str(1.0))
```
Will give the output:
```{code-block} python
:class: no-copybutton
<class 'str'>
```
``````

(example_string_convert_int)=
``````{prf:example} Convert the integer 1  to string "1"
Let's check the type of `1`:
```{code-block} python
type(1)
```
Will give the output:
```{code-block} python
:class: no-copybutton
<class 'int'>
```

It is a {term}`integer`, but let's convert it to a {term}`string`:
```{code-block} python
str(1)
```
Will give the output:
```{code-block} python
:class: no-copybutton
'1'
```

To be sure, let's check the type:
```{code-block} python
type(str(1))
```
Will give the output:
```{code-block} python
:class: no-copybutton
<class 'str'>
```
``````

(example_string_convert_bool)=
``````{prf:example} Convert the Boolean True to string "True"
Let's check the type of `True`:
```{code-block} python
type(True)
```
Will give the output:
```{code-block} python
:class: no-copybutton
<class 'bool'>
```

It is a {term}`Boolean <Boolean data type>`, but let's convert it to a {term}`string`:
```{code-block} python
str(True)
```
Will give the output:
```{code-block} python
:class: no-copybutton
'True'
```

To be sure, let's check the type:
```{code-block} python
type(str(True))
```
Will give the output:
```{code-block} python
:class: no-copybutton
<class 'str'>
```
``````

## Operators

### Numeric operators

### String operators

(boolean_operators)=
### Boolean operators

## Variables and Variable Assignment

## Built-in Functions

### pow() ???

### `len()`

### `help()`

### `print()`

### `input()`

## Comments in Code

## Exercises
