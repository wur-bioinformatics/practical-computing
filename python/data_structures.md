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


## Data Structures
Apart from the simple data types discussed in [](#data_types_section), Python has built-in data structures to organize data. Here, we will discuss the main ones: lists, dictionaries, tuples, and sets. There are also more complex data structures within Python, but they are not necessary for the problems at hand.

### Lists
Lists are ordered collections of items. The items within a list can be of different data types ([](#example_list_different_data_types)), and the same value can occur multiple times ([](#example_list_same_values)). Each item in the lists has an index, starting at `0`. The last item in the list has the index `-1`. In other programming languages, lists are often called "arrays". Though, Python lists are more flexible than standard arrays.

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
