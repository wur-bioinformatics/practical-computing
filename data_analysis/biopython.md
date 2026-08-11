---
title: Biopython
label: biopython
abbreviations:
    BOLD: Barcode Of Life Data
bibliography:
    .bib
---

```{important} Learning outcomes
After completing this section you should be able to:
- learning_outcome1
- learning_outcome2
```

## Introduction
[Biopython](https://biopython.org/) is a collection of tools that makes it easy to work with biological data in Python. General Python is excellent for programming, but it doesn't understand DNA or proteins. Biopython provides specialized tools for molecular biology and bioinformatics. It is one of the oldest and most widely used bioinformatics libraries. It is used in research institutes, hospitals, universities, and biotech companies.


(section_biopython_sequence_objects)=
## Biopython Sequence Objects
Without Biopython DNA is just text: `ATGGCCATCG...`. With Biopython DNA becomes a biological object. A sequence can be stored in a `Seq` object on which we can call its methods. The `Seq` object behaves similarly to a Python string, so we can use some of the string methods on it. However, other methods relating to bioinformatics questions can be applied on the `Seq` object. In addition, the `Seq` object  `translate()` method differs from the basic Python string `.translate()` method by doing biological translation.

We can immediately ask questions on the `Seq` object such as:
- How long is the sequence? 
- What is the GC percentage? 
- What protein does it encode? 
- What is the reverse complement?

### Sequence Manipulation
To use the `Seq` object, first we need to import it:
```{code-block} python
from Bio.Seq import Seq
```

On this `Seq` object, we can perform various operations. As mentioned [before](#section_biopython_sequence_objects), we can perform string operations such as obtaining the length with `len()` ([](#example_biopython_seq_len)) and taking a slice ([](#example_biopython_seq_slice)). We can also obtain the reverse complement using the `.reverse_complement()` method ([](#example_biopython_seq_revc)), or translate the sequence into protein using the `.translate()` method ([](#example_biopython_seq_translate)).



(example_biopython_seq_len)=
``````{prf:example} Get the length of a DNA sequence
Define a DNA sequence using the `Seq` object:
```{code-block} python
seq = Seq("ATGGCCATTGTA")
```
Get the length using `len()`:
```{code-block} python
len(seq)
```
Will give the output:
```{code-block} python
:class: no-copybutton
12
```
``````

(example_biopython_seq_slice)=
``````{prf:example} Take a slice of a DNA sequence
Define a DNA sequence using the `Seq` object:
```{code-block} python
seq = Seq("ATGGCCATTGTA")
```
Take a slice similar to string slicing:
```{code-block} python
seq[:6]
```
Will give the output:
```{code-block} python
:class: no-copybutton
Seq('ATGGCC')
```
``````


(example_biopython_seq_revc)=
``````{prf:example} Get the reverse complement of a DNA sequence
Define a DNA sequence using the `Seq` object:
```{code-block} python
seq = Seq("ATGGCCATTGTA")
```
Get the reverse complement:
```{code-block} python
seq.reverse_complement()
```
Will give the output:
```{code-block} python
:class: no-copybutton
Seq('TACAATGGCCAT')
```
``````

(example_biopython_seq_translate)=
``````{prf:example} Translate a DNA sequence into a protein sequence
Define a DNA sequence using the `Seq` object:
```{code-block} python
seq = Seq("ATGGCCATTGTA")
```
Translate into protein:
```{code-block} python
seq.translate()
```
Will give the output:
```{code-block} python
:class: no-copybutton
Seq('MAIV')
```
``````

```{seealso} Further Reading
- Biopython tutorial on [Sequence objects](https://biopython.org/docs/latest/Tutorial/chapter_seq_objects.html)
```

## Biopython Sequence Annotation Objects
A bioinformatician spends a surprising amount of time reading files. Fortunately, Biopython already understands most common formats ([](#table_biological_file_formats)). It can store the contents of biological records in a `SeqRecord` object. 

(table_biological_file_formats)=
:::{list-table} Biological file formats
:header-rows: 1
* - Format
  - Contents
* - FASTA
  - DNA or protein sequences
* - FASTQ
  - Sequence + sequencing quality
* - GenBank
  - Sequence + annotations
* - EMBL
  - Annotated sequences
* - PDB
  - Protein structures
* - GFF/GTF
  - Gene annotation
:::

### Reading Biological Data
To use the `SeqRecord` object, we can use the biopython `SeqIO` utilities to read in a file. First, import `SeqIO`:
```{code-block} python
from Bio. import SeqIO
```
Then read in a file:
```{code-block} python
:class: no-copybutton
record = SeqIO.read(
    "sequence.fasta",
    "fasta"
)
```
The `.read()` method opens the file, recognizes the format and immediately creates the `SeqRecord` object to store the records. In [](#figure_seqrecord), we can see a graphic representation of what is stored in a GenBank `SeqRecord`.

(figure_seqrecord)=
:::{figure} img/SeqRecord.png
A biopython SeqRecord object of a GenBank file and its contents
:::


```{seealso} Further Reading
- Biopython tutorial on [Sequence annotation objects](https://biopython.org/docs/latest/Tutorial/chapter_seq_annot.html)
```

## Exercises
In today's exercises, you will create the first steps in an automated species identification pipeline. We will do so by combining Python code and command line tools in a Jupyter Notebook.

We aim to identify the three mosquitoes, X1, X2, and X3, from which a small part of the mitochondrial Cytochrome Oxidase I ([CO1](https://en.wikipedia.org/wiki/Cytochrome_c_oxidase_subunit_I)) gene has been sequenced. These can be used to identify the species by comparing to a global database of mosquito DNA 'barcodes', the [BOLD database](http://www.boldsystems.org/).


For these exercises, we will work with a Jupyter Notebook on a remote server.

``````{exercise} Start the Jupyter Notebook on the remote server
We will use the Jupyter Notebook W4D4 that can be downloaded along with the data from Brightspace. 

Similar to previous days, follow the instructions on Brightspace "Starting a Jupyter Notebook on a remote server and connecting via an SSH tunnel".
``````

Again, the instructions are in the Jupyter Notebook.

``````{exercise} First explorations
- Run Linux commands in a Jupyter Notebook by prepending them with an exclamation mark
- Run Linux commands in a Jupyter Notebook by using the `check_output()` function from the `subprocess` module
- Show the contents of a fasta file, using a Linux command, and two Python ways
- Use `SeqIO` from Biopython to parse a fasta file into a `SeqIO` object, a `SeqRecord` object
- Use `SeqRecord` methods and attributes to get familiar with the data structure
- Get the reverse complement of a sequence using a `SeqRecord` method
- Translate all open reading frames of a sequence using a `SeqRecord` methods
- Use Linux tools to explore properties of the BOLD mosquito table
``````

``````{exercise} Converting from tabular to FASTA format
Convert the tab-delimited file to fasta, so that we can convert it subsequently to a blastable database.
- Open and close the tsv file
- Explore the contents of the tsv file
- Use Biopython utilities to create a FASTA file from a list of `SeqRecord` objects
``````

``````{exercise} Blasting the mystery mosquito data
- Create a BLAST database from the database FASTA file
- Blast the mystery mosquitos against the BLAST database using `check_output()`
- Use `glob` module to create a list of files based on path and wildcards
- Apply the `glob` syntax to blast all mystery moquitos in one script
``````