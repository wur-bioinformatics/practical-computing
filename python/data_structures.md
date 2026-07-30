---
title: Data Structures
label: python_data_structures
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

(section_data_structures)=
## Data Structures
Apart from the simple data types discussed in [](#data_types_section), Python has built-in data structures to organize data. Here, we will discuss the main ones: lists, dictionaries, tuples, and sets. There are also more complex data structures within Python, but they are not necessary for the problems at hand.

### Lists
Lists are ordered collections of items. The items within a list can be of different data types ([](#example_list_different_data_types)), and the same value can occur multiple times ([](#example_list_same_values)). Each item in a list has an index, starting at `0`. The last item in the list has the index `-1`. In other programming languages, lists are often called "arrays". Though, Python lists are more flexible than standard arrays. Lists can grow and shrink: they are mutable. Most often, elements are added to the end of the list, but it also possible to add or remove internal elements. Additionally, we can concatenate lists (similar as for {term}`strings<string>` *#! or section ref?*).

(example_list_different_data_types)=
``````{prf:example} Items in lists can have different data types
```{code-block} python
a = ["ATG", 4, 1.5, True]
```
```{code-block} python
print(a)
```
Will give the output:
```{code-block} python
:class: no-copybutton
['ATG', 4, 1.5, True]
```
``````

(example_list_same_values)=
``````{prf:example} Items in lists can have the same value
```{code-block} python
b = ["ATG", "TATA", "ATG"]
```
```{code-block} python
print(b)
```
Will give the output:
```{code-block} python
:class: no-copybutton
["ATG", "TATA", "ATG"]
```
``````


#### Creating a List
There are several ways to create a list. First, a list can be created by so-called "list display". This means that you create the list as it would appear as it would be for example printed. We already used list-display in [](#example_list_different_data_types) and [](#example_list_same_values). We can also create a list of only one item ([](#example_list_one_item)), or an empty list ([](#example_list_empty)). Creating an empty list can be used before for example a loop in which the list will be filled with items.


(example_list_one_item)=
``````{prf:example} Create a one-item list using list display
```{code-block} python
c = [42]
```
```{code-block} python
print(c)
```
Will give the output:
```{code-block} python
:class: no-copybutton
[42]
```
``````

(example_list_empty)=
``````{prf:example} Create an empty list using list display
```{code-block} python
d = []
```
```{code-block} python
print(d)
```
Will give the output:
```{code-block} python
:class: no-copybutton
[]
```
``````

Second, we can create a list by repeating a single-element list ([](#), [](#)). This can be useful when you already know how long your final list will be, and you want to initialize it before altering the values of each item (with for example a loop). 

(example_list_intialise_repeating_zeros)=
``````{prf:example} Create a list of zeros by repeating a single-element list
```{code-block} python
e = [0] * 5
```
```{code-block} python
print(e)
```
Will give the output:
```{code-block} python
:class: no-copybutton
[0, 0, 0, 0, 0]
```
``````

(example_list_intialise_repeating_None)=
``````{prf:example} Create a list of None by repeating a single-element list
```{code-block} python
f = [None] * 5
```
```{code-block} python
print(f)
```
Will give the output:
```{code-block} python
:class: no-copybutton
[None, None, None, None, None]
```
`None` type can be used to create a list of "empty" cells.
``````

Last, a list can be created using the `list()` function ([](#)). The {term}`argument` supplied to `list()` should be an iterable.

(example_list_list_function)=
``````{prf:example} Create a list by using the list() function
```{code-block} python
g = list("12345")
```
```{code-block} python
print(g)
```
Will give the output:
```{code-block} python
:class: no-copybutton
['1', '2', '3', '4', '5']
```
``````


#### List Indexing and Slicing

#### List Versus String

### Dictionaries

#### Creating a Dictionary

#### Selecting from a Dictionary

### Tuples

#### Creating a Tuple

#### Tuple Indexing



### Sets
#### Creating a Set

#### Set operations


## Exercises
