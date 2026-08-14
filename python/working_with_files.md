---
title: Working with Files
label: working_with_files
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

## Text Files vs. Binary Files
A text file is organized in lines. There are newline (`\n`) characters at the end of each line. Moreover, lines may have further internal structure, e.g. CSV files where fields/columns are separated by a comma. Program files (e.g. Python) are also text files. When reading from/writing to text files, the values are strings.

A binary file is a (long) sequence of bytes, which are not human readable, e.g. XLSX files. Any structure within a binary file is defined by the application that reads/writes it. They are typically used by a software library for reading/writing. They can contain floats, dates, and other types in machine format. 

## Structure of Text Files
Data is often structured in a certain way in text files. Many text files contain a header line as the first line in the file. For example, in a CSV file, the first line defines the column names ([](#example_text_file_csv)).

Ideally, a text file stores one record per line as this makes reading the data easier. It is possible to have more than one record on a line, but it is not usual. When there are multiple lines for one record, processing becomes more complicated. Then, we need special symbols to define the start (and/or the end) of a record. For example, in a FASTA file, the sequences can be spanned over multiple lines. There, a new record starts with '`>`'. When there are either multiple lines per record or multiple records per line, it is possible that elements are repeated per line/record.

(example_text_file_csv)=
``````{prf:example} CSV file
```{code-block} python
:filename: WoF.txt
name,relative chance
Alice in Wonderland,47.77
Favorite Student,92.02
James Brown,29.23
Jane Doe,67.98
John Doe,45.50
Moby Dick,56.54
Monty Python,87.33
Nobody Special,15.77
Robin Hood,53.06
Winny the Pooh,25.73
```
``````

## Processing Text Files

### Reading a File
When reading a file, the program usually follows the structure of the input file. While the file is being read, the data is either stored in a data structure in memory or written into an output file per record. 

When there is a header line present, it is best to first read it, so it will not be stored as a record. Then, you can loop over the remaining lines of the file. Within the loop, you process the text by splitting the line, interpreting the text, and when necessary by converting from string to other data types.


(example_text_file_reading)=
``````{prf:example} Read a text file into a dictionary
Given  `WoF.txt` in [](#example_text_file_csv), read the contents into a dictionary.

First, initialize an empty dictionary so we can fill it later:
```{code-block} python
table = {}
```
Then, open the file:
```{code-block} python
infile = open('WoF.txt')
```
Read the first line, so we ignore the header line when storing the records:
```{code-block} python
header = infile.readline() # ignore
```
Then, loop over the remaining lines, storing each record as a separate entry in the dictionary:
```{code-block} python
for line in infile:
    cells = line.strip().split(',')
    assert len(cells) == 2 # explicitly assume
    name = cells[0]
    chance = float(cells[1])
    table[name] = chance
```
Last, explicitly close the file: 
```{code-block} python
infile.close()
```
Let's see what is in the dictionary:
```{code-block} python
table
```
Will give the output:
```{code-block} python
:class: no-copybutton
{'Alice in Wonderland': 47.77, 'Favorite Student': 92.02, 'James Brown': 29.23, 'Jane Doe': 67.98, 'John Doe': 45.5, 'Moby Dick': 56.54, 'Monty Python': 87.33, 'Nobody Special': 15.77, 'Robin Hood': 53.06, 'Winny the Pooh': 25.73}
```
``````


### Writing a File
When writing to a file, the program follows the structure of the data as it is stored in memory (or of the input file when writing to the output file while processing the input file). We create the structure of the output file by writing to it. If applicable, first, write a header line. Then, loop over the data structure (or input file). This is often done using a `for` loop, but it depends on the data structure. Inside the loop, any data type needs to be converted to a string. Additionally, newlines (`\n`) need to be written explicitly. 

(example_text_file_writing)=
``````{prf:example} Write a table to a text file from a dictionary
Given the dictionary in [](#example_text_file_reading), write the table to a text file.

First, open the file:
```{code-block} python
outfile = open('WoF_out.txt', 'w')
```
Write the header line:
```{code-block} python
outfile.write('relative chance,name\n')
```
Loop over the dictionary and write each line:
```{code-block} python
for name in table:
    chance = table[name]
    outfile.write(str(chance))
    outfile.write(',')
    outfile.write(name)
    outfile.write('\n')
```
Last, explicitly close the file:
```{code-block} python
outfile.close()
```

Now, if we print the contents of the file to the screen:
```{code-block} bash
cat WoF_out.txt
```
Will give the output:
```{code-block} bash
:class: no-copybutton
relative chance,name
47.77,Alice in Wonderland
92.02,Favorite Student
29.23,James Brown
67.98,Jane Doe
45.5,John Doe
56.54,Moby Dick
87.33,Monty Python
15.77,Nobody Special
53.06,Robin Hood
25.73,Winny the Pooh
```
``````


## Python Utilities for Text Files
Python contains many utilities for processing (text) files in its standard library. Some useful methods for file objects and string objects will be shortly discussed here.

(section_wwf_file_methods)=
### File Methods
Python has a dedicated type for files called a file object (or file handle) which connects Python to a file on the disk. The data remains on the disk, meaning it is not read into the Python session when creating a file object. The file object only contains administrative data and a "buffer". To create a file object, we need the file name or path of a file on disk as a string. This file object data type has many useful methods for processing the file.

Here, we will discuss some file object methods that can be used to open, close, and read files. Some are illustrated in [](#example_file_reading_file_methods) and [](#example_file_writing_file_methods).

(example_file_reading_file_methods)=
``````{prf:example} Read WoF.txt into a dictionary using file methods
Read the `WoF.txt` from [](#example_text_file_csv) into a dictionary:
```{code-block} python
:linenos:
:emphasize-lines: 2,3
table = {}
with open('WoF.txt') as infile:
    header = infile.readline() # ignore
    for line in infile:
        cells = line.strip().split(',')
        assert len(cells) == 2 # explicitly assume
        name, chance = cells # unpack at once
        chance = float(chance)
        table[name] = chance
```
In line **2**, we use `open()` to create a file object.\
In line **3**, we use `.readline()` to read the first line (the header line).
``````

(example_file_writing_file_methods)=
``````{prf:example} Writing the table to WoF_out.txt using file methods
Given the dictionary in [](#example_file_reading_file_methods), write the table to a text file:
```{code-block} python
:linenos:
:emphasize-lines: 1,2,6
with open('WoF_out.txt', 'w') as outfile:
    outfile.write('relative chance,name\n')
    for name in table:
        chance = table[name]
        line = str(chance) + ',' + name + '\n'
        outfile.write(line)
```
In line **1**, we use `open()` to create a file object and specify the mode as writing.\
In line **2**, we use `.write()` to write the header line.\
In line **5**, we use `.write()` to write the `line` which contains each element in the table formatted as a CSV file. Note that the newline character is explicitly added.
``````

#### `open()` and `.close()`
To create the file object, we use function `open()`:
```{code-block} python
:class: no-copybutton
open(file_name, access_mode)
```
where `file_name` is the name (or path) of the file we want to open and the `access_mode` is the mode in which the file will be opened. The default mode (without specifying it) is `'r'` for **r**ead. If we want to **w**rite to a file, we use `'w'`. 

After we are done processing the file, we need to explicitly close is using the file object method `.close()`. This ensures Python disconnects from the file on disk (and the write "buffer"). 

```{code-block} python
:class: no-copybutton
file_name.close()
```

```{caution} You should always close your files
It is best practice to close your files. If you do not, you might not be able to see the changes made to the file because of buffering. Additionally, sometimes other programs cannot access the file while it is still open.
```

To implicitly close the file after being done processing, we can use the `with` statement:
```{code-block} python
:class: no-copybutton
with open(file_name) as my_file:
    ...
```
In the `with` statement, we write the program for processing the file. This adds a level of indentation, but guarantees closing the file.


#### `.write()`
To write a string to a file, we can use the file object method `.write()`:
```{code-block} python
:class: no-copybutton
file_name.write(text)
```
where `text` is a string to write to the file. If we want to write multiple lines (for example, one record per line), we need to write the newline character explicitly.


#### `.readline()`
To read one line from a file, we can use file object method `.readline()`:
```{code-block} python
:class: no-copybutton
file_name.readline()
```
This method should **not** be inside a loop that goes over each line of the file. Instead, we can use it to skip a line such as a header line ([](#example_text_file_reading)).


#### `.readlines()` and `.read()`
To read the whole file into memory, we can use either `.readlines()` or `.read()`. However, if you are reading in huge files, this can be problematic.

The `.readlines()` method returns a list with each line as an element of the list. If you want to process the file contents, you still need to loop over the list. Therefore, it is better practice to loop over the lines of a file, process each line, and only store what you need.

The `.read()` method returns the specified number of bytes from the file as a string, defaulting to `-1` which means the whole file. Again, to process the file contents, you will need to go over this string and take out the relevant bits. If you read in a huge file, this can be extremely tedious.


### Looping over Files
When processing an input file, it is best to loop over the file content line by line:
```{code-block} python
:class: no-copybutton
:linenos:
:emphasize-lines: 2
with open(file_name) as my_file:
    for line in my_file:
        # do something
```
`line` is then one complete line (including a newline character) with string as the data type.

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 3.7.1 Text Files
```

### String Methods
Because lines in a file are essentially strings, we can use string methods on them for processing. Some relevant ones are summarized in [](#table_str_methods_file_processing) and illustrated in [](#example_file_processing_str_methods).

(table_str_methods_file_processing)=
:::{list-table}
:header-rows: 1
* - String method
  - Parameter(s)
  - Example usage
  - Description
* - `.strip(c)`
  - `c`: string, character(s) to remove, by default any whitespace (spaces, tabs, newlines)
  - `line.strip()`
  - Removes any leading and trailing (both ends) `c` from the string
* - `.lstrip(c)`
  - `c`: string, character(s) to remove, by default any whitespace (spaces, tabs, newlines)
  - `line.lstrip()`
  - Removes any leading (**l**eft hand end) `c` from the string
* - `.rstrip(c)`
  - `c`: string, character(s) to remove, by default any whitespace (spaces, tabs, newlines)
  - `line.rstrip()`
  - Removes any trailing (**r**ight hand end) `c` from the string
* - `.split(c)`
  - `c`: string, character(s) to split on, by default any whitespace (spaces, tabs, newlines)
  - `line.split(',')`
  - Splits a string on a character into a list of strings. Note: any trailing '\n' goes into the last element of the resulting list
:::

(example_file_processing_str_methods)=
``````{prf:example} Read WoF.txt into a dictionary using string methods
Read the `WoF.txt` from [](#example_text_file_csv) into a dictionary:
```{code-block} python
:linenos:
:emphasize-lines: 5
table = {}
with open('WoF.txt') as infile:
    header = infile.readline() # ignore
    for line in infile:
        cells = line.strip().split(',')
        assert len(cells) == 2 # explicitly assume
        name, chance = cells # unpack at once
        chance = float(chance)
        table[name] = chance
```
In line **5**, we use `.strip()` to first strip off both leading and trailing whitespace, and then use `.split(',')` to split the line on commas into a list. 
``````


## Processing Multiple Files
It is possible to process multiple files either at the same time in one loop, or consecutively in multiple loops. When processing at the same time, we use limited amount of memory. When processing consecutively, we must store (almost) all data in memory, which makes it infeasible for large file. 

We can process multiple files consecutively using nested loops or a sequence of loops. We would then store the data while reading and write later separately. We can store the data in a list when the order is important. However, if the order is different in the multiple files, this is inefficient. Then, it might be better to use a dictionary, where the order is the insertion order. When writing the output file, we would then loop over the created data structure(s).

## Exercises
All exercises of today essentially handle one record at a time. So, reading and writing have to be interleaved, keeping very little information in memory at the same time.
- In the first exercise, the program must copy complete lines from input to output, but only those lines that meet some criteria.
- The second exercise deals with multi-line inputs from FASTA files. We use [Rosalind](https://rosalind.info/problems/locations/) problem "(DNA) Counting DNA Nucleotides" as an example application.
- The last exercise creates multiple output lines per input line.

``````{exercise} Start the W3D1 Jupyter Notebook
Download the W3D1 Jupyter Notebook from Brightspace.

Just like previous days, run the notebook with `jupyter notebook` in the terminal.
``````

Here, we define the assignments. The Jupyter notebook contains additional steps and hints.


:::{note} Using a Jupyter Notebook for reading files
Please note, that experimenting in a Jupyter notebook for reading files can be awkward. 

Repeating a cell that reads from a file will often not give the same result again. It will only do so if code for opening and closing the file is included in the same cell. 

Instead, we will mostly experiment with fixed values for lines as if read from file.
:::


### Selecting Lines from a Text File
``````{exercise} Selecting lines from a text file
Find and copy those lines from file `plantsvshuman_outmft6.csv` for which query and target have the same length (i.e. where `EndQ‒StartQ` is equal to `EndT‒StartT`). Note: This is not the same as `#gaps-open=0`

The first line of the input file is a header line that can be copied directly to output file. 

For all other lines, we have to break the line up into constituent parts and interpret those parts. This is called parsing. When the line passes the test (query and target have the same length), the complete line is written to the output file.

The program has to write output lines to the output file while reading the input file; so don't keep more than one line in memory at the same time.

Let the program write to file `plantsvshuman_selected.csv`.

See file `plantsvshuman_selected_expected.csv` for the expected output.
``````


### Reading FASTA Files
(exc_wwf_reading_fasta)=
``````{exercise} (DNA) Counting DNA Nucleotides
In the first set of Python exercises (*#! cross ref?*), we have done the essential part of [Rosalind](https://rosalind.info/problems/locations/)'s problem "(DNA) Counting DNA Nucleotides". 

*#! this bit is confusing, what are we trying to say?*\
For some other problems on Rosalind (e.g. GC), we have to be able to read a file in FASTA format. 

For Rosalind's "(ORF) Open Reading Frames" problem, we have done all other steps last week; for completely finishing that problem, the program should read a FASTA file again. *#! until here*

Now, we will apply Rosalind's DNA to FASTA files.


A FASTA file can contain multiple sequences, were one sequence usually spans multiple lines. At the start of each sequence, one line that starts with a right-pointed bracket (or larger sign, `>`) gives meta-information on that sequence.

For example, a sample input file from Rosalind is:
```{code-block} bash
>Rosalind_6404
CCTGCGGAAGATCGGCACTAGAATAGCCAGAACCGTTTCTCTGAGGCTTCCGGCCTTCCC
TCCCACTAATAATTCTGAGG
>Rosalind_5959
CCATCGGTAGCGCATCCTTAGTCCAATTAAGTCCCTATCCAGGCGCTCCGCCGAAGGTCT
ATATCCATTTGTCAGCAGACACGC
>Rosalind_0808
CCACCCTCGTGGTATGGCTAGGCATTCAGGAACCGGAGAACGCTTCAGACCAGCCCGGAC
TGGGAACCTGCGGGCAGTAGGTGGAAT
```
Such input is hard to process by `input()`. But once we know files *#! what?*, we can let Python assemble the lines that belong together.

The assignment is to make a Python program that reads a file in FASTA format, and for each sequence write the identification and counts of nucleotides to another text file.

The program does not have to remember any sequences after their nucleotide counts were computed.

The output file corresponding to the sample input file above looks like this:
```{code-block} bash
:class: no-copybutton
Rosalind_6404 A: 18 C: 25 G: 18 T: 19
Rosalind_5959 A: 19 C: 28 G: 17 T: 20
Rosalind_0808 A: 20 C: 24 G: 29 T: 14
```
``````


### Flattening Matrix Data
``````{exercise} Flattening matrix data
Write a program that "flattens" file `GeneDistanceMatrix.csv` to a file `GeneDistanceTable.csv`.

The result file should have three columns:\
from: ID taken from the first column in the matrix\
to: ID taken from the first row in the matrix\
distance: float value from the cell in the corresponding row and column of the matrix\

The program has to keep all column IDs (first row of the matrix) and the current row ID in memory; all float values can be written immediately.
``````