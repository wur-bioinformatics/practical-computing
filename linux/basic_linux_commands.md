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
When you connect to a Linux system, you enter an environment with its own structure, conventions, and language. In this section, you will learn how to navigate the file system and organize your files and directories. Becoming comfortable with the command line is an essential first step towards using a compute server efficiently and confidently.

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
When working on a server, there is no graphical user interface (GUI). Instead, there is a {term}`command-line interface`, which means you will type in commands, and often assess the text-based output printed to screen. That also means that there is no GUI {term}`file system` ([](#file_system)), where you can see where you are, and what files are available for you to manipulate (such as File Explorer for Windows and Finder for macOS). Luckily, Linux comes with utilities that help to navigate the Linux {term}`file system`: `pwd`, `ls`, and `cd`. Additionally, there are utilities that allow you to create, copy, move, and remove files and directories: `mkdir`, `cp`, `mv`, and `rm`, respectively. 

When navigating and managing the {term}`file system`, you will use either {term}`absolute paths <absolute path>` or {term}`relative paths <relative path>` to indicate where you want to go or where you want to manage files/directories. An {term}`absolute path` points to a fixed position in the directory tree, like `/usr/bin`. A {term}`relative path` is the path from your current location in the directory tree to the designated location. A {term}`relative path` does not start with `/`.

*#! maybe fig with directory tree that I am using in the next examples?*

(pwd_section)=
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

(cd_section)=
### cd
You can also move around within the {term}`file system`. To **c**hange **d**irectory, you can use `cd`:
```{code-block} bash
:class: no-copybutton
cd [OPTION] DIRECTORY
```
Where `DIRECTORY` is the {term}`argument` specifying your (already existing) directory of choice ([](#example_cd)).

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

(ls_section)=
### ls
Without GUI to see what files and subdirectories are present in your current directory or a directory of interest, you can use `ls`. It **l**i**s**ts all the files and subdirectories.
```{code-block} bash
:class: no-copybutton
ls [OPTION] FILE
```
Where `FILE` is the file/directory of which you want to list the information ([](#example_ls_dir)), the default (without an {term}`argument`) is the current directory ([](#example_ls_no_arg)). 

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

The usage of `ls` can be altered by using {term}`options <option>` ([](#ls_options)). 

```{list-table} Some useful ls options
:header-rows: 1
:name: ls_options
* - Option
  - Behaviour
* - `-a`
  - List **a**ll files and directories, including hidden ones
* - `-l`
  - Use a **l**ong listing format, providing additional details about the files and directories
* - `-d`
  - List **d**irectories themselves, not their contents
```

When using `ls -l`, you can also supply it with a file as {term}`argument`, to see the file's details. 

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 1.4.3 Navigating the Directory System
```

(cp_section)=
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

(mv_section)=
### mv
With `mv`, you can **m**o**v**e a file or directory. Similarly to [`cp`](#cp_section), you need the `SOURCE` and `DESTINATION` to supply of the file/directory you want to move as arguments:
```{code-block} bash
:class: no-copybutton
mv [OPTION] SOURCE DESTINATION
```

In contrast to [`cp`](#cp_section), `mv` will automatically copy all the contents of a directory to the new destination, without the need of adding an {term}`option` ([](#example_mv_dir)).

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

(rm_section)=
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

(mkdir_section)=
### mkdir
If we want to **m**a**k**e a new **dir**ectory we can use `mkdir`:
```{code-block} bash
:class: no-copybutton
mkdir [OPTION] DIRECTORY
```
Where `DIRECTORY` is the path to the directory we want to create ([](#example_mkdir)). A useful {term}`option` is `-p`, which allows you to make parent directories to the final directory if they don't exist yet ([](#example_mkdir_nested)).

(example_mkdir)=
``````{prf:example} Make new directory for exercises of week 1 day 3
Current directory:
```{code-block} bash
pwd
```
Will give the output:
```{code-block} bash
:class: no-copybutton
/home/user001
```

Suppose we want to prepare for tomorrow and already make the `day3` directory:
```{code-block} bash
mkdir exercises/week1/day3
```

Let's see if it worked:
```{code-block} bash
ls exercises/week1/
```
Will give the output:
```{code-block} bash
:class: no-copybutton
day2
day3
```
``````

(example_mkdir_nested)=
``````{prf:example} Make new directories for exercises of week 2 day 1
Current directory:
```{code-block} bash
pwd
```
Will give the output:
```{code-block} bash
:class: no-copybutton
/home/user001
```

Suppose we want to prepare for next week and already make the `week2/day1` directories in one go:
```{code-block} bash
mkdir -p exercises/week2/day1
```

Let's see if it worked:
```{code-block} bash
ls exercises/
```
Will give the output:
```{code-block} bash
:class: no-copybutton
week1
week2
```

```{code-block} bash
ls exercises/week2/
```
Will give the output:
```{code-block} bash
:class: no-copybutton
day1
```
``````

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 1.5.1 Handling Directories and Files
```

(file_section)=
### file
You can determine the type of a **file** using `file`:
```{code-block} bash
:class: no-copybutton
file [OPTION] FILE
```
Where `FILE` is the file of interest ([](#example_file_cranes)).

(example_file_cranes)=
``````{prf:example} File type of cranes.csv
```{code-block} bash
file cranes.csv
```
Will give the output:
```{code-block} bash
:class: no-copybutton
cranes.csv: CSV ASCII text
```
``````

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 1.5.2 Viewing and Processing Text Files
```

(less_section)=
### less
With `less` you can progressively look at a file, meaning it does not open the whole file in a text editer, but loads only the bits that are displayed on screen. This makes it especially useful when you want to inspect large files. 

To navigate the `less` environment:
- {kbd}`Ctrl`+ {kbd}`F` for moving one screen **f**orward
- {kbd}`Ctrl`+ {kbd}`B` for moving one screen **b**ackward
- {kbd}`h` for the manual/**h**elp
- {kbd}`q` for exiting/**q**uitting the environment

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 1.5.2 Viewing and Processing Text Files
```

(cat_section)=
### cat
With `cat` you can con**cat**enate and print files to screen (standard output):
```{code-block} bash
:class: no-copybutton
cat [OPTION] [FILE]
```
Where `FILE` is either one or multiple files. When only one file is provided, the contents are printed to screen ([](#cat_example)). When multiple files are provided, they are concatenated and then printed to screen.

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

(wc_section)=
### wc
To see the line, **w**ord, and byte (**c**haracter) count of a file, we can use `wc`:
```{code-block} bash
:class: no-copybutton
wc [OPTION] [FILE]
```
Where `FILE` is the file of interest ([](#wc_no_options_example)). You can also only print the **l**ine ([](#wc_lines_example_1)), only the **w**ord or only the byte/**c**haracter count by using {term}`options <option>` `-l`, `-w`, `-c`, respectively.

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


```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 1.5.2 Viewing and Processing Text Files
```

(head_section)=
### head
To inspect the **head** of a file, or the first couple of lines, you can use `head`:
```{code-block} bash
:class: no-copybutton
head [OPTION] [FILE]
```
Where `FILE` is the file of interest. When multiple files are supplied, the first lines (default is 10) is printed for each file. With {term}`option` `-n` you can specify the amount of lines you want to print ([](#example_head_n)).

(example_head_n)=
``````{prf:example} Print the first 3 lines of cranes.csv
```{code-block} bash
head -3 cranes.csv
```
Will give the output:
```{code-block} bash
:class: no-copybutton
event-id,visible,timestamp,location-long,location-lat,argos:altitude,gps:hdop,ground-speed,heading,tag-tech-spec,tag-voltage,sensor-type,individual-taxon-canonical-name,tag-local-identifier,individual-local-identifier,study-name
250386109,true,2013-07-12 04:10:14.000,13.3524,57.33415,,,,,"",,"gps","Grus grus","8621","8621","GPS telemetry of Common Cranes, Sweden"
250386110,true,2013-07-12 04:24:05.000,13.352072,57.333359,210.0,1.7,0.257,0.0,"3",4.18,"gps","Grus grus","8621","8621","GPS telemetry of Common Cranes, Sweden"
```
``````

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 1.5.2 Viewing and Processing Text Files
```

(tail_section)=
### tail
You can print the **tail**, or last couple of lines, of a file using `tail`:
```{code-block} bash
:class: no-copybutton
tail [OPTION] [FILE]
```
Where `FILE` is the file of interest. When multiple files are supplied, the first lines (default is 10) is printed for each file. With {term}`option` `-n` you can specify the amount of lines you want to print ([](#example_tail_n)).


(example_tail_n)=
``````{prf:example} Print the last 3 lines of cranes.csv
```{code-block} bash
tail -3 cranes.csv
```
Will give the output:
```{code-block} bash
:class: no-copybutton
1119958190,true,2015-12-10 13:44:00.000,9.635656,53.272591,28.0,2.8,0.0,,"3",3.66,"gps","Grus grus","7558","7558","GPS telemetry of Common Cranes, Sweden"
1119958189,true,2015-12-10 14:14:00.000,9.638817,53.296185,34.0,1.4,2.0,,"3",3.65,"gps","Grus grus","7558","7558","GPS telemetry of Common Cranes, Sweden"
1119958188,true,2015-12-10 14:45:00.000,9.63322,53.296234,35.0,3.8,0.0,,"3",3.65,"gps","Grus grus","7558","7558","GPS telemetry of Common Cranes, Sweden"
```
``````

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 1.5.2 Viewing and Processing Text Files
```

## Exercises

### Finding your Way Around the Server
On a Linux server you are always inside a directory, starting out in your home directory.

``````{exercise} What is your current directory?
To see your current directory, use the [`pwd`](#pwd_section) command:
```{code-block} bash
pwd
```
``````

``````{exercise} What is in your current directory?
Use the [`ls`](#ls_section) command to see the files and directories in your current directory.

```{code-block} bash
ls
```

Like most commands, [`ls`](#ls_section) also has a number of {term}`options <option>` to alter its behavior. Add
the `-a` {term}`option`:
```{code-block} bash
ls -a
```

**What do you think the `-a` {term}`option` does?**

Check your assumption in the manual for [`ls`](#ls_section):
```{code-block} bash
man ls
```
``````

```{tip}
Use the {kbd}`↑` (up-arrow) to scroll through your command-line history.
```

You can think of the directory structure in Linux as a tree with a root and a lot of branches extending from this root ({numref}`file_system_structure`). 

``````{exercise} List all the files in root
To list the files in the root of the system you can simply use: 
```{code-block} bash
ls /
```

So, the `/home/user001` directory is two levels away from the root.
``````


``````{exercise} Move to a different directory
To move to a different directory, you can use the [`cd`](#cd_section) command, for **c**hange **d**irectory. Move to the directory `/bin` using:
```{code-block} bash
cd /bin
```
Use [`ls`](#ls_section) to see the files, most are programs that you can run. 

```{code-block} bash
ls
```

Also, the program that handles all your commands, the {term}`shell`, is located here: `/bin/bash`
``````

``````{exercise} Using wildcards in the commandline
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

The last [`cd`](#cd_section) gave an error, because there is no `/bin/bin` directory.

In {term}`relative paths <relative path>` you can use `..` to move up one directory and `.` for the current
directory:

```{code-block} bash
cd /home
```
Change `user001` to your username:
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

### Getting Organized

``````{exercise} Creating a new directory
Create a new directory called `exercises` using the command [`mkdir`](#mkdir_section). Inside that directory, create a directory called `week1`, and inside that directory create a directory called `day2`. 
```{code-block} bash
mkdir exercises
```
Move to the `exercises` directory with the command you've just learned.
```{code-block} bash
mkdir week1
```
Move to the `week1` directory and make the `day2` directory with the commands you've just learned.

Alternatively, you can create all three directories in one command using the `-p` {term}`option`.
```{code-block} bash
mkdir -p exercises/week1/day2
```
``````

### Working with Text
``````{exercise} DNA sequence of human chromosome 22
To explore working with text in a {term}`command-line interface`, we will first download the sequence of human chromosome 22 from the ENSEMBL website. 

Make sure you are in the `exercises/week1/day2` directory.

Downloading from a website usually requires a web browser. There is a command-line browser:
```{code-block} bash
lynx www.ensembl.org
```
This is not very user friendly. Fortunately, there is a command called `wget` that allows you to download a file from a website: (the URL is too long for one line)
```{code-block} bash
wget https://ftp.ensembl.org/pub/release-114/fasta/homo_sapiens/dna/Homo_sapiens.GRCh38.dna.chromosome.22.fa.gz
```

**What is the size of the file in {term}`bytes <byte>`?**

```{code-block} bash
ls -l
```

The length in nucleotides of human chromosome 22 is 50,818,468. Knowing that and the size of the file, you can determine the ratio of {term}`bytes <byte>` per nucleotide. You could use a calculator, but for now let's do a preview to the next part of the course and use Python to do the calculation. 

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

**What is the ratio of {term}`bytes <byte>` per nucleotide?**

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

Again, check the size of the now uncompressed file in {term}`bytes <byte>` using Python.

For most text files on a Linux system, one character takes up exactly one {term}`byte`.

**Now what is the ratio of {term}`bytes <byte>` per nucleotide?**
``````

Reading text files on a Linux system can be done with a number of programs, from the very simple [`cat`](#cat_section) and `more`, to more versatile text editors like `nano` and `vim`. Especially `vim` is quite powerful, but also very challenging to use.

``````{exercise} Accounting for all bytes in the file: DNA sequence of human chromosome 22
To view the uncompressed file, we will use the program [`less`](#less_section), which deceptively is actually more advanced than the program `more`:

```{code-block} bash
less Homo_sapiens.GRCh38.dna.chromosome.22.fa
```

The text file starts with a description line, followed by many lines with the actual sequence. This follows the so-called [FASTA format](wiki:fasta_format) for sequence files (hence the `.fa` filename extension)

Looking at the nucleotides in the first lines of the sequence, you may notice that these are not informative, the same goes for the last part of the sequence (jump to the end of the file with the {kbd}`Shift`+{kbd}`g` combination and back to the top with just the {kbd}`g`). Apparently, the telomeric ends of the chromosome are not very well characterized.

Let's try to account for all {term}`bytes <byte>` in the FASTA file. The bulk of the file consists of nucleotides, but these do not add up to the number of {term}`bytes <byte>` in the file, even if you add the 56 characters of the first line. 

**What is the difference?**

**What is taking up these remaining {term}`bytes <byte>`?** As a clue, let's count the lines of the file.

First exit [`less`](#less_section) by pressing {kbd}`q` and then use the `wc` program like this:
```{code-block} bash
wc -l Homo_sapiens.GRCh38.dna.chromosome.22.fa
```
**Do you recognize the number?**

How does [`less`](#less_section) know when to break to the next line? That information is stored in the text file, in the form of a hidden character, which can be visualized like this (for the first 200 characters of the file):
```{code-block} bash
od -c -N 200 Homo_sapiens.GRCh38.dna.chromosome.22.fa
```
The `\n` is called the **newline** character, which takes up one {term}`byte` per line.

With these newline characters we should have accounted for all {term}`bytes <byte>` in the file.

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 1.9.2 Line Terminators
```

Now we are finished with the chromosome 22 file, you can [remove](#rm_section) it to save space on our home drive:
```{code-block} bash
rm Homo_sapiens.GRCh38.dna.chromosome.22.fa
```
```{caution} Removing a file is irreversible
**Removing a file on a Linux {term}`file system` is irreversible, without an undo option.** There is no trash bin!
```
``````

### Using BLAST from the command line
Now, let's do some biology on the command-line. One of the most used programs in bioinformatics is called BLAST.

With BLAST you can search for a protein or nucleotide sequence in a database of known sequences. It does not only find exact matches, but also similar sequences. This allows you to look for homologous sequences. These are sequences that originate from the same ancestral gene, for instance the human hemoglobin beta and delta proteins have a very similar amino acid sequence.

BLAST is extensively covered in the [Introduction to Bioinformatics](https://wur-bioinformatics.github.io/introduction-to-bioinformatics/chapter2/#blast) course. Most researchers will use BLAST via the [NCBI website](https://blast.ncbi.nlm.nih.gov/Blast.cgi), which works fine for a few sequences. If you have a lot of protein or nucleotide sequences that you want to search, using BLAST from the command-line is more efficient. 


``````{exercise} command-line BLAST a protein sequence
Using the command [`cp`](#cp_section), copy the file `proteinX.fasta` from the `/mnt/local_scratch/BIF21806` directory to your `day2` directory.

Inspect the file with [`less`](#less_section) to see that it contains one protein sequence in FASTA format. 

We will search for it in the human protein sequences from the SwissProt database. SwissProt contains high-quality manually annotated and reviewed protein sequences [@uniprot_2022].

Copy the file `sp_human_single_line.fasta` from `/mnt/local_scratch/BIF21806` to your `day2` directory.

Create a BLAST database of the `sp_human_single_line.fasta` file using: 

```{code-block} bash
makeblastdb -in sp_human_single_line.fasta -out sp_human
```

This should create a BLAST database called sp_human, but something is still missing. Look in the {term}`options <option>` for `makeblastdb` to solve the problem:
```{code-block} bash
makeblastdb -help
```

When you've found the right {term}`option`, make the BLAST database with the corrected command. The database uses an {term}`index` to find sequences faster.

The BLAST command-line programs come in several [flavors](https://wur-bioinformatics.github.io/introduction-to-bioinformatics/chapter2/#blast-types), depending on whether you want to search protein or nucleotide sequences, in a protein or a nucleotide database. In this case we want to search a protein database for a protein sequence, which requires `blastp`.

First, to get an overview of the {term}`options <option>`, run:

```{code-block} bash
blastp -help
```

**What is the {term}`option` to provide the query FASTA file?** \
**What is the {term}`option` to provide the name of the database?**\
**What is the {term}`option` to specify the name of the {term}`output` file?**

Run `blastp` with the appropriate parameters for the three {term}`options <option>` mentioned above, call the {term}`output` file: `proteinX.blast`

Use the [`less`](#less_section) command to view the {term}`output` file. 

**What is proteinX?**

Now run `blastp` again , but change the {term}`output` file name to `proteinX.html` and add the {term}`option` `-html`.

The resulting file can be viewed in a web browser, so let's copy it over to your own computer. The easiest way to do that is to use the `scp` command on your computer:

```{code-block} bash
scp [[SERVER_NAME]]:~/exercises/week1/day1_2/proteinX.html .
```

Locate the file on your computer and open it with a web browser.

Congratulations, you completed your first command-line bioinformatics analysis! 🎉
``````

