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


(data_types_section)=
## Data Types
Python contains different data types to store values: {term}`integers <integer>`, {term}`floats<float>` (real numbers), {term}`Booleans <Boolean data type>` (True, False), and {term}`strings<string>`. These data types are automatically detected by the Python interpreter [@w3schools_pythonnumbers_nodate;@w3schools_pythonbooleans_nodate;@w3schools_pythonstrings_nodate;@pythonsoftwarefoundation_built-types_2026]. To find out the data type of a value, you can use function `type()` ([](#example_type_function)).

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

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 3.3.3 Simple Calculations with Basic Data Types
```

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
A {term}`Boolean <Boolean data type>`, or bool, represents truth values and can be one of two values: `True` or `False` ([](#example_bool_truth_values)). They are often the result for when evalutating an expression ([](#boolean_operators_section)). 

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
Operators can be used to perform operations on values (and [variables](#variables_section)) [@w3schools_pythonoperators_nodate]. *Each [data type](#data_types_section) has their own respective operators. #!edit*

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 3.3.3 Simple Calculations with Basic Data Types
```

### Numerical Operators
Numerical operators are used with numeric values to perform common mathematical operations. In this way, Python can be used as a calculator. The various numerical operators are presented in [](#numerical_operators_table). 

:::{table} Numerical operators
:label: numerical_operators_table

| Numerical operator | Operation | Note |
| :---: | :--- | :--- |
| `+` | Addition | Also used as prefix operator (unary operator) representing a positive number |
| `-` | Subtraction | Also used as prefix operator (unary operator) representing a negative number |
| `*` | Multiplication | So no '`X`' or other similar symbol |
| `/` | Division | Always gives float result |
| `//` | Floor division | Always gives int result, rounds the number down |
| `%` | Modulo | Remainder of integer division |
| `**` | Exponentiation | Can't write superscripts in code |
:::


*#! if time left: add examples, esp. modulo example*

(string_operators_example)=
### String Operators
String operators work on, you guessed it, {term}`strings <string>`. They are listed in [](#string_operators_table)

:::{table} String operators
:label: string_operators_table

| String operator | Operation | Note |
| :---: | :--- | :--- |
| `+` | Concatenation | To combine strings, either side of the operator must be a string |
| `*` | Multiplication | Repetition, one side of the operator must be int the other must be str|
| `%` | Formatting | Format a string according to `format % values` |
:::

*#! add example*

Other data types can only be combined with {term}`strings <string>` if we use string formatting. An older style of string formatting uses the `%` symbol. The left hand must be a {term}`string` containing the `%` placeholder(s) for other data types. The right hand must contain as many values as placeholders ([](#example_string_formatting_old)).

(example_string_formatting_old)=
``````{prf:example} Old-style string formatting
Let's format a {term}`string` using an int `4`, a {term}`string` `"abc"`, and a {term}`float` `1.234` all separated by an `@`:
```{code-block} python
"%d@%s@%.2f" % (4, "abc", 1.234)
```
Will give the output:
```{code-block} python
:class: no-copybutton
'4@abc@1.23'
```
Formatting explained:
- the {term}`integer` is formatted with the placeholder `%d`
- the {term}`string` is formatted with the placeholder `%s`
- the {term}`float` is formatted with the placeholder `%.2f`, the `.2` means rounding to two decimal points
``````

### Comparison Operators
Comparison operators are used to compare two values. There are presented in [](#comparison_operators_table)

:::{table} Comparison operators
:label: comparison_operators_table

| Comparison operator | Operation | Data types |
| :---: | :--- | :--- |
| `==` | Equal to | Any data type, test for equality |
| `!=` | Differs from | Any data type, test for inequality |
| `>` | Greather than | At least for numeric and string types |
| `<` | Less than | At least for numeric and string types |
| `>=` | Greather than or equal to | At least for numeric and string types |
| `<=` | Less than or equal to | At least for numeric and string types |
:::

*#! add example*

(boolean_operators_section)=
### Boolean Operators
Boolean or logical operators are used to combine multiple Boolean expressions or objects. They are listed in [](#boolean_operators_table). Boolean operators are lazy (also called they short-circuit), meaning that they stop evaluating the expressions if a decision is met. For example, if we have two conditions and they both need to be true (`and`), the interpreter will not assess the second condition if the first one is `False`. Additionally, when either side is not a Bool, the meaning of the operation may not be intuitive. 

:::{table} Boolean operators
:label: boolean_operators_table

| Boolean operator | Operation | Data types |
| :---: | :--- | :--- |
| `and` | Conjunction | If both conditions are True, the expression returns True |
| `or` | Disjunction | If one of the conditions is True, the expression returns True  |
| `not` | Negation | If both conditions are False, the expression returns True |
:::


```{caution} Logical operators vs bit-wise operators
The book also mentions that you can use the `&`, `|`, and `!` bit-wise operators instead of the `and`, `or`, and `not` logical operators, respectively, but we advise against that because they have different meaning in standard Python.
```

```{margin}
Here are the reasons (you don't need to remember these):
- In Python, `!` is not an operator.
- The `&` and `|` operators are bit-wise operators, meaning they compare at the binary representation of integers and perform math at the bit-level, whereas `and` and `or` are logical operators, meaning they assess the truthiness of the entire Boolean expression.
- Logical operators are lazy (they short-circuit), whereas bit-wise operators do not.
- Logical operators have very low priority in Python's order of operation, whereas bit-wise operators have very high priority, meaning your logic can break if you do not account for this.

```

(variables_section)=
## Variables and Variable Assignment

## Built-in Functions

### pow() ???

### `len()`

### `help()`

### `print()`

### `input()`

## Comments in Code

## Exercises
