---
title: Advanced Linux Commands and Pipes
label: adv_linux_commands_pipes
abbreviations:
    BLAST: Basic Local Alignment Search Tool
bibliography:
    advanced_linux_commands_and_pipes.bib
---

```{important} Learning outcomes
After completing this section you should be able to:
- explain the concepts standard input (stdin), standard output (stdout), and standard error (stderr).
- construct command pipelines to transform and filter data across multiple Linux tools.
```

## Introduction
Most Linux commands are designed to perform one specific task, such as displaying a file, counting lines, sorting values, or filtering text. By combining several commands in a pipeline, the output of one command can be passed directly to the next. This makes it possible to perform surprisingly powerful analyses on very large datasets without having to load the data into a spreadsheet or write a complete program. In this section, you will learn how to combine commands efficiently and build transparent, reusable data-processing workflows.

(input-outputstreams)=
## Input/Output streams
### Standard input, standard output, standard error
When running a program on the Linux command-line, you will always deal with the Input/Output streams: standard input ({term}`stdin`), standard output ({term}`stdout`), and standard error ({term}`stderr`) ({numref}`io_streams`). 

```{figure} img/input-output_streams.png
:label: io_streams

Input/Output streams of Linux command-line
```

The {term}`stdin` of a program is often your keyboard or a file. This is the input that you want the program to act upon. The {term}`stdout` is by default the terminal screen, but some programs include an {term}`option` to redirect the output to a file. This is the output created by the program. The {term}`stderr` is by default the terminal screen. This is the stream where error messages are directed towards. [@ibm_aix_2025; @nazeer_standard_2024; @geeksforgeeks_shell_nodate]

