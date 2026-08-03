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

### Writing a File

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