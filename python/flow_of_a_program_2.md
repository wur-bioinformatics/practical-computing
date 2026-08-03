---
title: Flow of a Program 2
label: flow_of_a_program_2
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

## Useful Functions for Looping
When looping over a data structure, the functions `len()` and `range()` are especially useful. 

### `len()`
The function `len()` gives the number of elements of a data type or structure, or the **len**gth. It is supported by most structured data types and iterables and commonly used on lists [](#example_len_list), strings ([](#example_len_str)), dictionaries ([](#example_len_dict)), and sets ([](#example_len_set)).

(example_len_list)=
``````{prf:example} Length of a list
Create a list:
```{code-block} python
codons = ['AUG', 'UUU', 'GCU', 'GUU', 'CCU']
```
The amount of elements in the list can be returned with `len()`:
```{code-block} python
len(codons)
```
Will give the output:
```{code-block} python
:class: no-copybutton
5
```
``````

(example_len_str)=
``````{prf:example} Length of a string
```{code-block} python
len('ATG')
```
Will give the output:
```{code-block} python
:class: no-copybutton
3
```
``````


(example_len_dict)=
``````{prf:example} Length of a dictionary
```{code-block} python
transcription_dict = {'A' : 'U', 
                      'C' : 'G', 
                      'G' : 'C', 
                      'T' : 'A'}
```
```{code-block} python
len(transcription_dict)
```

Will give the output:
```{code-block} python
:class: no-copybutton
4
```
``````

(example_len_set)=
``````{prf:example} Length of a set
```{code-block} python
polar_aa = {'Ser', 'Thr', 'Tyr', 'Asn', 'Gln'}
```
```{code-block} python
len(polar_aa)
```

Will give the output:
```{code-block} python
:class: no-copybutton
5
```
``````


### `range()`
The function `range()` allows us to iterate through a **range** of elements in a `for` loop. It creates an iterator object with a fixed memory footprint of type range. By turning the range into a list, we can see what is stored in the object ([](#example_range_inside)).


(example_range_inside)=
``````{prf:example} Turn a range object into a list
```{code-block} python
list(range(5))
```
Will give the output:
```{code-block} python
:class: no-copybutton
[0, 1, 2, 3, 4]
```
``````

It takes three arguments:
```{code-block} python
:class: no-copybutton
range(start, stop, step)
```
where `start` is the number from which the range starts (defaults to 0, included), `stop` is the number until the range ends (excluded), and `step` is the steps it takes to build the range: the increment when positive, and decrement when negative. Only `stop` is required.

`range()` can be combined with `len()` to create an iterable from a list ([](#example_range_from_list)). When providing the `start` and `stop` arguments, you can specify the exact range you want to build ([](#example_range_start_end)). The `step` argument can be useful when you want to skip certain elements in a list ([](#example_range_start_end_step)).


(example_range_from_list)=
``````{prf:example} Create a range from a list
Given the list:
```{code-block} python
x = [0.3, 0.7, 1.9, 3.5]
```
Get the indexes of `x`:
```{code-block} python
indexes = list(range(len(x)))
```
```{code-block} python
print(indexes)
```
Will give the output:
```{code-block} python
:class: no-copybutton
[0, 1, 2, 3]
```
``````


(example_range_start_end)=
``````{prf:example} Create a range from start until end (excluded)
Get a range of sub-indexes and turn it into a list to see what is inside:
```{code-block} python
sub_indexes = list(range(1, 3))
```
```{code-block} python
print(sub_indexes)
```

Will give the output:
```{code-block} python
:class: no-copybutton
[1, 2]
```
``````

(example_range_start_end_step)=
``````{prf:example} Create a range with step
Get a sub-range of even `indexes` ([](#example_range_from_list)) and turn it into a list to see what is inside:
```{code-block} python
list(range(0, len(x), 2))
```
Will give the output:
```{code-block} python
:class: no-copybutton
[0, 2]
```
``````


## Looping - Expanded

### `for` loop

### Looping over a List

### Looping over a Dictionary

### Looping over a Tuple or Set

## Data Representations

## Data Structure Conversions

## Exercises

### (PROT) Translating RNA to Protein

### Rosalind’s SUBS using Lists

### Binomial Distribution
– basis
– generalized
– on dictionaries