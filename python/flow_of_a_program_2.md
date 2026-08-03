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

(section_looping_over_a_list)=
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
There are several ways to loop over a dictionary. We can loop over the complete data structure ([](#example_loop_dict_complete)), or the keys ([](#example_loop_dict_keys)), the values ([](#example_loop_dict_values)), or the items ([](#example_loop_dict_items)) of a dictionary.

(example_loop_dict_complete)=
``````{prf:example} Looping over a dictionary object
Given the following dictionary:
```{code-block} python
transcription_dict = {'A' : 'U', 
                      'C' : 'G', 
                      'G' : 'C', 
                      'T' : 'A'}
```
```{code-block} python
for key in transcription_dict:
    print(key, ':', transcription_dict[key])
```
Will give the output:
```{code-block} python
:class: no-copybutton
A : U
C : G
G : C
T : A
```
``````

(example_loop_dict_keys)=
``````{prf:example} Looping over the keys of a dictionary
Given the following dictionary:
```{code-block} python
transcription_dict = {'A' : 'U', 
                      'C' : 'G', 
                      'G' : 'C', 
                      'T' : 'A'}
```
```{code-block} python
for key in transcription_dict.keys():
    print(key, ':', transcription_dict[key])
```
Will give the output:
```{code-block} python
:class: no-copybutton
A : U
C : G
G : C
T : A
```
``````

(example_loop_dict_values)=
``````{prf:example} Looping over the values of a dictionary
Given the following dictionary:
```{code-block} python
transcription_dict = {'A' : 'U', 
                      'C' : 'G', 
                      'G' : 'C', 
                      'T' : 'A'}
```
```{code-block} python
for value in transcription_dict.values():
    print(value)
```
Will give the output:
```{code-block} python
:class: no-copybutton
U
G
C
A
```
By looping over the values, we cannot access the keys.
``````

(example_loop_dict_items)=
``````{prf:example} Looping over the items of a dictionary
Given the following dictionary:
```{code-block} python
transcription_dict = {'A' : 'U', 
                      'C' : 'G', 
                      'G' : 'C', 
                      'T' : 'A'}
```
```{code-block} python
for key, value in transcription_dict.items():
    print(key, ':', value)
```
Will give the output:
```{code-block} python
:class: no-copybutton
A : U
C : G
G : C
T : A
```
The `.items()` method creates an iterable with tuples of `(key, value)` pairs.
``````


### Looping over a Tuple or Set
Looping over a tuple is similar to [looping over a list](#section_looping_over_a_list): we can retrieve both the content ([](#example_looping_tuple_content)) and the indexes ([](#example_looping_tuple_index)). For sets, however, we can only retrieve the content ([](#example_looping_set)). Since sets are unordered, their elements do not have an index.

(example_looping_tuple_content)=
``````{prf:example} Looping over the content of a tuple
Create a tuple from a string:
```{code-block} python
amino_acids = tuple('ACDEFGHIKLMNPQRSTVWY')
```
```{code-block} python
amino_acids
```
Will give the output:
```{code-block} python
:class: no-copybutton
('A', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'K', 'L', 'M', 'N', 'P', 'Q', 'R', 'S', 'T', 'V', 'W', 'Y')
```
Looping over the content:
```{code-block} python
for aa in amino_acids: 
    print(aa)
```
Will give the output:
```{code-block} python
:class: no-copybutton
A
C
D
E
F
G
H
I
K
L
M
N
P
Q
R
S
T
V
W
Y
```
``````

(example_looping_tuple_index)=
``````{prf:example} Looping over the index of a tuple
Create a tuple from a string:
```{code-block} python
amino_acids = tuple('ACDEFGHIKLMNPQRSTVWY')
```
```{code-block} python
amino_acids
```
Will give the output:
```{code-block} python
:class: no-copybutton
('A', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'K', 'L', 'M', 'N', 'P', 'Q', 'R', 'S', 'T', 'V', 'W', 'Y')
```
Looping over the index:
```{code-block} python
for i in range(len(amino_acids)): 
    print(i, amino_acids[i])
```
Will give the output:
```{code-block} python
:class: no-copybutton
0 A
1 C
2 D
3 E
4 F
5 G
6 H
7 I
8 K
9 L
10 M
11 N
12 P
13 Q
14 R
15 S
16 T
17 V
18 W
19 Y
```
``````


(example_looping_set)=
``````{prf:example} 
Create a set from a string:
```{code-block} python
unique_chars = set("While and for are different looping structures to alter the flow of a program")
```
```{code-block} python
unique_chars 
```
Will give the output:
```{code-block} python
:class: no-copybutton
{'c', 'i', 'p', ' ', 'r', 'u', 'a', 'd', 's', 'w', 'l', 'g', 't', 'm', 'e', 'W', 'n', 'o', 'f', 'h'}
```
Looping over the content:
```{code-block} python
for c in unique_chars:
    print(c)
```
Will give the output:
```{code-block} python
:class: no-copybutton
c
i
p

r
u
a
d
s
w
l
g
t
m
e
W
n
o
f
h
```
``````


## Data Representations
There are many ways to represent data in (a combination of) data structures. Here, we will show ways to store information about some of the moons of Jupiter in parallel lists ([](#example_data_representations_parallel_lists)), a list of tuples ([](#example_data_representations_list_of_tuples)), a dictionary ([](#example_data_representations_dict)), a dictionary of dictionaries ([](#example_data_representations_dict_of_dicts)), and a list of dictionaries ([](#example_data_representations_dict_of_lists)).

(example_data_representations_parallel_lists)=
``````{prf:example} Store data in parallel lists
```{code-block} python
names = ['Io', 'Europa', 'Ganymede', ]
masses = [8.9319e+22, 4.8000e+22, 1.4819e+23, ]
distances = [0.421700, 0.671034, 1.070412, ]
```
``````

(example_data_representations_list_of_tuples)=
``````{prf:example} Store data in a list of tuples
```{code-block} python
moons = [
    ('Io', 8.9319e+22, 0.421700),
    ('Europa', 4.8000e+22, 0.671034),
    ('Ganymede', 1.4819e+23, 1.070412),
]
```
``````

(example_data_representations_dict)=
``````{prf:example} Store data in a dictionary
```{code-block} python
moons = {
    'Io', : (8.9319e+22, 0.421700),
    'Europa', : (4.8000e+22, 0.671034),
    'Ganymede', : (1.4819e+23, 1.070412),
}
```
``````

(example_data_representations_dict_of_dicts)=
``````{prf:example} Store data in a dictionary of dictionaries
```{code-block} python
moons = {
    'Io', : {'mass' : 8.9319e+22, 'weight' : 0.421700},
    'Europa', : {'mass' : 4.8000e+22, 'weight' : 0.671034},
    'Ganymede', : {'mass' : 1.4819e+23, 'weight' : 1.070412},
}
```
``````

(example_data_representations_dict_of_lists)=
``````{prf:example} Store data in a list of dictionaries
```{code-block} python
moons = [
    {'name' : 'Io', 'mass' : 8.9319e+22, 'weight' : 0.421700},
    {'name' : 'Europa', 'mass' : 4.8000e+22, 'weight' : 0.671034},
    {'name' : 'Ganymede', 'mass' : 1.4819e+23, 'weight' : 1.070412},
]
```
``````


## Data Structure Conversions
Using loops, we can also convert one data structure to another. We can convert the parallel lists in [](#example_data_representations_parallel_lists) to a list of tuples in [](#example_data_representations_list_of_tuples) ([](#example_convert_parallel_lists_2_list_of_tuples)). Additionally, we can convert the list of tuples in [](#example_data_representations_list_of_tuples) to a dictionary of dictionaries in [](#example_data_representations_dict_of_dicts) ([](#example_convert_list_of_tuples_2_dict_of_dicts)).


(example_convert_parallel_lists_2_list_of_tuples)=
``````{prf:example} Convert parallel lists to a list of tuples
Given:
```{code-block} python
names = ['Io', 'Europa', 'Ganymede', ]
masses = [8.9319e+22, 4.8000e+22, 1.4819e+23, ]
distances = [0.421700, 0.671034, 1.070412, ]
```
Convert to a list of tuples:
```{code-block} python
moons = []
for i in range(len(names)):
    d = (
        names[i],
        masses[i],
        distances[i]
    )
    moons += [d] # or: result.append(d)
```
```{code-block} python
moons
```
Will give the output:
```{code-block} python
:class: no-copybutton
[('Io', 8.9319e+22, 0.4217), ('Europa', 4.8e+22, 0.671034), ('Ganymede', 1.4819e+23, 1.070412)]
```
``````

(example_convert_list_of_tuples_2_dict_of_dicts)=
``````{prf:example} Convert a list of tuples to a dictionary of dictionaries
Given:
```{code-block} python
moons = [
    ('Io', 8.9319e+22, 0.421700),
    ('Europa', 4.8000e+22, 0.671034),
    ('Ganymede', 1.4819e+23, 1.070412),
]
```
Convert to a dictionary of dictionaries:
```{code-block} python
dict_of_dicts = {}
for d in moons:
    name, mass, distance = d
    tmp = {} # or {'name' : name}
    tmp['mass'] = mass
    tmp['distance'] = distance
    dict_of_dicts[name] = tmp
```
```{code-block} python
dict_of_dicts
```
Will give the output:
```{code-block} python
:class: no-copybutton
{'Io': {'mass': 8.9319e+22, 'distance': 0.4217}, 'Europa': {'mass': 4.8e+22, 'distance': 0.671034}, 'Ganymede': {'mass': 1.4819e+23, 'distance': 1.070412}}
```
``````


## Exercises
Today, we will do some more [Rosalind](https://rosalind.info/problems/locations/) exercises: PROT and SUBS. 

``````{exercise} Start the W2D4 Jupyter Notebook
Download the W2D4 Jupyter Notebook from Brightspace.

Just like previous days, run the notebook with `jupyter notebook` in the terminal.

The Jupyter Notebook contains all the instructions.
``````


### (PROT) Translating RNA to Protein
``````{exercise} (PROT) Translating RNA to Protein
Given an RNA string (corresponding to a strand of mRNA), write the protein string encoded by the RNA string. 

A codon table dictates the details regarding the encoding of specific codons into amino acids. Amino acids are represented by 20 different letters (all letters except B, J, O, U, X, and Z).

Sample input:
```{code-block} bash
:class: no-copybutton
AUGGCCAUGGCGCCCAGAACUGAGAUCAAUAGUACCCGUAUUAACGGGUGA
```
Sample output:
```{code-block} bash
:class: no-copybutton
MAMAPRTEINSTRING
```
``````

### (SUBS) Finding a Motif in DNA - using Lists
``````{exercise} (SUBS) Finding a Motif in DNA - using Lists
The assignment is to change the code for "(SUBS) Finding a Motif in DNA" ([](#exc_foap1_subs)) to work with lists instead of strings.

The (two) inputs of the program are still strings, but now we convert them to lists immediately. 

Interestingly, we do not have to change any other code for finding the positions of substrings – sublists now.

As an additional exercise in working with lists, we do not print positions when we find them, but gather all found positions in a list. Only after we have found all positions, we will print the result.
``````


### Binomial Distribution
In a number of biological processes (e.g. male/female offspring, polygenic inheritance) probabilities are distributed according to the so-called binomial distribution. The binomial distribution defines chances for a series of discrete values, usually represented as whole numbers 0 to n (inclusive).

For example, if a couple gets three children and chances for a boy or girl are equal, the chances for three girls or three boys are $1/8$ each, and the chances for two boys and one girl or two girls and one boy are $3/8$ each. We can list this result (for $n=3$) as the chances for k girls with k=0,1,2,3.

This will be 0: 1/8; 1: 3/8; 2: 3/8; 3: 1/8, or in Python `[0.125, 0.375, 0.375, 0.125]` (index values are implicit).

There is an exact formula for a binomial distribution. However, in this exercise, we will make a table for a given $n$ by drawing random numbers repeatedly and keeping tallies.

The assignment is to write a script that asks the user for a number $n$ and then prints an approximate table of the binomial distribution for that $n$. The number of times to draw random numbers can be a fixed number in your program, or the program can ask it from the user as well.

The output for $n=3$ (as above) could look like this:
```{code-block} bash
:class: no-copybutton
number chance
0 0.125019
1 0.375334
2 0.374542
3 0.125105
```

``````{exercise} Generalized Bionomial Distribution
The generalized binomial distribution makes $n$ yes/no choices (or girl/boy, etc.) where each choice has a probability $p$ for answer yes (or girl in the example above). The probability for outcome $k$ ($k=0..n$) is the probability that exactly $k$ of
those $n$ choices give answer yes.

Again, there is an exact formula for a binomial distribution for any $p$ and $n$. But, again, we will make an approximation by repeatedly drawing numbers.

Copy your previous script and extend it to asks the user for a probablity $p$ as well as a number $n$, and then prints an approximate table of the generalized binomial distribution for that $p$ and $n$.
``````

``````{exercise} [optional] Generalized Bionomial Distribution using Dictionary 
For values of $p$ near to $1$ and relatively large $n$, the list of tallies will start with many zeros.

In a list, we cannot get rid of those zeros, because index values are absolute. We could do some bookkeeping to offset all index values. However, that would be very tricky. Instead, we can use a dictionary with the 'index' as key. Then we only have to fill cells for non-zero tallies.

The assignment is to replace the list of tallies by a corresponding dictionary. 
``````
