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

(input-outputstreams)=
## Input/Output streams
### Standard input, standard output, standard error
When running a program on the Linux command-line, you will always deal with the Input/Output streams: standard input (stdin), standard output (stdout), and standard error (stderr) ({numref}`io_streams`). 

```{figure} img/input-output_streams.png
:label: io_streams

Input/Output streams of Linux command-line
```

The stdin of a program is often your keyboard or a file. This is the input that you want the program to act upon. The stdout is by default the terminal screen, but some programs include an {term}`option` to redirect the output to a file. This is the output created by the program. The stderr is by default the terminal screen. This is the stream where error messages are directed towards. [@ibm_aix_2025; @nazeer_standard_2024; @geeksforgeeks_shell_nodate]

### Redirection
If a tool does not have the {term}`option` to redirect to a file, you can use the `>` symbol ([](#redirect_example)).

(redirect_example)=
``````{prf:example} Redirecting output to a file
```{code-block} bash
:class: no-copybutton
program > filename
```
``````

```{caution} Be careful when using >
Using the redirect symbol `>` will overwrite any contents of the file given, which cannot be undone. 
```

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 1.6.1 Redirection and Pipes
```

(Advanced_Unix_Commands)=
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
`wget` is a tool that can retrieve files from a URL ([](#wget_example)).

(wget_example)=
``````{prf:example} Download a FASTA file
```{code-block} bash
wget http://www.bioinformatics.nl/plants.fasta
```
``````

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 1.9.3 Miscellaneous Commands
```

### cat
`cat` is a tool that prints the contents of a file (or standard input) to standard output (often the screen) ([](#cat_example)).

(cat_example)=
``````{prf:example} Print contents of a FASTA file to screen
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

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 1.5.2 Viewing and Processing Text Files
```

### grep
`grep` is a tool that filters text for a given term. It searches for a pattern in a file or standard input ([](#grep_basic_example)).

(grep_basic_example)=
``````{prf:example} Filter lines that contain 'sp'
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

`grep` can be used with {term}`Regular Expressions <Regular Expression>` using the `-E` {term}`option`, making it even more powerful ([](#grep_regex_example_1), [](#grep_regex_example_2), [](#grep_regex_example_3), [](#grep_regex_example_4)).

(grep_regex_example_1)=
``````{prf:example} Filter lines containing a sequence of 16 'A's
```{code-block} bash
grep -E "A{16}" plants.fasta
```
Will give the output:
```{code-block} bash
:class: no-copybutton
PLLQKRQEVVTKQSNPVPPSTPSSASSAAAAAAAAAAAAAAAAATAATKGKDMAPVS
```
``````

(grep_regex_example_2)=
``````{prf:example} Filter lines containing a sequence of 10 'A's at the start of the line
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

(grep_regex_example_3)=
``````{prf:example} Filter lines containing a pattern showing only the first occurence
```{code-block} bash
grep -m 1 -E "^[^>].*[BJOUXZ]" plants.fasta
```
Will give the output:
```{code-block} bash
:class: no-copybutton
ILNSPDRACNLAKQAFDEAISELDSLGEESYKDSTLIMQLLXDNLTLWTSDTNEDGGDEI
```
``````

(grep_regex_example_4)=
``````{prf:example} Filter lines containing a character 59 times showing only the first occurence
```{code-block} bash
grep -E –m 1 "(.)\1{59}" plants.fasta 
```
Will give the output:
```{code-block} bash
:class: no-copybutton
XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
```
``````

You can use {numref}`redirection <Redirection>` (`>`) to redirect the filtered lines to a file ([](#grep_redirect_example)).

(grep_redirect_example)=
``````{prf:example} Redirect grep stdout
```{code-block} bash
grep sp plants.fasta > out.txt
```
``````

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 1.6.5 Selecting Lines Using `grep`
```

### wc
`wc` counts lines or characters in a text ([](#wc_no_options_example)).

(wc_no_options_example)=
``````{prf:example} wc default usage
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

To only count the amount of lines in a file, you can use the `-l` {term}`option` ([](#wc_lines_example_1), [](#wc_lines_example_2)). 

(wc_lines_example_1)=
``````{prf:example} Count lines in a file 1
```{code-block} bash
wc –l plants.fasta
```
Will give the output:
```{code-block} bash
:class: no-copybutton
250177 plants.fasta
```
``````
(wc_lines_example_2)=
``````{prf:example} Count lines in a file 2
contain 'sp'.
```{code-block} bash
wc –l out.txt
```
Will give the output:
```{code-block} bash
:class: no-copybutton
33851 out.txt
```
``````

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 1.5.2 Viewing and Processing Text Files
```

### cut
With `cut` you can extract parts of lines in a file. It prints the selected parts of lines from a file or standard input to standard output. To specify what you want to select, you can use one of the {term}`options <option>`:
- `-b` for bytes, select only these bytes
- `-c` for characters, select only these characters ([](#cut_c_example))
- `-f` for fields, select only these fields/columns ([](#cut_f_example)). 

It uses 1-based counting.

(cut_c_example)=
``````{prf:example} Extract the first 9 characters of crane_data.csv

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

(cut_f_example)=
``````{prf:example} Extract the first field of crane_data.csv
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

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 1.6.2 Selecting Columns Using `cut`
```

### sort
With `sort` you can write the sorted content of a file (or standard input) to standard output. You can sort based on a field/column when using both the `-k` and `-t` {term}`options <option>` ([](#sort_k_example)). The {term}`option` `-k` specifies the start and stop position of the field/column, and the {term}`option` `-t` specifies the delimiter. With {term}`option` `-r`, you can sort in reverse order ([](#sort_r_example))

(sort_k_example)=
``````{prf:example} Sort crane_data.csv on the third column
```{code-block} bash
sort -t, -k3,3 crane_data.csv 
```
The first 3 lines of the output will be:
```{code-block} bash
:class: no-copybutton
250386109,true,2013-07-12 04:10:14.000,13.3524,57.33415,,,,,"",,"gps","Grus grus","8621","8621","GPS telemetry of Common Cranes, Sweden"
250386110,true,2013-07-12 04:24:05.000,13.352072,57.333359,210.0,1.7,0.257,0.0,"3",4.18,"gps","Grus grus","8621","8621","GPS telemetry of Common Cranes, Sweden"
250386111,true,2013-07-12 04:38:51.000,13.352212,57.333355,203.0,8.3,0.257,0.0,"3",4.18,"gps","Grus grus","8621","8621","GPS telemetry of Common Cranes, Sweden"
```
``````

(sort_r_example)=
``````{prf:example} Sort crane_data.csv on the third column in reverse order
```{code-block} bash
sort -t, -k3,3 -r crane_data.csv 
```
The first 3 lines of the output will be:
```{code-block} bash
:class: no-copybutton
event-id,visible,timestamp,location-long,location-lat,argos:altitude,gps:hdop,ground-speed,heading,tag-tech-spec,tag-voltage,sensor-type,individual-taxon-canonical-name,tag-local-identifier,individual-local-identifier,study-name
1119958188,true,2015-12-10 14:45:00.000,9.63322,53.296234,35.0,3.8,0.0,,"3",3.65,"gps","Grus grus","7558","7558","GPS telemetry of Common Cranes, Sweden"
1119958189,true,2015-12-10 14:14:00.000,9.638817,53.296185,34.0,1.4,2.0,,"3",3.65,"gps","Grus grus","7558","7558","GPS telemetry of Common Cranes, Sweden"
```
*#! this is different in the slides, there the header line is not shown*
``````

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 1.5.2 Viewing and Processing Text Files
```

### tr
With `tr`, you can translate characters from standard input and write to standard output ([](#tr_dna_example), [](#tr_case_example)).

(tr_dna_example)=
``````{prf:example} Translate DNA string into RNA string
```{code-block} bash
echo ATGCATTAG | tr 'T' 'U'
```
Will give the output:
```{code-block} bash
:class: no-copybutton
AUGCAUUAG
```
``````

(tr_case_example)=
``````{prf:example} Make a string lowercase
```{code-block} bash
echo Hello World | tr 'A-Z' 'a-z'
```

```{code-block} bash
:class: no-copybutton
hello world
```
``````

```{note}
Because `tr` only takes input from standard input, we used `echo` to direct the strings in [](#tr_dna_example) and [](#tr_case_example) to stdin and the pipe (`|`) to redirect stdin to `tr`. This will be explained more extensively in {numref}`Pipelines`.
```

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 1.6.3 Substituting Characters Using `tr`
```

### awk
`awk` is a text processor or manipulator [@turner_intro_2021]. It works by searching for strings and then performing an action when it finds those strings. The usage can be described as: \
`'pattern {action}'`\
The `pattern` describes what lines `awk` should act upon and the `action` describes what should be done when the lines are found. The full `awk` program is wrapped in single quotes (`''`). 

`awk` uses the `-F` {term}`option` to specify the field/column delimiter ([](#awk_F_example)). `awk` uses 1-based counting, though the `$0` means the whole line. 

(awk_F_example)=
``````{prf:example} Select lines where the longitude is greater than 13
Here, we filter for lines that have a longitude (`$4`, field 4 is the location-long, or the longitude) greater than 13 (`> 13`).
```{code-block} bash
awk -F, '$4 > 13' crane_data.csv 
```
The first two lines of the output will be: 
```{code-block} bash
:class: no-copybutton
event-id,visible,timestamp,location-long,location-lat,argos:altitude,gps:hdop,ground-speed,heading,tag-tech-spec,tag-voltage,sensor-type,individual-taxon-canonical-name,tag-local-identifier,individual-local-identifier,study-name
250386109,true,2013-07-12 04:10:14.000,13.3524,57.33415,,,,,"",,"gps","Grus grus","8621","8621","GPS telemetry of Common Cranes, Sweden"
```
``````

We can perform a filter using `'$n~/filter/'`, where `n` is the field/column number (`0` for whole line) and `filter` is the filter that we want to apply ([](#awk_filter_example). The filter can be a {term}`Regular Expression`. 

(awk_filter_example)=
``````{prf:example} Select lines with records on 12-10
The third field holds the date and time.
```{code-block} bash
awk -F, '$3~/12-10/' crane_data.csv
```
The first line of the output will be:
```{code-block} bash
:class: no-copybutton
1119958195,true,2015-12-10 06:38:00.000,9.570068,53.259296,29.0,0.9,0.0,,"3",3.64,"gps","Grus grus","7558","7558","GPS telemetry of Common Cranes, Sweden"
```
``````

Until now we have only searched for a pattern in [](#awk_F_example) and [](#awk_filter_example). By default `awk` prints the whole line, which would be the same as the action `'{print $0}'`. Instead, we can also print parts of a line [](#awk_print_example)).

(awk_print_example)=
``````{prf:example} Print the third field
```{code-block} bash
awk -F, '{print $3}' crane_data.csv
```
The first two lines of the output will be:
```{code-block} bash
:class: no-copybutton
timestamp
2013-07-12 04:10:14.000
```
``````

Let's combine the search for a pattern and the action of printing a specific field in [](#awk_full_example).

(awk_full_example)=
``````{prf:example} Print longitude of records on 12-10
```{code-block} bash
awk -F, '$3~/12-10/ {print $4}' crane_data.csv
```
The output will be:
```{code-block} bash
:class: no-copybutton
9.570068
9.623796
9.637121
9.637557
9.636033
9.635656
9.638817
9.63322
```
``````

```{caution} When to use awk?
For simple searches {ref}`grep` might be more suitable. However, when you want to find something and print something else, `awk` can be very powerful.
```

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 1.9.3 Miscellaneous Commands
```

### sed
`sed` is short for **s**tream **ed**itor. It is used for filtering and transforming text. It takes text from either a file or standard input and returns the processed text to standard output. 

The Find&Replace structure of the command is as follows: \
`sed 's/search_pattern/replacement/' file.txt`

`sed` support the usage of {term}`Regular Expressions <Regular Expression>` in the `search_pattern` part ([](#sed_fasta_example)). 

(sed_fasta_example)=
``````{prf:example} Edit FASTA header line
```{code-block} bash
head -3 plants.fasta
```
```{code-block} bash
:class: no-copybutton
>sp|Q43495|108_SOLLC Protein 108 OS=Solanum lycopersicum PE=2 SV=1
MASVKSSSSSSSSSFISLLLLILLVIVLQSQVIECQPQQSCTASLTGLNVCAPFLVPGSP
TASTECCNAVQSINHDCMCNTMRIAAQIPAQCNLPPLSCSAN
```
Let's remove the first part of the header line by replacing it with nothing:

```{code-block} bash
sed 's/>.*|//' plants.fasta
```
The first three lines of the output will be:
```{code-block} bash
:class: no-copybutton
108_SOLLC Protein 108 OS=Solanum lycopersicum PE=2 SV=1
MASVKSSSSSSSSSFISLLLLILLVIVLQSQVIECQPQQSCTASLTGLNVCAPFLVPGSP
TASTECCNAVQSINHDCMCNTMRIAAQIPAQCNLPPLSCSAN
```
The text-file is not edited in place, but the above output is printed to screen.
``````

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 1.9.3 Miscellaneous Commands
```

## Pipelines
Now that we have seen some more advanced Unix commands, let's explore how we can combine them by using pipelines. A pipeline is a string of commands for which the stdout of the previous command is redirected towards the stdin of the following command ({ref}`input-outputstreams`). This is done with the pipe symbol (`|`). 

To illustrate, we combined the commands from [](#grep_redirect_example) and [](#wc_lines_example_2) in [](#pipeline_example). Now we don't have to create a separate text file and store it when we are only interested in the amount of entries in the FASTA file with 'sp' in the header.

(pipeline_example)=
``````{prf:example} Pipeline example
```{code-block} bash
cat plants.fasta | grep sp | wc –l
```
Will give the output:
```{code-block} bash
:class: no-copybutton
33851
```
The `plants.fasta` file is sent to `grep`, which only sends lines containing **sp** to the `wc` command, which in turn counts those lines. Thus, the output represents the amount of lines containing **sp**.
``````

The flow of {numref}`this <pipeline_example>` pipeline example is visualised in {numref}`fig_pipeline_example`.

```{figure} img/pipeline_example.png
:label: fig_pipeline_example

Data stream of example pipeline with `cat`, `grep`, and `wc`.
```

For the next example ([](#pipe_cut_sort_example)), let's combine a {ref}`cut` command with a {ref}`sort` command.

(pipe_cut_sort_example)=
``````{prf:example} Extract the third column of crane.csv and sort in reverse order
```{code-block} bash
cat crane_data.csv | cut -d, -f3 | sort -r
```
The first five lines of the output will be:
```{code-block} bash
:class: no-copybutton
timestamp
2015-12-10 14:45:00.000
2015-12-10 14:14:00.000
2015-12-10 13:44:00.000
2015-12-10 13:13:00.000
```
``````

What if removed all newline characters from a file and counted the lines ([](#tr_newline_example))?

(tr_newline_example)=
``````{prf:example} Remove all newline characters from a file and count the lines
```{code-block} bash
cat plants.fasta | tr '\n' ' ' | wc -l
```
The output will be:
```{code-block} bash
:class: no-copybutton
0
```
**Why do you think the output is `0`?** (Look at the usage of `wc -l`)
``````

Finally, let's combine {ref}`grep` and {ref}`sed` in a pipeline ([](#pipe_grep_sed_example)).

(pipe_grep_sed_example)=
``````{prf:example} Extract all protein identifiers in plants.fasta
If we are only interested in the header lines of a FASTA file we can filter on '>' with `grep`. 

```{code-block} bash
grep ">" plants.fasta
```
The first three lines of the output will be:
```{code-block} bash
:class: no-copybutton
>sp|Q43495|108_SOLLC Protein 108 OS=Solanum lycopersicum PE=2 SV=1
>sp|Q9XHP0|11S2_SESIN 11S globulin seed storage protein 2 OS=Sesamum indicum PE=2 SV=1
>sp|P19084|11S3_HELAN 11S globulin seed storage protein G3 OS=Helianthus annuus GN=HAG3 PE=3 SV=1
```

Then we can extract just the protein identifiers with `sed` as was done in [](#sed_fasta_example>`.

```{code-block} bash
grep ">" plants.fasta | sed 's/>.*|//'
```
The first three lines of the output will be:
```{code-block} bash
:class: no-copybutton
108_SOLLC Protein 108 OS=Solanum lycopersicum PE=2 SV=1
11S2_SESIN 11S globulin seed storage protein 2 OS=Sesamum indicum PE=2 SV=1
11S3_HELAN 11S globulin seed storage protein G3 OS=Helianthus annuus GN=HAG3 PE=3 SV=1
```
``````

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 1.6.1 Redirection and Pipes
```


## Practical

