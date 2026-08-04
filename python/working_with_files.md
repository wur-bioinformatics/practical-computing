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

### File Methods

#### `.open()`

#### `.close()`

#### `.write()`

#### `.readline()`

#### `.readlines()`

#### `.read()`

### Looping over Files

### String Methods

## Processing Multiple Files


## Exercises

### Selecting Lines from a Text File

### Reading FASTA Files

### Flattening Matrix Data