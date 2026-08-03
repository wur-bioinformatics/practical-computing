---
title: Getting Started with Python
label: getting_started_with_python
abbreviations:
    
bibliography:
    getting_started_with_python.bib
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
{term}`Strings <string>` are how Python handles textual data. A {term}`string`, or str, is a sequences of characters ([](#example_str_basic)). They are written by surrounding text by either single (`'`) or double (`"`) quotes, so that if you want to include on or the other in your {term}`string`, you can ([](#example_str_quotes)). {term}`Strings <string>` can contain any type of character (defined in for example [](wiki:ASCII) or [](wiki:UTF-8) by [](wiki:Unicode)), such as, but not limited to: letters, numbers, and punctuation characters ([](#example_str_complex)). {term}`Strings <string>` are immutable, meaning that they cannot be changed. You can assign a new value to a variable that holds a {term}`string`, but you cannot in-place alter the value of a {term}`string` variable (for example by changing a character to another character in a {term}`string`). 

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

(section_str_indexing_and_slicing)=
#### String Indexing and Slicing
Since {term}`strings<string>` are a sequence of characters, we can obtain individual characters by indexing:
```{code-block} python
:class: no-copybutton
my_string[index]
```
where `my_string` is a {term}`string` and `index` is the position in the {term}`string` we want to access ([](#example_str_indexing)).

(example_str_indexing)=
``````{prf:example} Obtain the third character of a string via indexing
Let's define a {term}`string` with a DNA sequence:
```{code-block} python
dna = "ATGTGACT"
```
Let's take the third character of `dna`:
```{code-block} python
dna[3]
```
Will give the output:
```{code-block} python
:class: no-copybutton
'T'
```
If you expected it to be `'G'`:

```{note} Python uses 0-based counting
Python starts counting from 0, so the first character has count `0`, the second `1`, the third `2`, etc.
```
``````

We can also access a substring of a {term}`string`, by so-called slicing:
```{code-block} python
:class: no-copybutton
my_string[start:end]
```
where `my_string` is a {term}`string`, `start` is the start index of the slice (inclusive), and `end` is the end index of the slice (exclusive) ([](#example_str_slicing)). 


(example_str_slicing)=
``````{prf:example} Slice the first three characters of a string
Let's define a {term}`string` with a DNA sequence:
```{code-block} python
dna = "ATGTGACT"
```
Let's slice out the first three characters of `dna`:
```{code-block} python
dna[0:3]
```
Will give the output:
```{code-block} python
:class: no-copybutton
'ATG'
```
``````

You can also use negative indexing in indexing and slicing. That way you can access elements from the end of the {term}`string`. The last characters has index `-1`, the second to last `-2` etc. ([](#example_str_negative_indexing)).


(example_str_negative_indexing)=
``````{prf:example} Use negative indexing to obtain the last character of a string
Let's define a {term}`string` with a DNA sequence:
```{code-block} python
dna = "ATGTGACT"
```
Let's slice out the last characters of `dna`:
```{code-block} python
dna[-1]
```
Will give the output:
```{code-block} python
:class: no-copybutton
'T'
```
``````


#### String Methods
Since Python is object-oriented, all variables are objects. Objects contain both the data (value(s)) and methods that can be used on the data. A method can be seen as a function specifically designed for that object. To see all methods associated with a Python variable or value you can use function `dir()`. 

Methods are called in the format:
```{code-block} python
:class: no-copybutton
object.method()
```
Where `object` can be a variable or value, and `method` is the relevant method for that object. 

There exist many useful string methods, we will discuss the following here: `.replace()` ([](#example_str_method_replace)), `.find()` ([](#example_str_method_find)), `.count()` ([](#example_str_method_count)), `.split()` ([](#example_str_method_split)), `.strip()` ([](#example_str_method_strip)), `.lower()` ([](#example_str_method_lower)), and `.upper()` ([](#example_str_method_upper)). 

(example_str_method_replace)=
``````{prf:example} Replace a character in a string with another character
Let's define a {term}`string` with a DNA sequence:
```{code-block} python
dna = "ATGTGACT"
```
Let's turn it into RNA by using the `.replace()` string method:
```{code-block} python
dna.replace("T", "U")
```
Will give the output:
```{code-block} python
:class: no-copybutton
'AUGUGACU'
```
``````

(example_str_method_find)=
``````{prf:example} Find the first occurence of a substring in a string
Let's define a {term}`string` with:
```{code-block} python
dna = "ATGTGACT"
```
Let's find the first occurence of `"C"` using the `.find()` string method:
```{code-block} python
dna.find("C")
```
Will give the output:
```{code-block} python
:class: no-copybutton
6
```

Let's find the first occurence of `"ATG"` using the `.find()` string method:
```{code-block} python
dna.find("ATG")
```
Will give the output:
```{code-block} python
:class: no-copybutton
0
```
```{note} Python uses 0-based counting
Python starts counting from 0, so the first character has count `0`, the second `1`, the third `2`, etc.
```
``````

(example_str_method_count)=
``````{prf:example} Count occurrence of a substring in a string
Let's define a {term}`string` with:
```{code-block} python
dna = "ATGTGACT"
```
Let's count the first occurences of `"G"` using the `.count()` string method:
```{code-block} python
dna.count("G")
```
Will give the output:
```{code-block} python
:class: no-copybutton
2
```
``````

(example_str_method_split)=
``````{prf:example} Split a string
Let's define a {term}`string` with:
```{code-block} python
plant = "Arabidopsis thaliana"
```
Let's split the {term}`string` using the `.split()` string method:
```{code-block} python
plant.split()
```
Will give the output:
```{code-block} python
:class: no-copybutton
['Arabidopsis', 'thaliana']
```
:::{note} `.split()` splits on whitespace by default
You can split on other characters (for example commas in a CSV file) by supplying the character you want to split on as argument.
:::
``````

(example_str_method_strip)=
``````{prf:example} Strip a string of a substring
Let's define a {term}`string` with leading and trailing whitespaces:
```{code-block} python
plant = " Arabidopsis thaliana "
```
Let's strip the {term}`string` of leading and trailing whitespaces using the `.strip()` string method:
```{code-block} python
plant.strip()
```
Will give the output:
```{code-block} python
:class: no-copybutton
'Arabidopsis thaliana'
```

:::{note} `.strip()` strips whitespace by default
You can strip other characters by supplying the character you want to strip as argument.
:::

``````

(example_str_method_lower)=
``````{prf:example} Make a string lower case
Let's make a {term}`string` lower case using the `.lower()` string method:
```{code-block} python
"ATGTGACT".lower()
```
Will give the output:
```{code-block} python
:class: no-copybutton
'atgtgact'
```
``````

(example_str_method_upper)=
``````{prf:example} Make a string upper case
Let's make a {term}`string` upper case using the `.upper()` string method:
```{code-block} python
'atgtgact'.upper()
```
Will give the output:
```{code-block} python
:class: no-copybutton
'ATGTGACT'
```
``````


```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 3.3.6 Strings
```


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

(comparison_operators_section)=
### Comparison Operators
Comparison operators are used to compare two values. There are presented in [](#comparison_operators_table).

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

*#! add example*

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
A variable is a named place to store a value. Often, we do not only use a value once. If we assign it to a variable, we can use it later on in our program and manipulate it. To create a variable, you simple assign it a value by using the `=` ([](#example_variable_assignment_simple)). On the left-hand of the `=` is the variable name, on the right-hand the value. 

(example_variable_assignment_simple)=
``````{prf:example} Assign a value to a variable
```{code-block} python
x_1 = 3
```
```{code-block} python
x_1
```
Will give the output:
```{code-block} python
:class: no-copybutton
3
```
``````

The following rules apply for naming a variable:
- The name has to start with a letter, then the remaining characters can be letters, digits, and underscores.
- Names are case-sensitive, so `x_1` and `X_1` are two different variables.
- Keywords (such as 'if', 'else', 'and', etc.) by itself cannot be used as variable names. 

Variables can be used instead of literals in formulas ([](#example_variable_assignment_formula)) and operations ([](#example_variable_assignment_operation)). Variables can be assigned new values, as many times as you want ([](#example_variable_assignment_new_value)).

(example_variable_assignment_formula)=
``````{prf:example} Variables can be used in formulas
```{code-block} python
y = x_1 * x_1 // 2
```
```{code-block} python
y
```
Will give the output:
```{code-block} python
:class: no-copybutton
4
```
``````

(example_variable_assignment_operation)=
``````{prf:example} Variables can be used in operations
```{code-block} python
x_1 > y
```
Will give the output:
```{code-block} python
:class: no-copybutton
False
```
``````


(example_variable_assignment_new_value)=
``````{prf:example} Variables can be assigned new values
```{code-block} python
x_1 = y + 1
```
```{code-block} python
x_1
```
Will give the output:
```{code-block} python
:class: no-copybutton
5
```
``````

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 3.3.4 Variable Assignment
```

## Built-in Functions
Python contains many useful functions that we can use to manipulate and query our variables. They are called as the function name, then the {term}`arguments<argument>` in parentheses separated by commas:
```{code-block} python
:class: no-copybutton
function_name(argument1, [argument2])
```
Functions often take at least one {term}`argument`.


```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 3.3.5 Built-In Functions
```

### Numerical Functions
There are many numerical functions available in Python. Some you can use straight away, such as: `pow(a,b)` for returning `a` to the power of `b` ([](#example_pow_function)), `abs(a)` for getting the absolute value of `a`, and `round(a, d)` for rounding `a` to `d` amount of decimal digits. For others you first need to import the `math` module by running: 
```{code-block} python
import math
```
Then, you can use for example `math.sin(a)` for returning the sine of `a`, and `math.floor(a)` to round `a` down to the nearest {term}`integer`.

(example_pow_function)=
``````{prf:example} Using pow(a,b) to return a to the power of b
```{code-block} python
pow(3,2)
```
Will give the output:
```{code-block} python
:class: no-copybutton
9
```
`pow(a,b)` is the same as `a**b`
``````

*#! add examples*

### `len()`
With function `len(a)` you can return the **len**gth of the variable `a`. For a {term}`string`, the length is the number of characters ([](#example_length_string)).

(example_length_string)=
``````{prf:example} Returning the length of a string
```{code-block} python
greeting = "Hello World"
```
```{code-block} python
len(greeting)
```
Will give the output:
```{code-block} python
:class: no-copybutton
11
```
``````


### `help()`
When using `help(a)` on the Python prompt, it will print information about argument `a`. The argument `a` can be a module ([](#example_help_module)), a function ([](#example_help_function)), a class, a variable or a value ([](#example_help_value)).

(example_help_module)=
``````{prf:example} Asking for help on a module
```{code-block} python
import math
```
```{code-block} python
help(math)
```
Will give the output (the first couple of lines):
```{code-block} python
:class: no-copybutton
Help on built-in module math:

NAME
    math

DESCRIPTION
    This module provides access to the mathematical functions
    defined by the C standard.

FUNCTIONS
    acos(x, /)
        Return the arc cosine (measured in radians) of x.

        The result is between 0 and pi.

    acosh(x, /)
        Return the inverse hyperbolic cosine of x.

    asin(x, /)
        Return the arc sine (measured in radians) of x.

        The result is between -pi/2 and pi/2.

    asinh(x, /)
        Return the inverse hyperbolic sine of x.
```
``````

(example_help_function)=
``````{prf:example} 
```{code-block} python
help(len)
```
Will give the output:
```{code-block} python
:class: no-copybutton
Help on built-in function len in module builtins:

len(obj, /)
    Return the number of items in a container.
```
```{note} Note how you ask for help on a function
When asking to print the documentation of a function using `help()`, you do not call the function (by using `len()`), you only name the function (by using `len`).
```
``````

(example_help_value)=
``````{prf:example} 
```{code-block} python
help(1)
```
Will give the output (the first couple of lines):
```{code-block} python
:class: no-copybutton
Help on int object:

class int(object)
 |  int([x]) -> integer
 |  int(x, base=10) -> integer
 |
 |  Convert a number or string to an integer, or return 0 if no arguments
 |  are given.  If x is a number, return x.__int__().  For floating-point
 |  numbers, this truncates towards zero.
 |
 |  If x is not a number or if base is given, then x must be a string,
 |  bytes, or bytearray instance representing an integer literal in the
 |  given base.  The literal can be preceded by '+' or '-' and be surrounded
 |  by whitespace.  The base defaults to 10.  Valid bases are 0 and 2-36.
 |  Base 0 means to interpret the base from the string as an integer literal.
 |  >>> int('0b100', base=0)
 |  4
```
``````


### `print()`
To print output to screen, we can use function `print()`. It can take multiple arguments, each separated by a comma and they can be of different data types ([](#example_print)).

(example_print)=
``````{prf:example} Print multiple values to screen
```{code-block} python
print(3, '*', 4, '=', 3*4)
```
Will give the output:
```{code-block} python
:class: no-copybutton
3 * 4 = 12
```
``````


### `input()`
To take input from the console, we can use the `input()` function ([](#example_input_string)). It converts what you type to a {term}`string`. If you want to store the input as a different data type, you need to convert it ([](#example_input_int)).


(example_input_string)=
``````{prf:example} Take a name as input from the console
```{code-block} python
name  = input('What is your name?')
```
In the console, it will state:
```{code-block} python
:class: no-copybutton
What is your name?
```
We can type directly after the question our name:
```{code-block} python
:class: no-copybutton
What is your name?User
```
Then if we print the variable `name`:
```{code-block} python
print(name)
```
It will give the output:
```{code-block} python
:class: no-copybutton
User
```
``````

(example_input_int)=
``````{prf:example} Take a number n as input from the console to print a string n amount of times
Take the input for `n` as:
```{code-block} bash
n = input('How many times?')
```
In the console, it will state:
```{code-block} python
:class: no-copybutton
How many times?
```
We can type directly after the question our number
```{code-block} python
:class: no-copybutton
How many times?4
```
Then if we print the variable `n`:
```{code-block} python
print(n)
```
It will give the output:
```{code-block} python
:class: no-copybutton
4
```

Print the string `'z'` `n` amount of times:
```{code-block} bash
print('z' * n)
```
Will give an error! 

We need to convert `n` to an {term}`integer`:
```{code-block} python
n = int(n)
```
If we try again:
```{code-block} bash
print('z' * n)
```
Will give the output:
```{code-block} bash
:class: no-copybutton
zzzz
```
``````


## Comments in Code
You can write comments in code by using the `#`. Anything after will be seen as a comment and not executed. Comments can be helpful to be more explicit in your code ([](#example_comment_explaining)), but don't overdo it ([](#example_comment_overdoing)).

(example_comment_explaining)=
``````{prf:example} Use comments to explain your code
```{code-block} python
# now x must be positive
```
``````

(example_comment_overdoing)=
``````{prf:example} Don't use comments to write what can easily be deduced from your code
```{code-block} python
x = 0 # initialize x to 0
```
``````

You can also use comments to temporarily switch off some code. Many editors have keybord short cuts for this.
```{tip}
In PyCharm to comment/uncomment a line or multiple lines of code use: \
{kbd}`Ctrl` + {kbd}`/` (Windows) or {kbd}`⌘Cmd` + {kbd}`/` (macOS) while standing with your cursor on the line or selecting the line(s) [@jetbrains_pycharmkeyboard_13072026].
```



## Exercises
### Installing Python and PyCharm
``````{exercise} Install Python (conda/anaconda) and PyCharm on your machine
Follow the guide on Brightspace "Installing Conda and Pycharm".
``````


### Experiment with Python
For these exercises we use a Jupyter notebook. First you need to obtain the notebook file from Brightspace; it is contained in the data ZIP-file (Week 2, Data).

(exc_start_w2d1_notebook)=
``````{exercise} Start W2D1 Jupyter Notebook
To start the notebook, first start a terminal by typing in your search bar "Anaconda Prompt" (Windows) or "terminal" (Mac/Linux). 

In the terminal, navigate to the directory where you saved the notebook.

```{tip}
Use [](#cd_section).

On Windows the directory path contains backward slashes (`\`) instead of forward slashes (`/`).
```

Start the notebook server by typing `jupyter notebook` at the command prompt. 

In the terminal, you will see some messages about starting the program. Then your browser will open and it shows a list of files at the current location. Jupyter Notebooks have file type `.ipynb` (probably there is just one notebook in the list right now). 

Double-click on the notebook that you have downloaded to open it.
``````

The W2D1 Jupyter Notebook contains all instructions for the exercises. They are repeated here for overview.

``````{exercise} Printing and asking input

- Write a Python command that prints your own name.
- Write a fragment of Python code that prints your own name 5 times below one another. Put each command on a line of its own.
- Write a fragment of Python code that assigns your first name to one variable, your second name to a second variable, and then concatenates them and stores the result in a third variable. Then print the third variable.
- Write Python code that prints your own name 100 times (tedious without loops?).
- Write Python code that asks the user’s name and prints it (once).
- Include a ‘prompt’ in the command that asks the name.
- Write Python code that asks the user’s name and prints it 100 times.
- Write Python code that asks the user’s name, then asks a number, and then prints the name that many times.
- Turn the last fragment of code into a Python script and run it outside this notebook.

``````

``````{exercise} Working with numbers
- Try to find out the following aspects of numbers in Python.
- Comments on “What is the largest int number in Python?”
- Find the largest float number in Python, up to a factor 2.
- Find a limit to the number of significant digits of a float number in Python.
- Find the smallest positive float number in Python, up to a factor 2.
``````

``````{exercise} Counting DNA nucleotides
- Find the appriopriate method for counting letters, and apply it for finding the counts for each of the nucleotides.
- Now write Python code that prints these counts together on one line, separated by spaces.
- Find out what type of value is contained in each of the variables introduced in this section.
``````

(exc_gswp_gc_content)=
``````{exercise} (GC) GC content - Computing the GC-content of a DNA sequence
- Determine the number of nucleotides in the given DNA sequence.
- Now compute and print the GC-content of the given DNA sequence.
- Write the answer as something like: `The GC-content is 23.456` (the exact number will differ)
- Finally, put the pieces of code together into a script. Then you can apply it to find the GC-content of the human IGF1 gene sequence.
``````

``````{exercise} Strings as objects
- Find a method in the DNA string that converts it from uppercase to lowercase letters.
- Check whether it really converted the variable to lowercase.
- Replace a variable by the same string in lowercase.
``````

``````{exercise} Other features of strings in Python
- Execute given lines of code for accessing individual characters in a string (indexing).
- Try some more values for the index.
- What happens if the index is negative?
- What happens if the index is too large?
- Execute given lines of code for obtaining a substring for a string (slicing).
- Do you see a pattern for the length of the slice?
- What is the meaning of the index value before the colon?
- What is the meaning of the index value after the colon?
- Try some more.
- Can we use negative index values?
- What happens if you leave out one or both ends?
- What happens if values are reversed?
- What happens if the ending index is too large?
- For the (lowercase) DNA string defined previously in the Jupyter notebook, we want to capture bases 8 (second c) through 16 (fourth c). Note that in DNA
sequences the convention is to count from 1, so the first base is called base 1
- Write Python code to capture bases 8 through 16 and assign the result to a variable.
- Now convert the selected substring to uppercase, and re-insert it into the DNA string, at its original position.
``````

