---
title: Basic Linux Commands
label: basic_linux_commands_page
abbreviations:
    BLAST: Basic Local Alignment Search Tool
    RAM: Random Access Memory
    GUI: Graphical User Interface
bibliography:
    basic_linux_commands.bib
---

```{important} Learning outcomes
After completing this section you should be able to:
- navigate and manipulate the Linux file system using core directory and file management utilities (cd, ls, mkdir, cp, mv, rm)
```

## Introduction
When you connect to a Linux system, you enter an environment with its own structure, conventions, and language. In this section, you will learn how to navigate the file system, inspect the available computing resources, see who else is using the system, and organize your files and directories. Becoming comfortable with the command line is an essential first step towards using a compute server efficiently and confidently.

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 1.3.2 Directory Structure
```

## Structure of a Linux Command
The general structure of Linux commands can be written as:

```{code-block} bash
:class: no-copybutton
command [-option(s) [value]] [argument(s)]
```

An {term}`argument` is a value passed to a command, often specifying the input. An {term}`option` modifies the default behaviour of the command. They start with a hyphen/dash (`-`). {term}`Options <option>` can have values. These are written after the {term}`option`. 

Some commands can run without any {term}`option` or {term}`argument` , others require at least one of the two. 

## Searching for Help
Part of mastering the command line {term}`shell` is knowing how to search for help. Most commands/tools/programs have a help page that is printed to screen when running either:
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

where you replace `<tool>` with the relevant tool/program/command.

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 1.4.2 How to Get Help in Unix
```

