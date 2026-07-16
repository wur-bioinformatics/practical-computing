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
In this section, you will learn about Input/Output streams, some advanced Linux command-line tools and how to connect them using pipelines. 

## Input/Output streams
### Standard input, standard output, standard error
When running a program on the Linux command-line, you will always deal with the Input/Output streams: standard input (stdin), standard output (stdout), and standard error (stderr) ({numref}`io_streams`). 

```{figure} img/input-output_streams.png
:label: io_streams

Input/Output streams of Linux command-line
```

The stdin of a program is often your keyboard or a file. This is the input that you want the program to act upon. The stdout is by default the terminal screen, but some programs include an {term}`option` to redirect the output to a file. This is the output created by the program. The stderr is by default the terminal screen. This is the stream where error messages are directed towards. [@ibm_aix_2025; @nazeer_standard_2024; @geeksforgeeks_shell_nodate]



### Redirection
If a tool does not have the {term}`option` to redirect to a file, you can use the `>` symbol ({numref}`Example %s <redirect_example>`).
``````{admonition} Redirecting output to a file
:name: redirect_example
:numbered: true
:class: simple myst-example
:icon: false

```{code-block} bash
:class: no-copybutton
program > filename
```
``````

```{caution} Be careful when using >
Using the redirect symbol `>` will overwrite any contents of the file given, which cannot be undone. 
```

## Advanced Unix Commands
Now that you have mastered the basics of using the {term}`shell` in {numref}`intro_to_computing`, let's explore some more advanced command-line tools. The tools explored here are by no means an exhaustive list of Unix tools, but these tools are very useful for handling biological data (files). 

``````{caution} Remember how to search for help
Part of mastering the command line shell is knowing how to search for help. Most tools have a help page that is printed to screen when running (depending on the tool) either:
```{code-block} bash
<tool> -h
```
or
```{code-block} bash
<tool> --help
```
Alternatively, you can open the manual via:
```{code-block} bash
man <tool>
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
`grep` is a tool that filters text for a given term. It searches for a pattern in a file or standard input ({numref}`Example %s <grep_basic_example>`).

``````{admonition} Filter lines that contain 'sp'
:name: grep_basic_example
:numbered: true
:class: simple myst-example
:icon: false

```{code-block} bash
grep sp plants.fasta
```
The first 10 lines of the output will be:
```{code-block} bash
:class: no-copybutton
>sp|Q43495|108_SOLLC Protein 108 OS=Solanum lycopersicum PE=2 SV=1
>sp|Q9XHP0|11S2_SESIN 11S globulin seed storage protein 2 OS=Sesamum indicum PE=2 SV=1
>sp|P19084|11S3_HELAN 11S globulin seed storage protein G3 OS=Helianthus annuus GN=HAG3 PE=3 SV=1
>sp|P13744|11SB_CUCMA 11S globulin subunit beta OS=Cucurbita maxima PE=1 SV=1
>sp|Q05349|12KD_FRAAN Auxin-repressed 12.5 kDa protein OS=Fragaria ananassa PE=2 SV=1
>sp|O23878|13S1_FAGES 13S globulin seed storage protein 1 OS=Fagopyrum esculentum GN=FA02 PE=2 SV=1
>sp|O23880|13S2_FAGES 13S globulin seed storage protein 2 OS=Fagopyrum esculentum GN=FA18 PE=2 SV=1
>sp|Q9XFM4|13S3_FAGES 13S globulin seed storage protein 3 OS=Fagopyrum esculentum GN=FAGAG1 PE=1 SV=1
>sp|P83004|13SB_FAGES 13S globulin basic chain OS=Fagopyrum esculentum PE=1 SV=1
>sp|P48347|14310_ARATH 14-3-3-like protein GF14 epsilon OS=Arabidopsis thaliana GN=GRF10 PE=2 SV=1
```
``````

`grep` can be used with {term}`Regular Expressions <Regular Expression>` using the `-E` {term}`option`, making it even more powerful ({numref}`Example %s <grep_regex_example_1>`, {numref}`Example %s <grep_regex_example_2>`, {numref}`Example %s <grep_regex_example_3>`, {numref}`Example %s <grep_regex_example_4>`).

``````{admonition} Filter lines containing a sequence of 16 'A's
:name: grep_regex_example_1
:numbered: true
:class: simple myst-example
:icon: false

```{code-block} bash
grep -E "A{16}" plants.fasta
```
Will give the output:
```{code-block} bash
:class: no-copybutton
PLLQKRQEVVTKQSNPVPPSTPSSASSAAAAAAAAAAAAAAAAATAATKGKDMAPVS
```
``````

``````{admonition} Filter lines containing a sequence of 10 'A's at the start of the line
:name: grep_regex_example_2
:numbered: true
:class: simple myst-example
:icon: false

```{code-block} bash
grep -E "^A{10}" plants.fasta
```
Will give the output:
```{code-block} bash
:class: no-copybutton
AAAAAAAAAADYDGSPPPPRGKKKKDDEERSSSLPEEKDAKNGGGDEVLSAVTTEDSSAG
```
``````

```{tip}
The `-m` option limits the number of matching lines.
```

``````{admonition} Filter lines containing a pattern showing only the first occurence
:name: grep_regex_example_3
:numbered: true
:class: simple myst-example
:icon: false

```{code-block} bash
grep -m 1 -E "^[^>].*[BJOUXZ]" plants.fasta
```
Will give the output:
```{code-block} bash
:class: no-copybutton
ILNSPDRACNLAKQAFDEAISELDSLGEESYKDSTLIMQLLXDNLTLWTSDTNEDGGDEI
```
``````

``````{admonition} Filter lines containing a character 59 times showing only the first occurence
:name: grep_regex_example_4
:numbered: true
:class: simple myst-example
:icon: false

```{code-block} bash
grep -E –m 1 "(.)\1{59}" plants.fasta 
```
Will give the output:
```{code-block} bash
:class: no-copybutton
XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
```
``````

You can use {numref}`redirection <Redirection>` (`>`) to redirect the filtered lines to a file ({numref}`Example %s <grep_redirect_example>`)

``````{admonition} Redirect grep stdout
:name: grep_redirect_example
:numbered: true
:class: simple myst-example
:icon: false

```{code-block} bash
grep sp plants.fasta > out.txt
```
``````

### wc
`wc` counts lines or characters in a text ({numref}`Example %s <wc_no_options_example>`).
``````{admonition} wc default usage
:name: wc_no_options_example
:numbered: true
:class: simple myst-example
:icon: false

```{code-block} bash
wc plants.fasta
```
Will give the output:
```{code-block} bash
:class: no-copybutton
  250177   565372 15617658 plants.fasta
