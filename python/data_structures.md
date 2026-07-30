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

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 3.4.1 Lists
```

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
Similar to [](#section_str_indexing_and_slicing), we can also access elements in lists using indexing (example_list_indexing) and obtain a part of a list using slicing ([](#)). Again, negative indices mean counting from the end, with `[-1]` taking the last element. 

(example_list_indexing)=
``````{prf:example} Access an element in a list using indexing
Given list `b` created in [](#example_list_same_values), we can access the second element using:
```{code-block} python
b[1]
```
Will give the output:
```{code-block} python
:class: no-copybutton
'TATA'
```
The result of indexing is the value of the indexed item, with as data type the data type of the value.
``````

(example_list_slicing)=
``````{prf:example} Access part of a list using slicing
Given list `g` created in [](#example_list_list_function), we can access slice going from the second to the fourth element by:
```{code-block} python
g[1:4]
```
Will give the output:
```{code-block} python
:class: no-copybutton
['2', '3', '4']
```
The result of slicing is a copy of the elements in the list.
``````

Since lists are mutable, you can replace values of items using indexing for replacing a single item ([](#example_list_indexing_replacing_value)) and slicing for replacing multiple items ([](#example_list_slicing_replacing_values)). When replacing a slice, you must supply the replacement with an iterable. You can replace the slice with a smaller or larger sized iterable than the original slice, thereby adding or removing items. 

(example_list_indexing_replacing_value)=
``````{prf:example} Replace a value of an item in a list using indexing
Given list `g` created in [](#example_list_list_function), we can replace the first item in the list (with value `'1'`) by:
```{code-block} python
g[0] = '0'
```
```{code-block} python
g
```
Will give the output:
```{code-block} python
:class: no-copybutton
['0', '2', '3', '4', '5']
```
``````

(example_list_slicing_replacing_values)=
``````{prf:example} Replace values of items in a list using slicing
Given list `g` created in [](#example_list_list_function), we can replace the second and third item in the list by:
```{code-block} python
g[1:3] = [2,3]
```
```{code-block} python
g
```
Will give the output:
```{code-block} python
:class: no-copybutton
['1', 2, 3, '4', '5']
```
``````

```{note} Square brackets are used in list display and when indexing or slicing
When creating a list using list display, you use the square brackets (`[]`). 

When indexing or slicing from a list you also use square brackets (`[]`).
```

#### List Versus String
Both lists and {term}`strings<string>` support indexing and slicing. It is important to remember that {term}`strings<string>` are immutable while lists are mutable. Consequently, you cannot alter the elements and slices of a {term}`string`, but you can for a list. Since both are iterables they can be converted from and to another ([](#example_list_list_function),[](#example_string_convert_list),[](#example_string_join_list)).

(example_string_convert_list)=
``````{prf:example} Convert a string to a list and the list to a string
Convert a {term}`string` to a list using `list()`:
```{code-block} python
my_string = 'abcdefg'
```
```{code-block} python
my_list =  list(my_string)
```
```{code-block} python
my_list
```
Will give the output:
```{code-block} python
:class: no-copybutton
['a', 'b', 'c', 'd', 'e', 'f', 'g']
```
Convert a list to a {term}`string` using `str()`:
```{code-block} python
my_string_2 = str(mylist)
```
```{code-block} python
my_string_2
```

Will give the output:
```{code-block} python
:class: no-copybutton
"['a', 'b', 'c', 'd', 'e', 'f', 'g']"
```
``````

(example_string_join_list)=
``````{prf:example} Create a string by joining the elements of a list
With the string method `.join()` you can join elements of an iterable with the string the method is used on. 

When you want to concatenate the elements of a list together into a string, use an empty string: 
```{code-block} python
''.join(my_list)
```
Will give the output:
```{code-block} python
:class: no-copybutton
'abcdefg'
```

When you want to join the elements by anything else (like spaces), use that as the string:
```{code-block} python
' '.join(my_list)
```
Will give the output:
```{code-block} python
:class: no-copybutton
'a b c d e f g'
```
``````


### Dictionaries
A dictionary (in short, dict) is a mutable collection of data. They are also calles "lookup table" or "associative array". Entries in a dictionary are stored as a key-value pair. Each key in a dictionary is unique and immutable, it can be seen as the "index" of the entry. The value associated with a key is mutable and can be any data type (even a dictionary). 

You cannot slice into a dictionary or add entries via concatenation. 

The advantage of a dictionary is that it is very effient in lookup. Namely, lookup is almost independent of the number of entries in the dictionary, and checking if a key is present takses the same time as lookup. If the order of your entries does not really matter, and you want to quickly access entries, the dictionary is the way to go for storing your data. 


#### Creating a Dictionary
A dictionary can be created in two manners: by "dictionary display" ([](#example_dict_dictionary_display_multiple), [](#example_dict_dictionary_display_single)) or by using the `dict()` function ([](#example_dict_dict_function_multiple)). When using `dict()`, specify the key-value pairs with `key = value` as arguments, separated by a comma. The key should not be quoted if it's a string. 


(example_dict_dictionary_display_multiple)=
``````{prf:example} Create a dictionary with multiple entries using dictionary display
While creating a dictionary, you can put each key-value pair on a new line to make it clearer:
```{code-block} python
transcription_dict = {'A' : 'U', 
                      'C' : 'G', 
                      'G' : 'C', 
                      'T' : 'A'}