## Basic Linux Commands
When working on a server, there is no graphical user interface (GUI). Instead, there is a {term}`command-line interface`, which means you will type in commands, and often assess the text-based output printed to screen. That also means that there is no GUI {term}`file system` ([](#file-system)), where you can see where you are, and what files are available for you to manipulate (such as File Explorer for Windows *#! mac version?*). Luckily, Linux comes with utilities that help to navigate the Linux {term}`file system`: `pwd`, `ls`, and `cd`. Additionally, there are utilities that allow you to create, copy, move, and remove files and directories: `mkdir`, `cp`, `mv`, and `rm`, respectively. 

When navigating and managing the {term}`file system`, you will use either {term}`absolute paths <absolute path>` or {term}`relative paths <relative path>` to indicate where you want to go or where you want to manage files/directories. An {term}`absolute path` points to a fixed position in the directory tree, like `/usr/bin`. A {term}`relative path` is the path from your current location in the directory tree to the designated location. A {term}`relative path` does not start with `/`.

*#! maybe fig with directory tree that I am using in the next examples?*

### pwd
You are always somewhere in the {term}`file system`. To **p**rint the path to your current **w**orking **d**irectory you can use `pwd` ([](#example_pwd)).

(example_pwd)=
``````{prf:example} Print path to current working directory
```{code-block} bash
pwd
```
Will give the output:
```{code-block} bash
:class: no-copybutton
/home/user001
```
``````

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 1.4.3 Navigating the Directory System
```

### cd
You can also move around within the {term}`file system`. To **c**hange **d**irectory, you can use `cd` with as argument your (already existing) directory of choice ([](#example_cd)).

(example_cd)=
``````{prf:example} Change to exercises directory
```{code-block} bash
cd exercises
```
```{code-block} bash
pwd
```
Will give the output:
```{code-block} bash
:class: no-copybutton
/home/user001/exercises
```
``````

Additionally, you can change directory with `cd` using shortcuts ([](#cd_shortcuts), [](#example_cd_shortcuts)).

```{list-table} cd shortcuts for navigation
:header-rows: 1
:name: cd_shortcuts
* - Shortcut
  - Action
* - `cd ..`
  - Move one directory up
* - `cd /`
  - Move to the root directory
* - `cd ~`
  - Move to your home directory
```

(example_cd_shortcuts)=
``````{prf:example} Change back to home from exercises directory
```{code-block} bash
pwd
```
Will give the output:
```{code-block} bash
:class: no-copybutton
/home/user001/exercises
```
Go back home with:
```{code-block} bash
cd ..
```
or:
```{code-block} bash
cd ~
```
Current directory:
```{code-block} bash
pwd
```
Will give the output:
```{code-block} bash
:class: no-copybutton
/home/user001
```
``````

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 1.4.3 Navigating the Directory System
```

### ls
Without GUI to see what files and subdirectories are present in your current directory or a directory of interest, you can use `ls`. It **l**i**s**ts all the files and subdirectories. It can be used without an {term}`argument` ([](#example_ls_no_arg)) or with the path to the directory of interest ([](#example_ls_dir)).

(example_ls_no_arg)=
``````{prf:example} List all files and subdirectories in your current directory
```{code-block} bash
ls
```
Will give the output:
```{code-block} bash
:class: no-copybutton
exercises
```
``````

(example_ls_dir)=
``````{prf:example} List all files and subdirectories in a directory
```{code-block} bash
ls exercises/
```
Will give the output:
```{code-block} bash
:class: no-copybutton
week1
```
``````

The usage of `ls` can be altered by using {term}`options <option>` ([](#ls_options)). 

```{list-table} Some useful ls options
:header-rows: 1
:name: ls_options
* - Option
  - Behaviour
* - `-a`
  - List **a** files and directories, including hidden ones
* - `-l`
  - Use a **l**ong listing format, providing additional details about the files and directories
```

When using `ls -l`, you can also supply it with a file as {term}`argument`, to see the file's details. 

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 1.4.3 Navigating the Directory System
```

### cp
With `cp` you can **c**o**p**y a file or directory. It requires two arguments:
```{code-block} bash
:class: no-copybutton
cp [OPTION] SOURCE DESTINATION
```
Where `SOURCE` is the file or directory you want to copy and `DESTINATION` is the location to which you want to copy. When you want to copy a directory you need to add {term}`option` `-r` for **r**ecursive. Then, the directory and all its contents (including subdirectories and their contents) will be copied to the destination. You can use the `.` to specify that you want to copy to your current location ([](#example_copy_dir)). 

(example_copy_dir)=
``````{prf:example} Copy day directory to home directory
Current directory:
```{code-block} bash
pwd
```
Will give the output:
```{code-block} bash
:class: no-copybutton
/home/user001
```
Copy `day2` to current directory (`home`)
```{code-block} bash
cp -r exercises/week1/day2 .
```
Let's see if it worked:
```{code-block} bash
ls
```
Will give the output:
```{code-block} bash
:class: no-copybutton
exercises
day2
```
``````

When copying, you can also rename the file or directory in the process, by giving the `DESTINATION` a different name ([](#example_copy_dir_rename)).

(example_copy_dir_rename)=
``````{prf:example} Copy day2 directory to exercises directory and rename to w1d2
Current directory:
```{code-block} bash
pwd
```
Will give the output:
```{code-block} bash
:class: no-copybutton
/home/user001
```
Suppose we don't want a nested structure for our exercises of `weekX/dayY`, where `X` is the week number and `Y` is the day number. Instead, we want all our exercises in the `exercises` directory as `wXdY`. We can do that using `cp`:

```{code-block} bash
cp -r exercises/week1/day2 exercises/w1d2
```
Let's see if it worked:
```{code-block} bash
ls exercises/
```
Will give the output:
```{code-block} bash
:class: no-copybutton
w1d2
week1
```
``````

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 1.5.1 Handling Directories and Files
```

### mv
With `mv`, you can **m**o**v**e a file or directory. Similarly to [`cp`](#cp), you need the `SOURCE` and `DESTINATION` to supply of the file/directory you want to move as arguments:
```{code-block} bash
:class: no-copybutton
mv [OPTION] SOURCE DESTINATION
```

In contrast to [`cp`](#cp), `mv` will automatically copy all the contents of a directory to the new destination, without the need of adding an {term}`option` ([](#example_mv_dir)).

(example_mv_dir)=
``````{prf:example} Move w1d2 directory to home
Current directory:
```{code-block} bash
pwd
```
Will give the output:
```{code-block} bash
:class: no-copybutton
/home/user001
```
Suppose we don't want to use the `exercises` directory at all, but want to have all our exercises in our `home` directory. In general, this is not recommended, because it will get unorganized quickly. But for this example's sake:

```{code-block} bash
mv exercises/w1d2/ .
```
Let's see if it worked:
```{code-block} bash
ls 
```
Will give the output:
```{code-block} bash
:class: no-copybutton
day2
exercises
w1d2
```
```{code-block} bash
ls exercises/
```
Will give the output:
```{code-block} bash
:class: no-copybutton
week1
```
``````

We can also rename a file or directory using `mv`. This can be done in the process of moving by supplying the new name as the `DESTINATION`. It can also be done by moving "in-place", thereby renaming the file/directory but not actually moving to a new destination ([](#example_mv_rename)).

(example_mv_rename)=
``````{prf:example} Rename a directory by moving in place
Current directory:
```{code-block} bash
pwd
```
Will give the output:
```{code-block} bash
:class: no-copybutton
/home/user001
```
Suppose we want to rename our `w1d2` directory to a longer format of `week1day2`, we can do that using `mv`:
```{code-block} bash
mv w1d2/ week1day2
```
Let's see if it worked:
```{code-block} bash
ls 
```
Will give the output:
```{code-block} bash
:class: no-copybutton
day2
exercises
week1day2
```
``````

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 1.5.1 Handling Directories and Files
```

### rm
To **r**e**m**ove a file or directory we can use `rm`. The usage can be written as:
```{code-block} bash
:class: no-copybutton
rm [OPTION] FILE
```
Where `FILE` is a file or directory. With the `-r` {term}`option` (for **r**ecursive), you can delete a directory with its contents ([](#example_rm)). 

```{caution} Removing a file is irreversible
**Removing a file on a Linux {term}`file system` is irreversible, without an undo option.** There is no trash bin!

To ensure that the path to the file or directory you want to remove is correct, you can first specify it with `ls`. Then, you can see if you are only hitting your suspected target for removal, before accidentally removing unwanted files/directories. If the path is correct, you can change the `ls` to `rm` for files and `rm -r` for directories and execute. 
```

(example_rm)=
``````{prf:example} Clean up our home directory
Current directory:
```{code-block} bash
pwd
```
Will give the output:
```{code-block} bash
:class: no-copybutton
/home/user001
```

Let's get organised again and clean up our home directory. First, we are going to remove the `day2` directory. Check whether the path is targeting only the directory using `ls -d` (`-d` for listing **d**irectories themselves, not their contents):

```{code-block} bash
ls -d day2/
```
Will give the output:
```{code-block} bash
:class: no-copybutton
day2/
```
Now we know for sure that this is our only target, so let's remove it from home:
```{code-block} bash
rm -r day2/
```
Let's see if it worked:
```{code-block} bash
ls 
```
Will give the output:
```{code-block} bash
:class: no-copybutton
exercises
week1day2
```

Again for `week1day2`:
```{code-block} bash
ls -d week1day2/
```
Will give the output:
```{code-block} bash
:class: no-copybutton
week1day2/
```
Now we know for sure that this is our only target, so let's remove it from home:
```{code-block} bash
rm -r week1day2/
```
Let's see if it worked:
```{code-block} bash
ls 
```
Will give the output:
```{code-block} bash
:class: no-copybutton
exercises
```
We are all organised again 😄.
``````

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 1.5.1 Handling Directories and Files
```

### mkdir


```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 1.5.1 Handling Directories and Files
```

### file


```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 1.5.2 Viewing and Processing Text Files
```

### less


```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 1.5.2 Viewing and Processing Text Files
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

`zcat` works similarly to `cat` except that it uncompresses files to standard output (often the screen). 

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 1.5.2 Viewing and Processing Text Files
```

### wc

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 1.5.2 Viewing and Processing Text Files
```

### head

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 1.5.2 Viewing and Processing Text Files
```

### tail

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 1.5.2 Viewing and Processing Text Files
```

## Exercises

### Directories and Files
On a Linux server you are always inside a directory, starting out in your home directory.

``````{exercise} What is your current directory?
To see your current directory, use the `pwd` command:
```{code-block} bash
pwd
```
``````

``````{exercise} What is in your current directory?
Use the `ls` command to see the files and directories in your current directory.

```{code-block} bash
ls
```

Like most commands, `ls` also has a number of {term}`option`s to alter its behavior. Add
the `-a` {term}`option`:
```{code-block} bash
ls -a
```

**What do you think the `-a` {term}`option` does?**

Check your assumption in the manual for `ls`:
```{code-block} bash
man ls
```
``````

```{tip}
Use the {kbd}`↑` (up-arrow) to scroll through your command-line history.
```

You can think of the directory structure in Linux as a tree with a root and a lot of
branches extending from this root ({numref}`file_system_structure`). 

``````{exercise} List all the files in root
To list the files in the root of the system you can simply use: 
```{code-block} bash
ls /
```
``````

So, the `/home/user001` directory is two levels away from the root.

``````{exercise} Move to a different directory
To move to a different directory, you can use the `cd` command, for **c**hange **d**irectory. Move to the directory `/bin` using:
```{code-block} bash
cd /bin
```
Use `ls` to see the files, most are programs that you can run. 

```{code-block} bash
ls
```

Also, the program that handles all your commands, the {term}`shell`, is located here: `/bin/bash`
``````

*#! Insert python sidenote here?*

``````{exercise} Listing everything that matches a pattern *#! idk*
Another location for useful programs is `/usr/bin`. To only list the programs in `/usr/bin` for which the filename starts with 'bla', run: 
```{code-block} bash
ls /usr/bin/bla*
```
In the list of files, you should see the program `blastp` that we will use at the end of this practical.

To find programs that contain 'seq' in their name, try:
```{code-block} bash
ls /usr/bin/*seq*
```
To find programs that start with a 'q' or a 'z', try: 

```{code-block} bash
ls /usr/bin/[qz]*
```
``````


``````{exercise} Absolute and relative paths
Compare what you get with the following commands (in this order):

```{code-block} bash
cd /usr
```

```{code-block} bash
cd bin
```

```{code-block} bash
pwd
```

```{code-block} bash
cd /bin
```

```{code-block} bash
pwd
```

```{code-block} bash
cd bin
```

The last `cd` gave an error, because there is no `/bin/bin` directory.

In {term}`relative path`s you can use `..` to move up one directory and `.` for the current
directory:

```{code-block} bash
cd /home
```
**#! change to your username?**
```{code-block} bash
cd ./user001 
```

```{code-block} bash
cd ../../usr/bin
```
``````

``````{exercise} Go back to home
Go back to your home directory using `cd` without any {term}`option`s or attributes (your home directory is the default): *#! explain attribute?*
```{code-block} bash
cd
```
Or with `cd ~` (the tilde is shorthand for your home directory):
```{code-block} bash
cd ~
```
``````

``````{exercise} Creating a new directory
Create a new directory called `exercises` using the command `mkdir`. Inside that directory, create a directory called `week1`, and inside that directory create a directory called `day1_2`. 
```{code-block} bash
mkdir exercises
```
Move to the `exercises` directory with the command you've just learned
```{code-block} bash
mkdir week1
```
Move to the `week1` directory and make the `day1_2` directory with the commands you've just learned.

Alternatively, you can create all three directories in one command using the `-p` {term}`option`.
```{code-block} bash
mkdir -p exercises/week1/day1_2
```
``````

``````{exercise} Working with text: DNA sequence of human chromosome 22
To explore working with text in a {term}`command-line interface`, we will first download the sequence of human chromosome 22 from the ENSEMBL website. 

Make sure you are in the `exercises/week1/day1_2` directory.

Downloading from a website usually requires a web browser. There is a command-line browser:
```{code-block} bash
lynx www.ensembl.org
```
This is not very user friendly. Fortunately, there is a command called `wget` that allows you to download a file from a website: (the URL is too long for one line)
```{code-block} bash
wget https://ftp.ensembl.org/pub/release-114/fasta/homo_sapiens/dna/Homo_sapiens.GRCh38.dna.chromosome.22.fa.gz
```

**What is the size of the file in {term}`byte`s?**

```{code-block} bash
ls -l
```

The length in nucleotides of human chromosome 22 is 50,818,468. Knowing that and the size of the file, you can determine the ratio of {term}`byte`s per nucleotide. Now you could use a calculator, but for now let's do a preview to the next part of the course and use Python to do the calculation. 

Python is a programming language that is very popular for all kinds of analyses. It is available on [[SERVER_NAME]] as the
command-line program `python3`, run it like this: (replace `file_size` with the number you found with `ls -l`)

```{code-block} bash
:class: no-copybutton
user001@[[SERVER_NAME]]:~/exercises/week1/day1_2$ python3
user001@[[SERVER_NAME]]:/usr/local/bin$ python3
Python 3.13.6 (main, Aug 7 2025, 18:15:40) [GCC 11.4.0] on linux
Type "help", "copyright", "credits" or "license" for more
information.
>>> file_size / 50818468
```

**What is the ratio of {term}`byte`s per nucleotide?**

Exit Python using {kbd}`Ctrl`+{kbd}`d`.

Before continuing with the downloaded chromosome 22 sequence, examine the type of the downloaded file type using the command `file`:

```{code-block} bash
file Homo_sapiens.GRCh38.dna.chromosome.22.fa.gz
```

This should tell you that the file is compressed (to save space), the filename extension `.gz` also indicates that. 

A compressed file cannot be read directly, you first should uncompress/unzip it using `gunzip`:
```{code-block} bash
gunzip Homo_sapiens.GRCh38.dna.chromosome.22.fa.gz
```

Again, check the size of the now uncompressed file in {term}`byte`s using Python.

For most text files on a Linux system, one character takes up exactly one {term}`byte`.

**Now what is the ratio of {term}`byte`s per nucleotide?**
``````

Reading text files on a Linux system can be done with a number of programs, from the very simply `cat` and `more`, to more versatile text editors like `nano` and `vim`. Especially `vim` is quite powerful, but also very challenging to use.

``````{exercise} Accounting for all bytes in the file: DNA sequence of human chromosome 22
To view the uncompressed file, we will use the program `less`, which deceptively is actually more advanced than the program `more`:

```{code-block} bash
less Homo_sapiens.GRCh38.dna.chromosome.22.fa
```

The text file starts with a description line, followed by many lines with the actual sequence. This follows the so-called [FASTA format](wiki:fasta_format) for sequence files (hence the `.fa` filename extension)

Looking at the nucleotides in the first lines of the sequence, you may notice that these are not informative, the same goes for the last part of the sequence (jump to the end of the file with the {kbd}`Shift`+{kbd}`g` combination and back to the top with just the {kbd}`g`). Apparently, the telomeric ends of the chromosome are not very well characterized.

Let's try to account for all {term}`byte`s in the FASTA file. The bulk of the file consists of nucleotides, but these do not add up to the number of {term}`byte`s in the file, even if you add the 56 characters of the first line. 

**What is the difference?**

**What is taking up these remaining {term}`byte`s?** As a clue, let's count the lines of the file.

First exit `less` by pressing {kbd}`q` and then use the `wc` program like this:
```{code-block} bash
wc -l Homo_sapiens.GRCh38.dna.chromosome.22.fa
```
**Do you recognize the number?**

How does `less` know when to break to the next line? That information is stored in the text file, in the form of a hidden character, which can be visualized like this (for the first 200 characters of the file):
```{code-block} bash
od -c -N 200 Homo_sapiens.GRCh38.dna.chromosome.22.fa
```
The `\n` is called the **newline** character, which takes up one {term}`byte` per line.

With these newline characters we should have accounted for all {term}`byte`s in the file.

Now we are finished with the chromosome 22 file, you can remove it to save space on our home drive:
```{code-block} bash
rm Homo_sapiens.GRCh38.dna.chromosome.22.fa
```
``````

```{caution} Removing a file is irreversible
Removing a file on a Linux {term}`file system` is irreversible, without an undo option.
*#! I would add that it is better to first check whether the path you are selecting to remove only contains the files you want to remove by running `ls` first before running `rm`*
```

Now, let's do some biology on the command-line. One of the most used programs in bioinformatics is called BLAST.

With BLAST you can search for a protein or nucleotide sequence in a database of known sequences. It does not only find exact matches, but also similar sequences. This allows you to look for homologous sequences. These are
sequences that originate from the same ancestral gene, for instance the human hemoglobin beta and delta proteins have a very similar amino acid sequence.

BLAST is extensively covered in the [Introduction to Bioinformatics](https://wur-bioinformatics.github.io/introduction-to-bioinformatics/chapter2/#blast) course. Most researchers will use BLAST via the [NCBI website](https://blast.ncbi.nlm.nih.gov/Blast.cgi), which works fine for a few sequences. If you have a lot of protein or nucleotide sequences that you want to search, using BLAST from the command-line is more efficient. 


``````{exercise} command-line BLAST a protein sequence
Using the command `cp`, copy the file `proteinX.fasta` from the `/mnt/local_scratch/BIF21806` directory to your `day1_2` directory.

Inspect the file with `less` to see that it contains one protein sequence in FASTA format. 

We will search for it in the human protein sequences from the SwissProt database. SwissProt contains high-quality manually annotated and reviewed protein sequences [@uniprot_2022].

Copy the file `sp_human_single_line.fasta` from `/mnt/local_scratch/BIF21806` to your `day1_2` directory.

Create a BLAST database of the `sp_human_single_line.fasta` file using: 

```{code-block} bash
makeblastdb -in sp_human_single_line.fasta -out sp_human
```

This should create a BLAST database called sp_human, but something is still missing. Look in the {term}`option`s for `makeblastdb` to solve the problem:
```{code-block} bash
makeblastdb -help
```

When you've found the right {term}`option`, make the BLAST database with the corrected command. The database uses an {term}`index` to find sequences faster.

The BLAST command-line programs come is several [flavors](https://wur-bioinformatics.github.io/introduction-to-bioinformatics/chapter2/#blast-types), depending on whether you want to search protein or nucleotide sequences, in a protein or a nucleotide database. In this case we want to search a protein database for a protein sequence, which requires `blastp`.

First, to get an overview of the {term}`option`s, run:

```{code-block} bash
blastp -help
```

**What is the {term}`option` to provide the query FASTA file?** \
**What is the {term}`option` to provide the name of the database?**\
**What is the {term}`option` to specify the name of the {term}`output` file?**

Run `blastp` with the appropriate parameters for the three {term}`option`s mentioned above, call the {term}`output` file: `proteinX.blast`

Use the `less` command to view the {term}`output` file. 

**What is proteinX?**

Now run `blastp` again , but change the {term}`output` file name to `proteinX.html` and add the {term}`option` `-html`.

The resulting file can be viewed in a web browser, so let's copy it over to your own computer. The easiest way to do that is to use the `scp` command on your computer:

```{code-block} bash
scp [[SERVER_NAME]]:~/exercises/week1/day1_2/proteinX.html .
```

Locate the file on your computer and open it with a web browser.

Congratulations, you completed your first command-line bioinformatics analysis! 🎉
``````