```
The output is the amount of **lines**, **words**, and **byte counts** for each file.
``````

To only count the amount of lines in a file, you can use the `-l` {term}`option` ({numref}`Example %s <wc_lines_example_1>`, {numref}`Example %s <wc_lines_example_2>`). 

``````{admonition} Count lines in a file 1
:name: wc_lines_example_1
:numbered: true
:class: simple myst-example
:icon: false

```{code-block} bash
wc –l plants.fasta
```
Will give the output:
```{code-block} bash
:class: no-copybutton
250177 plants.fasta
```
``````

``````{admonition} Count lines in a file 2
:name: wc_lines_example_2
:numbered: true
:class: simple myst-example
:icon: false
`out.txt` was created in {numref}`Example %s <grep_redirect_example>`, and contains all the header lines of the `plants.fasta` file that contain 'sp'.
```{code-block} bash
wc –l out.txt
```
Will give the output:
```{code-block} bash
:class: no-copybutton
33851 out.txt
```
``````


### cut
With `cut` you can extract parts of lines in a file. It prints the selected parts of lines from a file or standard input to standard output. To specify what you want to select, you can use one of the {term}`options <option>`:
- `-b` for bytes, select only these bytes
- `-c` for characters, select only these characters ({numref}`Example %s <cut_c_example>`)
- `-f` for fields, select only these fields/columns ({numref}`Example %s <cut_f_example>`). 

It uses 1-based counting.

``````{admonition} Extract the first 9 characters of crane_data.csv
:name: cut_c_example
:numbered: true
:class: simple myst-example
:icon: false

```{code-block} bash
cut -c 1-9 crane_data.csv
```
The first 3 lines of the output will be:
```{code-block} bash
:class: no-copybutton
event-id,
250386109
250386110
```
``````

``````{admonition} Extract the first field of crane_data.csv
:name: cut_f_example
:numbered: true
:class: simple myst-example
:icon: false
`-d` sets field/column delimiter. The default is TAB.
```{code-block} bash
cut -d, -f1 crane_data.csv
```
The first 3 lines of the output will be:
```{code-block} bash
:class: no-copybutton
event-id
250386109
250386110
```
``````


### sort

### tr

### awk

### sed





## Pipelines

## Practical

## Glossary
```{glossary}
shell
: Outermost layer of the operating system, acting as an intermediate between the user and the operating system.
```