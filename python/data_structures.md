---
title: Data Structures
label: python_data_structures
abbreviations:
    
bibliography:
    .bib
---

```{important} Learning outcomes
After completing this section you should be able to:
- Describe the main characteristics of lists, dictionaries, tuples, and sets.
- Create and access data stored in these Python data structures.
- Explaint the difference between indexing and slicing.
- Modify data structures and apply basic operations such as indexing, slicing, and set operations.
```

## Introduction

(section_data_structures)=
## Data Structures
Apart from the simple data types discussed in [](#data_types_section), Python has built-in data structures to organize data. Here, we will discuss the main ones: lists, dictionaries, tuples, and sets. There are also more complex data structures within Python, but they are not necessary for the problems at hand.

(section_ds_lists)=
### Lists
Lists are ordered collections of items. The items within a list can be of different data types ([](#example_list_different_data_types)), and the same value can occur multiple times ([](#example_list_same_values)). Each item in a list has an index, starting at `0`. The last item in the list has the index `-1`. In other programming languages, lists are often called "arrays". Though, Python lists are more flexible than standard arrays. Lists can grow and shrink: they are mutable. Most often, elements are added to the end of the list, but it also possible to add or remove internal elements. Additionally, we can concatenate lists (similar as for {term}`strings<string>`.

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

Second, we can create a list by repeating a single-element list ([](#example_list_intialise_repeating_zeros), [](#example_list_intialise_repeating_None)). This can be useful when you already know how long your final list will be, and you want to initialize it before altering the values of each item (with for example a loop). 

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

Last, a list can be created using the `list()` function ([](#example_list_list_function)). The {term}`argument` supplied to `list()` should be an iterable.

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

(section_list_indexing_and_slicing)=
#### List Indexing and Slicing
Similar to [](#section_str_indexing_and_slicing), we can also access elements in lists using indexing (example_list_indexing) and obtain a part of a list using slicing ([](#example_list_slicing)). Again, negative indices mean counting from the end, with `[-1]` taking the last element. 

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

:::{note} Note
Square brackets (`[]`) are used: 
- when creating a list using list display
- when indexing or slicing from a list
:::

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
Tuples can be created by "tuple display" ([](#example_tuple_display)). To create a single-element tuple, you need to include a comma after the element ([](#example_tuple_single_element)), otherwise it will not be stored as a tuple ([](#example_tuple_single_element_incorrect)).

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
``````{prf:example} Create a single-element tuple using tuple display
```{code-block} python
year = (2026,)
```
```{code-block} python
year 
```
Will give the output:
```{code-block} python
:class: no-copybutton
(2026,)
```
``````

(example_tuple_single_element_incorrect)=
``````{prf:example} Create a single-element tuple - incorrect (without comma)
```{code-block} python
year = (2026)
```
```{code-block} python
year 
```
Will give the output:
```{code-block} python
:class: no-copybutton
2026
```
```{code-block} python
type(year)
```
Will give the output:
```{code-block} python
:class: no-copybutton
<class 'int'>
```
``````

#### Tuple Indexing and Slicing
Tuples are indexed and sliced exactly as [lists](#section_list_indexing_and_slicing) ([](#example_tuple_indexing_slicing)). The one difference is that, since tuples are immutable, you cannot change values within tuples by assigning new values to an index or slice of a tuple. 

(example_tuple_indexing_slicing)=
``````{prf:example} Tuple indexing and slicing
Given the following tuple:
```{code-block} python
taxonomy = ("Eukaryota", "Plantae", "Tracheophyta", "Magnoliopsida", "Brassicales", "Brassicaceae", "Arabidopsis", "Arabidopsis thaliana")
```
Getting the second to last element using indexing:
```{code-block} python
taxonomy[-2]
```
Will give the output:
```{code-block} python
:class: no-copybutton
'Arabidopsis'
```

Getting the first three elements using slicing:
```{code-block} python
taxonomy[:3]
```
Will give the output:
```{code-block} python
:class: no-copybutton
('Eukaryota', 'Plantae', 'Tracheophyta')
```
The result of a slice is a tuple.
``````

### Sets
Sets are unordered collections of immutable elements containing no duplicates. Because they are unordered, elements do not have an index and sets cannot be indexed or sliced. As no duplicates are allowed, if you create a set with duplicate elements, the resulting set will contain only one of them. Sets can consists of multiple data types, but only immutable data types.

#### Creating a Set
You can create a set using "set display" ([](#example_set_display_multiple_elements), [](#example_set_display_single_element)). They are created by using curly braces (`{}`). By not using a colon (`:`), the set is distinguished from a dictionary.

(example_set_display_multiple_elements)=
``````{prf:example} Create a set of multiple elements using set display
```{code-block} python
h = {1, 2, 3, 4, 5}
```
```{code-block} python
h
```
Will give the output:
```{code-block} python
:class: no-copybutton
{1, 2, 3, 4, 5}
```
``````

(example_set_display_single_element)=
``````{prf:example} Create a set of a single element using set display
```{code-block} python
i = {1}
```
```{code-block} python
i
```
Will give the output:
```{code-block} python
:class: no-copybutton
{1}
```
``````

You can also create a set by converting a list with the `set()` function ([](#example_set_function_list)). When there are duplicates in the list, they will be removed by creating a set from the list ([](#example_set_function_list_duplicates)).

(example_set_function_list)=
::::::{prf:example} Create a set of a list using `set()`
First, create a list:
```{code-block} python
j = [1, 2, 3, 4, 5]
```
Create a set from the list using `set()`:
```{code-block} python
k = set(j)
```
```{code-block} python
k
```
Will give the output:
```{code-block} python
:class: no-copybutton
{1, 2, 3, 4, 5}
```
::::::

(example_set_function_list_duplicates)=
::::::{prf:example} Create a set of a list with duplicates using `set()`
Let's create a list with duplicates (for example from [](#example_list_same_values)):
```{code-block} python
b = ["ATG", "TATA", "ATG"]
```
Create a set from the list using `set()`:
```{code-block} python
l = set(b)
```
```{code-block} python
l
```
Will give the output:
```{code-block} python
:class: no-copybutton
{'TATA', 'ATG'}
```
::::::

Sets come with methods for adding and removing elements. You can add an element with the `.add()` method ([](#example_sets_add_element)). If you supply it with a duplicate entry as argument, nothing will change. You can remove an item with either the `.remove()` method ([](#example_sets_remove_element)) or the `.discard()` method. The only difference is that the `.discard()` method does not give an error when the item does not exist in the set.

(example_sets_add_element)=
::::::{prf:example} Add an element to a set using `add()`
Let's add a DNA string to the `l` set of [](#example_set_function_list_duplicates):
```{code-block} python
l.add("ATA")
```
```{code-block} python
l
```
Will give the output:
```{code-block} python
:class: no-copybutton
{'TATA', 'ATA', 'ATG'}
```
::::::

(example_sets_remove_element)=
::::::{prf:example} Remove an element to a set using `remove()`
Let's remove the `"ATA"` DNA string to the `l` set of [](#example_sets_add_element):
```{code-block} python
l.remove("ATA")
```
```{code-block} python
l
```
Will give the output:
```{code-block} python
:class: no-copybutton
{'TATA', 'ATG'}
```
::::::

#### Set Operations
Sets have methods for checking the intersection ([](#example_set_intersection)), union ([](#example_set_union)), and difference ([](#example_set_difference)) of two sets. 

(example_set_intersection)=
::::::{prf:example} Check the intersection of two sets using `.intersection()`
First, define two sets:
```{code-block} python
s1 = {1, 2, 3, 4}
```
```{code-block} python
s2 = {3, 4, 5, 6}
```
Check for intersection (or overlap):
```{code-block} python
s1.intersection(s2)
```
Will give the output:
```{code-block} python
:class: no-copybutton
{3, 4}
```
::::::

(example_set_union)=
::::::{prf:example} Check the union of two sets using `.union()`
First, define two sets:
```{code-block} python
s1 = {1, 2, 3, 4}
```
```{code-block} python
s2 = {3, 4, 5, 6}
```
Check for union (or combined elements):
```{code-block} python
s1.union(s2)
```
Will give the output:
```{code-block} python
:class: no-copybutton
{1, 2, 3, 4, 5, 6}
```
::::::


(example_set_difference)=
::::::{prf:example} Check the difference between one set and another using `.difference()`
First, define two sets:
```{code-block} python
s1 = {1, 2, 3, 4}
```
```{code-block} python
s2 = {3, 4, 5, 6}
```
Check for difference:
```{code-block} python
s1.difference(s2)
```
Will give the output:
```{code-block} python
:class: no-copybutton
{1, 2}
```
:::{note} Note
`.difference()` returns a set containing items that exist only in the first set, and not in both sets. So it only returns the elements of `s1` that differ from `s2`.

If you want to obtain the elements that differ in both sets use `.symmetric_difference()`
:::
::::::



## Exercises
### Conceptual: Types of Data
``````{exercise} Types of Data 1 - Together
We look at the date contained in the file of Crane data. For this exercise we need just a part of the data: `first_and_last_100_lines_crane_data.csv`.

**For each column, what is a suitable type (Integer, Float, String, etc.)?**
``````

``````{exercise} Types of Data 2 - Alone
Take another data file that you have been using before (for example, you could use file `SRR1740460_example.fq` from week 1 day...).

**Find out which kinds of data are present**; usually not more than 10 or 20.

**For each kind of data you found, determine a suitable type (e.g. Integer, Float, String).**

**Do you need more types than listed in the book?** No problem, that happens in practice. Then describe those types.

Probably the same groups of (kinds of) data occur over and over again. **Find a suitable structured type for representing the repeated groups.**
``````




### Data Structures
``````{exercise} Start W2D3 Jupyter Notebook
Download the W2D3 Jupyter Notebook from Brightspace.

Just like previous days, run the notebook with `jupyter notebook` in the terminal.

The Jupyter Notebook contains all the instructions.
``````



``````{exercise} List indexing
Create fixed lists and obtain elements from them.
``````

``````{exercise} List slicing
Obtain sub-lists from other lists.
``````

``````{exercise} Assigning to (parts of) a list
Replace elements of lists, or even replace sub-lists.
``````


``````{exercise} 
Create fixed dictionaries and retrieve data from them.
``````

``````{exercise} 
Start with a small distionary and add data to it.

``````





### Conceptual: Data Structure for Storing a Data Set 

``````{exercise} Data structure for storing a data set (in memory)
Retrieve file `plantsvshuman_outmft6.csv` from Brightspace and open the file. [Which program do you use?] 

This file is a slightly edited output file from Blast, comparing plant proteins to human proteins. 

Explanation of columns can be found [here](http://www.drive5.com/usearch/manual/blast6out.html).

When we want to further process this kind of data, we have to read the file (or a part of it) into memory. The data structure in memory will consists of lists or dictionaries, with constituent parts that might be lists or dictionaries again. Ultimately, the basic elements of the data structure will be strings, numbers, and possibly other elementary data.

The data structure in memory might closely resemble the structure of the file, or the data structure in memory can be entirely different from the structure of the file.

**First, define a data structure that closely resembles the structure of the file.**
[Even then, there are multiple solutions...]

**Next, define a alternate data structure that uses a different organization of the data.**
``````