---
title: Biopython
label: biopython
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



## Biopython Sequence Annotation Objects


## Biological File Formats

## Biopython Utilities

### Reading Biological Data



## Exercises
