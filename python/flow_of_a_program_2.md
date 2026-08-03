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
[Previously](#section_foap1_looping), we have seen that looping can be used to alter the flow of a program and that there are two flavors: the `for` loop and the `while` loop. We saw that the loops can be controlled by a specified number of iterations (`for` loop) or by a given condition (`while` loop). Instead of using a number determining the number of iterations, we can also use data structures, such as a list, string or more general: an iterable. 


### Looping over a List
When looping over a list using a `for` loop, we can either loop over the content ([](#example_for_loop_list_content)) or over the index ([](#example_for_loop_list_indexes)). When looping over the index, we can use both the value of the element in the list as the index ([](#example_for_loop_list_sub_indexes)). We can also add conditional branching to only print certain elements in a list ([](#example_for_loop_list_if)).

(example_for_loop_list_content)=
``````{prf:example} Loop over the content of a list with a for loop
Create a list:
```{code-block} python
codons = ['AUG', 'UUU', 'GCU', 'GUU', 'CCU']
```
Loop over the content:
```{code-block} python
for codon in codons:
    print(codon)
```
Will give the output:
```{code-block} python
:class: no-copybutton
AUG
UUU
GCU
GUU
CCU
```
``````

(example_for_loop_list_indexes)=
``````{prf:example} Loop over the indexes of a list with a for loop
Create a list:
```{code-block} python
codons = ['AUG', 'UUU', 'GCU', 'GUU', 'CCU']
```
Loop over the indexes:
```{code-block} python
for i in range(len(codons)):
    print(codons[i])
```
Will give the output:
```{code-block} python
:class: no-copybutton
AUG
UUU
GCU
GUU
CCU
```
``````

(example_for_loop_list_sub_indexes)=
``````{prf:example} Loop over part of the indexes of a list with a for loop
Create a list:
```{code-block} python
codons = ['AUG', 'UUU', 'GCU', 'GUU', 'CCU']
```
Loop over the indexes:
```{code-block} python
for i in range(len(codons)):
    print(i, codons[i])
```
Will give the output:
```{code-block} python
:class: no-copybutton
0 AUG
1 UUU
2 GCU
3 GUU
4 CCU
```
``````

(example_for_loop_list_if)=
``````{prf:example} Use conditional branching in a for loop, looping over a list
```{code-block} python
characters = list("While and for are different looping structures to alter the flow of a program")
```
```{code-block} python
for i in range(len(characters)-1):
    if characters[i] == characters[i+1]:
        print(i, characters[i])
```
Will give the output:
```{code-block} python
:class: no-copybutton
20 f
29 o
```
**Can you deduce what this program is doing?**
``````


Moreover, we can use a `while` loop to loop over a list. We can rewrite the [previous example](#example_for_loop_list_if) to use a `while` loop ([](#example_while_loop_list_if)). In a `while` loop, we can also add a Boolean to determine whether the condition is met ([](#example_while_loop_list_if_bool_1), [](#example_while_loop_list_if_bool_2)).

(example_while_loop_list_if)=
``````{prf:example} Use conditional branching in a while loop, looping over a list
```{code-block} python
characters = list("While and for are different looping structures to alter the flow of a program")
```
```{code-block} python
i = 0
while i < len(characters)-1:
    if characters[i] == characters[i+1]:
        print(i, characters[i])
    i += 1
```

Will give the output:
```{code-block} python
:class: no-copybutton
20 f
29 o
```
``````


(example_while_loop_list_if_bool_1)=
``````{prf:example} Add a Boolean value that turns True when the condition is met
```{code-block} python
characters = list("While and for are different looping structures to alter the flow of a program")
```
```{code-block} python
i = 0
found = False
while i < len(characters) - 1:
    if characters[i] == characters[i+1]:
        print(i, characters[i])
        found = True
    i += 1
print('found?', found)
```

Will give the output:
```{code-block} python
:class: no-copybutton
20 f
29 o
found? True
```
``````

(example_while_loop_list_if_bool_2)=
``````{prf:example} Use a Boolean value and a list to determine the condition of a while loop
```{code-block} python
characters = list("While and for are different looping structures to alter the flow of a program")
```
```{code-block} python
i = 0
found = False
while i < len(characters) - 1 and not found:
    if characters[i] == characters[i+1]:
        print(i, characters[i])
        found = True
    i += 1
print('found?', found)
```

Will give the output:
```{code-block} python
:class: no-copybutton
20 f
found? True
```
**What is different compared to the [previous example](#example_while_loop_list_if_bool_1)?**
``````


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