```
```{code-block} python
transcription_dict
```
Will give the output:
```{code-block} python
:class: no-copybutton
{'A': 'U', 'C': 'G', 'G': 'C', 'T': 'A'}
```
``````

(example_dict_dictionary_display_single)=
``````{prf:example} Create a dictionary with one entry using dictionary display
```{code-block} python
int2str_dict = {37 : '37'}
```
```{code-block} python
int2str_dict
```
Will give the output:
```{code-block} python
:class: no-copybutton
{37 : '37'}
```
``````

(example_dict_dict_function_multiple)=
``````{prf:example} Create a dictionary with multiple entries using dict()
When using `dict()`, specify the key-value pairs with `key = value` for the arguments, separated by a comma:
```{code-block} python
transcription_dict = dict(A = 'U', C = 'G', G = 'C', T = 'A')
```
```{code-block} python
transcription_dict
```
Will give the output:
```{code-block} python
:class: no-copybutton
{'A': 'U', 'C': 'G', 'G': 'C', 'T': 'A'}
```
``````

You can also create an empty dictionary using both methods ([](#example_dict_create_empty)). After you have initialized an empty dictionary, you can fill it with entries by adding key-value pairs one by one ([](#example_dict_fill_onebyone)). If you assign a value to an existing key, you will override the associated value. If you assign a new key, you add an entry into the dictionary.


(example_dict_create_empty)=
``````{prf:example} Create an empty dictionary
You can create an empty dictionary by using either dictionary display:
```{code-block} python
transcription_dict = {}
```
or by using `dict()`:
```{code-block} python
transcription_dict = dict()
```
```{code-block} python
transcription_dict
```
Will give the output for both cases as:
```{code-block} python
:class: no-copybutton
{}
```
``````

(example_dict_fill_onebyone)=
``````{prf:example} Fill an empty dictionary by adding key-value pairs one by one
Starting with an empty dictionary:
```{code-block} python
transcription_dict = {}
```
We can add entries as follows:
```{code-block} python
transcription_dict['A'] = 'U'
```
```{code-block} python
transcription_dict['C'] = 'G'
```
```{code-block} python
transcription_dict['G'] = 'C'
```
```{code-block} python
transcription_dict['T'] = 'A'
```
The dictionary is now filled:
```{code-block} python
transcription_dict
```

Will give the output:
```{code-block} python
:class: no-copybutton
{'A': 'U', 'C': 'G', 'G': 'C', 'T': 'A'}
```
``````

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 3.4.2 Dictionaries
```

#### Selecting from a Dictionary
Selecting from a dictionary is technically also called indexing. Here, we also use the square brackets (`[]`) ([](#example_dict_indexing)). If the key does not exist, you will get a `KeyError`.


(example_dict_indexing)= 
``````{prf:example} Get the associated value of a key in a dictionary using indexing
Given the dictionary: 
```{code-block} python
transcription_dict = {'A' : 'U', 
                      'C' : 'G', 
                      'G' : 'C', 
                      'T' : 'A'}
```
Get the associated value for the `'A'` key:
```{code-block} python
transcription_dict['A']
```
Will give the output:
```{code-block} python
:class: no-copybutton
'U'
```
``````


### Tuples
Tuples are immutable ordered collections of elements. They are very similar to lists, but unlike lists, tuples cannot be changed (hence, immutable). Consequently, they can be used as keys for a dictionary ([](#example_tuple_as_dict_key)).

(example_tuple_as_dict_key)=
``````{prf:example} Tuples can be keys of a dictionary
```{code-block} python
plant_dict = {("Arabidopsis", "thaliana") : "thale cress"}
```
```{code-block} python
plant_dict
```
Will give the output:
```{code-block} python
:class: no-copybutton
{("Arabidopsis", "thaliana") : "thale cress"}
```
``````

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 3.4.3 Tuples
```

#### Creating a Tuple
Tuples can be created by "tuple display" ([](#example_tuple_display)). To create a single-element tuple, you need to include a comma after the element ([](#example_tuple_single_element)).

(example_tuple_display)=
``````{prf:example} Create a tuple using tuple display
```{code-block} python
taxonomy = ("Eukaryota", "Plantae", "Tracheophyta", "Magnoliopsida", "Brassicales", "Brassicaceae", "Arabidopsis", "Arabidopsis thaliana")
```
```{code-block} python
taxonomy 
```
Will give the output:
```{code-block} python
:class: no-copybutton
('Eukaryota', 'Plantae', 'Tracheophyta', 'Magnoliopsida', 'Brassicales', 'Brassicaceae', 'Arabidopsis', 'Arabidopsis thaliana')
```
``````

(example_tuple_single_element)=
``````{prf:example} Create a tuple using tuple display
```{code-block} python
taxonomy = ("Eukaryota", "Plantae", "Tracheophyta", "Magnoliopsida", "Brassicales", "Brassicaceae", "Arabidopsis", "Arabidopsis thaliana")
```
```{code-block} python
taxonomy 
```
Will give the output:
```{code-block} python
:class: no-copybutton
('Eukaryota', 'Plantae', 'Tracheophyta', 'Magnoliopsida', 'Brassicales', 'Brassicaceae', 'Arabidopsis', 'Arabidopsis thaliana')
```
``````

#### Tuple Indexing



### Sets
#### Creating a Set

#### Set operations


## Exercises
