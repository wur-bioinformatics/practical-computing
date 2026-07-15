---
title: Advanced Unix Commands and Pipes
label: adv_unix_commands_pipes
abbreviations:
    BLAST: Basic Local Alignment Search Tool
bibliography:
    advanced_unix_commands_and_pipes.bib
---

```{important} Learning outcomes
After completing this section you should be able to:
- be proficient in command line (shell) usage *#!this should be more specified I think*
```

## Introduction
In this section, you will learn some more advanced Linux command-line tools and connect them using pipelines. 

## Advanced Unix Commands
Now that you have mastered the basics of using the {term}`shell` in {numref}`intro_to_computing`, let's explore some more advanced command-line tools. The tools explored here are by no means an exhaustive list of Unix tools, but these tools are very useful for handling biological data (files). 

``````{caution} Remember how to search for help
Part of mastering the command line shell is knowing how to search for help. Most tools have an extensive help page that is printed to screen when running, depending on the tool, either:
```{code-block} bash
<tool_name> -h
```
or
```{code-block} bash
<tool_name> --help
```
Alternatively, you can open the manual via:
```{code-block} bash
man <tool_name>
```
``````

### wget
`wget` is a tool that can retrieve files from a URL ({numref}`Example %s <wget_example>`).

``````{admonition} Download a FASTA file
:name: wget_example
:numbered: true
:class: simple myst-example
:icon: false
```{code-block} bash
wget http://www.bioinformatics.nl/plants.fasta
```
``````

### cat
`cat` is a tool that prints the contents of a file (or standard input) to standard output (often the screen) ({numref}`Example %s <cat_example>`).

``````{admonition} Print contents of a FASTA file to screen
:name: cat_example
:numbered: true
:class: simple myst-example
:icon: false
```{code-block} bash
cat plants.fasta
```
The first lines of the output will be:
```{code-block} bash
:class: no-copybutton
>sp|Q43495|108_SOLLC Protein 108 OS=Solanum lycopersicum PE=2 SV=1
MASVKSSSSSSSSSFISLLLLILLVIVLQSQVIECQPQQSCTASLTGLNVCAPFLVPGSP
TASTECCNAVQSINHDCMCNTMRIAAQIPAQCNLPPLSCSAN
>sp|Q9XHP0|11S2_SESIN 11S globulin seed storage protein 2 OS=Sesamum indicum PE=2 SV=1
MVAFKFLLALSLSLLVSAAIAQTREPRLTQGQQCRFQRISGAQPSLRIQSEGGTTELWDE
RQEQFQCAGIVAMRSTIRPNGLSLPNYHPSPRLVYIERGQGLISIMVPGCAETYQVHRSQ
RTMERTEASEQQDRGSVRDLHQKVHRLRQGDIVAIPSGAAHWCYNDGSEDLVAVSINDVN
HLSNQLDQKFRAFYLAGGVPRSGEQEQQARQTFHNIFRAFDAELLSEAFNVPQETIRRMQ
SEEEERGLIVMARERMTFVRPDEEEGEQEHRGRQLDNGLEETFCTMKFRTNVESRREADI
FSRQAGRVHVVDRNKLPILKYMDLSAEKGNLYSNALVSPDWSMTGHTIVYVTRGDAQVQV
VDHNGQALMNDRVNQGEMFVVPQYYTSTARAGNNGFEWVAFKTTGSPMRSPLAGYTSVIR
AMPLQVITNSYQISPNQAQALKMNRGSQSFLLSPGGRRS
```
``````

### grep
`grep` is a tool that filters text for a given term. 

### wc

### cut

### sort

### tr

### awk

### sed

## Standard input, standard output, standard error

### Redirection

## Pipelines

## Practical

## Glossary
```{glossary}
shell
: Outermost layer of the operating system, acting as an intermediate between the user and the operating system.
```