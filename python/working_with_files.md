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
A text file is organized in lines. There are newline ('\n') characters at the end of each line. Moreover, lines may have further internal structure, e.g. CSV files where fields/columns are separated by a comma. Program files (e.g. Python) are also text files. When reading from/writing to text files, the values are strings.

A binary file is a (long) sequence of bytes, which are not human readable, e.g. XLSX files. Any structure within a binary file is defined by the application that reads/writes it. They are typically used by a software library for reading/writing. They can contain floats, dates, and other types in machine format. 

## Structure of (Text) Files

## Processing (Text) Files

### Reading a File

### Writing a File

## Python Utilities for (Text) Files

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