### Redirection
If a tool does not have the {term}`option` to save the {term}`standard output <stdout>` to a file, you can use the `>` symbol, to redirect the contents of {term}`standard output <stdout>` to a file ([](#redirect_example)).

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

(Advanced_Linux_Commands)=
## Advanced Linux Commands
Now that you have mastered the basics of using the {term}`shell` in [](#basic_linux_commands_page), let's explore some more advanced command-line tools. The tools explored here are by no means an exhaustive list of Linux tools, but these tools are very useful for handling biological data (files). 

``````{tip} Remember how to search for help
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

(wget_section)=
### wget
`wget` is a tool that can retrieve files from a URL:
```{code-block} bash
:class: no-copybutton
wget [OPTIONS] [URL]
```
where  `URL` is the URL or link to the file to download ([](#wget_example)).

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

(grep_section)=
### grep
`grep` is a tool that filters text for a given term. It searches for a pattern in a file or {term}`standard input <stdin>`: 
```{code-block} bash
:class: no-copybutton
grep [OPTION] PATTERNS [FILE]
```
where `PATTERNS` is/are the pattern(s) to search for in each `FILE` ([](#grep_basic_example)).

```{tip}
When using the `--color` {term}`option`, the part of the line that is matched will be colored in the {term}`stdout`.
```


(grep_basic_example)=
``````{prf:example} Filter lines that contain 'sp'
```{code-block} bash
grep --color sp plants.fasta
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
grep --color -E "A{16}" plants.fasta
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
grep --color -E "^A{10}" plants.fasta
```
Will give the output:
```{code-block} bash
:class: no-copybutton
AAAAAAAAAADYDGSPPPPRGKKKKDDEERSSSLPEEKDAKNGGGDEVLSAVTTEDSSAG
```
``````

```{tip}
The `-m` {term}`option` limits the number of matching lines.
```

(grep_regex_example_3)=
``````{prf:example} Filter lines containing a pattern showing only the first occurence
```{code-block} bash
grep --color -m 1 -E "^[^>].*[BJOUXZ]" plants.fasta
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
grep --color -E –m 1 "(.)\1{59}" plants.fasta 
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

(cut_section)=
### cut
With `cut` you can extract parts of lines in a file:
```{code-block} bash
:class: no-copybutton
cut OPTION [FILE]
```
where the `OPTION` specifies on what you want to select in each `FILE` (a file or {term}`standard input <stdin>`). The selected parts of lines are printed to {term}`standard output <stdout>`. 

To specify what you want to select, you can use one of the {term}`options <option>`:
- `-b` for bytes, select only these bytes
- `-c` for characters, select only these characters ([](#cut_c_example))
- `-f` for fields, select only these fields/columns ([](#cut_f_example)). 

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

(sort_section)=
### sort
With `sort` you can write the sorted content of a `FILE` (or {term}`standard input <stdin>`) to {term}`standard output <stdout>`:
```{code-block} bash
:class: no-copybutton
sort [OPTION] [FILE]
```

You can sort based on a field/column when using both the `-k` and `-t` {term}`options <option>` ([](#sort_k_example)). The {term}`option` `-k` specifies the start and stop position of the field/column, and the {term}`option` `-t` specifies the delimiter. With {term}`option` `-r`, you can sort in reverse order ([](#sort_r_example))

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

(tr_section)=
### tr
With `tr`, you can translate characters from {term}`standard input <stdin>` and write to {term}`standard output <stdout>`:
```{code-block} bash
:class: no-copybutton
tr [OPTION] STRING1 [STRING2]
```
where `STRING1` is the string/character you want to translate into the `STRING2` string/character ([](#tr_dna_example), [](#tr_case_example)).

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
Because `tr` only takes input from {term}`standard input <stdin>`, we used `echo` to direct the strings in [](#tr_dna_example) and [](#tr_case_example) to {term}`stdin` and the pipe (`|`) to redirect {term}`stdin` to `tr`. This will be explained more extensively in {numref}`Pipelines`.
```

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 1.6.3 Substituting Characters Using `tr`
```

(awk_section)=
### awk
`awk` is a text processor or manipulator [@turner_intro_2021]. It works by executing a "program" on a `FILE`, often by searching for strings and then performing an action when it finds those strings:
```{code-block} bash
:class: no-copybutton
awk [OPTIONS] 'PROGRAM' FILE
```
where the awk `PROGRAM` can be described as: `'pattern {action}'`. The `pattern` describes what lines `awk` should act upon and the `action` describes what should be done when the lines are found. The full `awk` program is wrapped in single quotes (`''`). 

`awk` uses the `-F` {term}`option` to specify the field/column delimiter ([](#awk_F_example)). In `awk`, the `$0` means the whole line. 

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
For simple searches [`grep`](#grep_section) might be more suitable. However, when you want to find something and print something else, `awk` can be very powerful.
```

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 1.9.3 Miscellaneous Commands
```

(sed_section)=
### sed
`sed` is short for **s**tream **ed**itor. It is used for filtering and transforming text. It takes text from either a file or {term}`standard input <stdin>` and returns the processed text to {term}`standard output <stdout>`:
```{code-block} bash
:class: no-copybutton
sed [OPTION] 'SCRIPT' [FILE]
```
where the `'SCRIPT'` contains a Find&Replace statement as: `'s/search_pattern/replacement/'`.

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

(uniq_section)=
### uniq

```{code-block} bash
:class: no-copybutton
uniq [OPTION]... [INPUT [OUTPUT]]
```
the uniq tool can only recognize that lines are the same if they are consecutive lines. That
is why you usually need to do a sort before doing a uniq


(tar_section)=
### tar

```{code-block} bash
:class: no-copybutton
tar [OPTION...] [FILE]...
```

(pipelines)=
## Pipelines
Now that we have seen some more advanced Linux commands, let's explore how we can combine them by using pipelines. A pipeline is a string of commands for which the {term}`stdout` of the previous command is redirected towards the {term}`stdin` of the following command ({ref}`input-outputstreams`). This is done with the pipe symbol (`|`). 

(wc_lines_example_2)=
``````{prf:example} Count lines in a file 2
Only lines in `plants.fasta` that contain 'sp'.
```{code-block} bash
wc –l out.txt
```
Will give the output:
```{code-block} bash
:class: no-copybutton
33851 out.txt
```
``````

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

For the next example ([](#pipe_cut_sort_example)), let's combine a [`cut`](#cut_section) command with a [`sort`](#sort_section) command.

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
:::{dropdown} Solution
`wc -l` counts newline characters
:::


Finally, let's combine [`grep`](#grep_section) and [`sed`](#sed_section) in a pipeline ([](#pipe_grep_sed_example)).

(pipe_grep_sed_example)=
``````{prf:example} Extract all protein identifiers in plants.fasta
If we are only interested in the header lines of a FASTA file we can filter on '>' with [`grep`](#grep_section). 

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

Then we can extract just the protein identifiers with [`sed`](#sed_section) as was done in [](#sed_fasta_example>`.

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


## Exercises
In the following exercises, you will:
- build up complex pipelines from small, less complex 'Lego' blocks;
- make bigger 'Lego' blocks and extend on those. 

For each of the exercises you will get commands which serve as building blocks of the pipeline. Connect them in the right order using the pipe (`|`) symbol as discussed in [](#pipelines). 


``````{tip}
As you add parts of your pipeline, check what actually comes out after each addition. 

To not "flood" your screen by intermediary output, you can always add a temporary [`head`](#head_section) command. For example, if you only want the first five lines to be printed to {term}`stdout`, add: 
```{code-block} bash
| head -5
```
``````

```{note} 
The exact syntax of [`awk`](#awk_section) is not that important, but try to see what it does. 
```


### Working with Column-Separated Data
For these exercises you will work with a smaller sample of the `crane.csv` dataset containing only the first and last one hundred lines of the original: `first_and_last_100_lines_crane_data.csv`. You will practice with extracting specific columns from tab-delimited files and selecting lines based on matches in only one column. You will also practice with two other very useful tools that can sort columns and extract and count unique content of columns and text.

```{tip}
Many of the shell tools that work easily with column data, recognize TAB (or any whitespace) as default delimiter. 

Converting from comma- to tab-delimited text therefore saves having to specify the delimiter for every tool separately. There can be vast differences in what {term}`option` each tool used to specify the delimiter.
```

*#! add how to get the file*

``````{exercise} Extract columns from data
Extract the first and third column of the data
```{tip}
The first command should read the data file.
```
```{code-block} bash
sed 's/,/\t/g' | sed 's/\t /, /g'
```
```{code-block} bash
cat first_and_last_100_lines_crane_data.csv
```
```{code-block} bash
cut -f1,3
```
The [`cut`](#cut_section) command means: take the first and third column; no delimiter specified so assumes TAB
``````


``````{exercise} Split a column into two columns & print columns in alternate order
Extract first and third columns, create separate columns for date and time, and print first date, then time, and then the observation id.
```{code-block} bash
cut -f1,3
```
```{code-block} bash
awk '{print $2"\t"$3"\t"$1}
```
```{code-block} bash
cat first_and_last_100_lines_crane_data.csv
```
```{code-block} bash
sed 's/,/\t/g' | sed 's/\t /, /g'
```
```{code-block} bash
sed 's/ /\t/'
```
The [`awk`](#awk_section) command prints second, third, and first column, in that order. [`awk`](#awk_section) will use any whitespace as column delimiter by default. To be explicit, in this example the space between the data and time in column 2 is explicitly converted to TAB. Always work as explicit as possible unless you know exactly how your tools are behaving.
``````


(exc_selecting_lines_1)=
``````{exercise} Select only those lines containing a specific date 1
Extract first and third columns, create separate columns for date and time, and select only those lines pertaining November 2015. 
```{code-block} bash
cut -f1,3
```
```{code-block} bash
awk '$2~/2015-11/'
```
```{code-block} bash
cat first_and_last_100_lines_crane_data.csv
```
```{code-block} bash
sed 's/ /\t/'
```
```{code-block} bash
sed 's/,/\t/g' | sed 's/\t /, /g'
```
The [`awk`](#awk_section) command means: line selected if second column contains '2015-11'
``````


``````{exercise} Select only those lines containing a specific date 2
Now do the same, but include latitude, longitude, and animal ID (the latter found in column 14). 
```{code-block} bash
awk '$2~/2015-11/'
```
```{code-block} bash
cat first_and_last_100_lines_crane_data.csv
```
```{code-block} bash
sed 's/,/\t/g' | sed 's/\t /, /g'
```
```{code-block} bash
cut -f1,3,4,5,14
```
```{code-block} bash
sed 's/ /\t/'
```
**What is the only difference with [](#exc_selecting_lines_1)?**
``````


(exc_count_observations_date)=
``````{exercise} Count number of observations on a specific date 1 
**Count the number of observations per day in November 2015.**
```{code-block} bash
cut -f2
```
```{code-block} bash
cut -f1,3
```
```{code-block} bash
cat first_and_last_100_lines_crane_data.csv
```
```{code-block} bash
sort
```
```{code-block} bash
sed 's/,/\t/g' | sed 's/\t /, /g'
```
```{code-block} bash
sed 's/ /\t/'
```
```{code-block} bash
awk '$2~/2015-11/'
```
```{code-block} bash
uniq -c
```
We need the [`sort`](#sort_section) command because [`uniq`](#uniq_section) expects a sorted list. \
The [`uniq`](#uniq_section) command means: show unique records, and counts occurrences because of `-c` {term}`option`.
``````

Now download the entire Common Crane tracking data set, using the command [`wget`](#wget_section):

```{code-block} bash
wget http://www.bioinformatics.nl/courses/BIF-21806/Examples/Common_Crane_tracking/GPS_telemetry_of_Common_Cranes_Sweden.csv.gz
```

The file is zipped. You can unzip it, but remember that these datasets could easily be five times larger ([](#io_compression)). Fortunately, there is a flavor of `cat` that can directly read zipped files: `zcat`.


``````{exercise} Count observations of complete file
```{code-block} bash
wc -l
```
```{code-block} bash
zcat GPS_telemetry_of_Common_Cranes_Sweden.csv.gz
```
**How many observations does the complete file contain?**
``````


``````{exercise} Count number of observations on a specific date for a specific animal
Similar to [](#exc_count_observations_date), extract date and time (put in different, tab-delimited columns), latitude, longitude,
and animal ID, for animal with ID 9480 for the month of November for every year. 
```{code-block} bash
cut -f1,3,4,5,14
```
```{code-block} bash
wc -l
```
```{code-block} bash
zcat GPS_telemetry_of_Common_Cranes_Sweden.csv.gz
```
```{code-block} bash
awk '$1~/-11-/'
```
```{code-block} bash
sed 's/,/\t/g' | sed 's/\t /, /g'
```
```{code-block} bash
sed 's/ /\t/'
```
```{code-block} bash
awk '$5~/9480'
```
**Count the number of occurrences.**
``````


``````{exercise} Count number of observations per animal
```{code-block} bash
cut -f14
```
```{code-block} bash
zcat GPS_telemetry_of_Common_Cranes_Sweden.csv.gz
```
```{code-block} bash
sort
```
```{code-block} bash
sed 's/,/\t/g' | sed 's/\t /, /g'
```
```{code-block} bash
uniq -c
```
**How many observations are there for each animal?**
``````



``````{exercise} (optional) Selecting lines on numerical columns using > and <
**How many observations are there for the vicinity of Wageningen (square between 51° and 52° lat, 5° and 6° lon)?**

Omit `wc -l` to answer the following two questions:\
**How many animals were involved?** \
**And when?**
```{code-block} bash
cut -f3,4,5,14
```
```{code-block} bash
sed 's/ /\t/'
```
```{code-block} bash
awk '$3>5&&$3<6&&$4>51&&$4<52
```
```{code-block} bash
zcat GPS_telemetry_of_Common_Cranes_Sweden.csv.gz
```
```{code-block} bash
sed 's/,/\t/g' | sed 's/\t /, /g'
```
```{code-block} bash
wc -l
```

When values in a column can be interpreted numerically, you can use [`awk`](#awk_section) to select based on comparison (smaller, larger, equal). You can include logic 'AND' by separating comparisons by double '`&&`' (logic 'OR' can be implemented by double pipe '`||`')
``````

### Finding the Longest Word -- Revisited
Remember that problem you solved yesterday? The one where you found the longest word in Charles Darwin's "On the Origin of Species"? Did you get '18' as the answer? 

Here we will do the same exercise, but now we will extract ONLY the words that are 18 (word) characters long.

The file is available on [[SERVER_NAME]] at: `/mnt/local_scratch/BIF21806/TOoS.txt` *#! still correct?*

(exc_18_char_words)=
``````{exercise} Select words that are 18 characters long
Find and extract the longest words using:
```{code-block} bash
grep -E '^\w{18}$'
```
```{code-block} bash
sed "s/[^{A-Za-z'}]/\n/g"
```
```{code-block} bash
cat TooS.txt
```
Note that the [`sed`](#sed_section) expressions are now double-quoted because of searching for single-quote in the expression itself. You can use either single or double quotes, but they have to close correctly.
``````

``````{exercise} Select words that are 17 characters long
Which 17-character words are there? Use the building blocks from [](#exc_18_char_words).
``````


### Bonus: Analyze the Word Use of Shakespeare's Collected Works
In this exercise (inspired by @Robbins2005-ry), you will make a shell one-liner to analyze the word use of the collected works of William Shakespeare. This may well be the most studied literary work written in modern history. Many thousands of students and scholars have labored for days, weeks, nay, months on end to understand the literary genius of The Bard. And now, you can easily extract some vital statistics on the collected works in milliseconds!

Let's first get a copy:
```{code-block} bash
wget http://www.bioinformatics.nl/courses/BIF-21806/Examples/Shakespeare/shakespeare.tar.gz
```

Mind that this is actually a collection of files (an archive), first "tarred" into a single file, then zipped. This is common practice in Linux systems to compress entire directories and their content.

To upack, do:
```{code-block} bash
tar -xzvf shakespeare.tar.gz
```
Then go to the directory `Shakespeare`:
```{code-block} bash
cd Shakespeare
```

(exc_shakespeare_words_1)=
``````{exercise} Print the 30 most frequent words 1
Process the text by putting each word on its own line (split on non-word characters), remove all empty lines, then sort alphabetically so that you can make the words unique and get their counts, and then sort the result by going from most frequent to least frequent word. Finally display the 30 most frequent words.

You should start with:
```{code-block} bash
cat *.txt
```
**Why?**

Combine the remaining building blocks into a pipeline:
```{code-block} bash
grep -v '^$'
```
```{code-block} bash
uniq -c
```
```{code-block} bash
sed "s/[^{A-Za-z'}]/\n/g"
```
```{code-block} bash
sort
```
```{code-block} bash
head -30
```
```{code-block} bash
sort -k1,1nr
```
```{code-block} bash
grep -v -E '[A-Z]{2,}'
```

The [`grep`](#grep_section) command `grep -v '^$'` filters out empty lines.\
The [`sort`](#sort_section) command `sort -k1,1nr` sorts numerically on the first column, in descending order.\
The [`grep`](#grep_section) command `grep -v -E '[A-Z]{2,}'` filters out words with two or more consecutive capital letters.

**What are the 30 most frequent words?**
``````

The result of [](#exc_shakespeare_words_1) is not perfect. For instance, the top 30 contains both 'the' as well as 'The'. Another problem is the use of single-quotes, not just inside a word, but also as quotations. Let's add some extra building blocks in [](#exc_shakespeare_words_2) to resolve this.


(exc_shakespeare_words_2)=
``````{exercise} Print the 30 most frequent words 2
Add these three building blocks, in the correct position, in your pipeline of [](#exc_shakespeare_words_1):

```{code-block} bash
tr 'A-Z' 'a-z'
```
```{code-block} bash
sed "s/^'//"
```
```{code-block} bash
sed "s/'$//"
```

```{tip}
They will not be useful at the end of your previous pipeline.
```
**Is there a difference in the result?**
``````
