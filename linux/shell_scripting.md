---
title: Shell Scripting
label: shell_scripting
bibliography:
    shell_scripting.bib
---


```{important} Learning outcomes
After completing this section you should be able to:
- explain what a shell script is and when it can be useful
- explain how the shell locates and executes scripts using executable flags (chmod +x) and the $PATH variable.
```

## Introduction
Data analysis usually involves many steps, from cleaning and preparing files to running analyses and summarizing the results. These steps can be performed manually, but doing so is time-consuming and makes it difficult to reproduce the analysis later. A shell script records the commands in a file that can be executed whenever needed. In this section, you will learn how to turn a sequence of commands into a script, add variables and basic logic, and create workflows that are easier to repeat, inspect, and share.

## Shell Scripting
Now that you have got more experience with {ref}`Advanced_Linux_Commands` and [](#section_alcap_pipelines), it is fairly easy to turn them into a script. Scripts can be written in different programming and scripting languages, such as Python, Bash, and R. Each language has its own syntax, rules, and vocabulary.

File extensions are commonly used to indicate the language in which a script is written. For example, Python scripts usually have the `.py` extension, while R scripts usually have the `.R` extension and bash shell scripts often have the `.sh` extension.

On Windows, the file extension determines which program is used to open or run a script. On Linux, the extension is mainly informative. To specify which interpreter should execute the script, you can add a *shebang* as the first line of the file.

```{margin}
The shebang (`#!`) is a combination of the sharp or hash symbol (`#`) and an exclamation mark, also known as bang (`!`).
```

The advantages of turning pipelines into scripts are that your commands are saved into a file and can be executed any time on any (relevant) file. For example, if you have multiple FASTA files on which you want to perform the same operations, you don't have to rewrite your pipeline many times, you can just execute the script with those files. Additionally, if in 6 months you want to perform that same operation on a new FASTA file, you don't have to go through your notes to find the right pipeline. Instead, you can use your written script. 

(section_basic_structure_of_a_shell_script)=
### Basic Structure of a Shell Script
A {term}`shell script` is a (text) file containing a series of commands that the {term}`shell` can interpret and execute [@geeksforgeeks_shellscripting_2026]. 

Let's build a simple {term}`shell script` that writes 'Hello World' to screen called `hello_world.sh`. 

To create or open a file we can use the `nano` command, which is a simple text editor on Linux:

```{code-block} bash
nano hello_world.sh
```


The first line of a {term}`shell script` is called the shebang line. It tells the {term}`shell` the path to the program it should use to interpret the script with. Here, that program is `bash`, so the first line of our {term}`shell script` is:
```{code-block} bash
:filename: hello_world.sh
:linenos:
:emphasize-lines: 1
#!/bin/bash
```
 
Alternatively, you can explicitly provide the interpreter when running the script, for example:
```{code-block} bash
bash hello_world.sh
```
 

Apart from the shebang line, we can write comments in our {term}`shell script` using the hashtag (`#`), these lines will not be executed:
```{code-block} bash
:filename: hello_world.sh
:linenos:
:emphasize-lines: 2
#!/bin/bash
# Script to write 'Hello World' to screen
```

Let's add the command:
```{code-block} bash
:filename: hello_world.sh
:linenos:
:emphasize-lines: 3
#!/bin/bash
# Script to write 'Hello World' to screen
echo "Hello World"
```

To close the editor and save the file, press: {kbd}`Ctrl` + {kbd}`x`, then {kbd}`Y` and press {kbd}`enter` to accept the filename.

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 1.7 Basic Scripting
```

(section_running_a_shell_script)=
### Running a Shell Script
Now that we have written a simple {term}`shell script`, we would like to run it in the same way as a Linux command:
```{code-block} bash
hello_world.sh
```
 
However, two issues must be addressed before this will work.
 
First, Linux searches for commands only in a predefined set of directories. These directories are listed in the `PATH` environment variable. To see which these are, you can print the value of `PATH`:
```{code-block} bash
printenv PATH
```
or
```{code-block} bash
echo $PATH
```


The directory containing your script is usually not included in `PATH`. Therefore, typing only the script name may result in a "command not found" error, even when the script is located in your current working directory.
 
You could add the directory to `PATH`, but the simplest solution is to specify the location of the script explicitly. When the script is in the current directory, use the {term}`relative path`:
```{code-block} bash
./hello_world.sh
```

:::{tip} Tip
The `.` represents the current directory. 
:::
 
Second, you may now receive a "permission denied" error. For security reasons, Linux does not allow every file to be executed as a command. You can view the permission flags of a file using:
```{code-block} bash
ls -l hello_world.sh
```
```{code-block} bash
:class: no-copybutton
-rw-r--r-- 1 user001 domain users 98 Jul 27 18:05 hello_world.sh
```

The first 10 characters indicate file properties/permissions:
```{code-block} bash
:class: no-copybutton
-rw-r--r--
1234567890
```
The very first character (**1**) is `-` for normal files, and for instance `d` for **d**irectories. \
Characters **2-4** show the permissions for the owner of the file (`user001`), who can **r**ead and **w**rite (`rw-`).\
Characters **5-7** show the permissions for users in the usergroup (`domain users`), who can only **r**ead (`r--`). \
Characters **8-10** show the permissions for all other users on the system, who also can only **r**ead (`r--`).

An `x` would indicate e**x**ecution permission, which nobody has for this file. To give the script executable permission, we can run the `chmod` command:
```{code-block} bash
chmod +x hello_world.sh
```
This gives everyone on the system executable permission. 


After that, you can run the script with:
```{code-block} bash
./hello_world.sh
```

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 1.6.7 Permissions
- Chapter 1.7 Basic Scripting
- Chapter 1.9.1 Setting a `PATH` in `.bash_profile`
```

### Specifying Variables
Variables are objects that store values or user input for reuse in commands [@geeksforgeeks_shellscripting_2026]. Using variables makes {term}`shell scripts <shell script>` more flexible. 

To introduce the usage of variables, let's make a new version of the `hello_world.sh` program called `greeting.sh` so the message is contained in a variable:
```{code-block} bash
:filename: greeting.sh
:linenos:
:emphasize-lines: 3,4
#!/bin/bash
# Script to write a greeting to screen
GREETING="Hello World"
echo $GREETING
```
In line **3** the variable is introduced. Note that there should be zero spaces around the '`=`' sign. By convention, variable names are written in all caps. Additionally, because variables can only contain one item, here string quotes are added because "Hello World" contains a space. \
In line **4** the variable is called by writing the dollar sign (`$`) before the variable name. 

We can also use variable calling when running a script with arguments. Instead of {term}`hard-coding<hard-code>` the greeting into the file, we can supply it on the command line as an argument, making the script more flexible:

```{code-block} bash
:filename: greeting.sh
:linenos:
:emphasize-lines: 3
#!/bin/bash
# Script to write a greeting to screen
echo $1
```
The `$1` is the first argument given to the script on the command line. The arguments are separated by spaces and stored in order of occurence.

Running the script as:
```{code-block} bash
./greeting.sh "Hello World"
```
It would store `"Hello World"` in `$1` and the script would give as output:
```{code-block} bash
:class: no-copybutton
Hello World
```
When running the script as:
```{code-block} bash
./greeting.sh "Good morning"
```
It would store `"Good morning"` in `$1` and the script would give as output:
```{code-block} bash
:class: no-copybutton
Good morning
```

To apply the concept of variables to a more biological problem, in [](#pipe_grep_sed_script_example) we turn the pipeline from [](#pipe_grep_sed_example) in [](#adv_linux_commands_pipes) into a flexible {term}`shell script`.

(pipe_grep_sed_script_example)=
``````{prf:example} Script to print all protein identifiers in a FASTA file to screen
Let's turn first the pipeline from [](#pipe_grep_sed_example) in [](#adv_linux_commands_pipes) into a shell script:

```{code-block} bash
:filename: extract_protein_ids_hardcoded.sh
#!/bin/bash
# Print all protein identifiers in plants.fasta to screen
grep ">" plants.fasta | sed 's/>.*|//'
```

We have now {term}`hard-coded<hard-code>` the filename `plants.fasta` into the script, meaning that everytime we run the script, it will print the protein identifiers of `plants.fasta`. If we would want to do the same thing but for a different file (for example `trees.fasta` containing all protein sequences of your favourite tree), we would have to make a copy of the script and alter the FASTA filename. This is of course tedious and misses the point of creating {term}`shell scripts <shell script>`. 

Instead, we can supply the script with the FASTA file as an argument and use variable calling in the script.

```{code-block} bash
:filename: extract_protein_ids.sh
#!/bin/bash
# Print all protein identifiers in a FASTA file to screen
grep ">" $1 | sed 's/>.*|//'
```

Now we can run the script with any FASTA file:
```{code-block} bash
./extract_protein_ids.sh plants.fasta
```
```{code-block} bash
./extract_protein_ids.sh trees.fasta
```
``````

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 1.7 Basic Scripting
```

(section_ss_for_loop)=
### `for` loops
A `for` loop in a {term}`shell script` allows you to execute commands or pipelines repeatedly, for a specified amount of times, or for multiple files. The basic structure of a `for` loop in a {term}`shell script` is:

```{code-block} bash
:class: no-copybutton
for i in range
do 
    action
done
```
The `range` here can be a range of numbers ([](#for_loop_number_example)) or multiple files in a directory ([](#for_loop_files_example)).

(for_loop_number_example)=
``````{prf:example} Looping over a range of numbers
Let's adapt the `hello_world.sh` program so now it prints a greeting 5 times.

```{code-block} bash
:filename: greeting_5_times.sh
#!/bin/bash
for i in {1..5}
do
    echo $1
done
```
Running the script as:
```{code-block} bash
 ./greeting_5_times.sh "Hello World"
```
Will give the output:
```{code-block} bash
:class: no-copybutton
Hello world
Hello world
Hello world
Hello world
Hello world
```
``````

(for_loop_files_example)=
``````{prf:example} Looping over files in a directory
Suppose we want to extract the protein IDs for multiple FASTA files in a directory. We can use a `for` loop and a wildcard ('`*`') as follows:

```{code-block} bash
:filename: extract_protein_ids_all_fasta_files.sh
:linenos:
:emphasize-lines: 3
#!/bin/bash
# Print all protein identifiers in all FASTA files in the current directory to screen
for file in *.fasta
    do grep ">" $file | sed 's/>.*|//'
done
```
In Line **3**, we create the variable `file` that, for each iteration in the `for` loop takes on the name of the filenames that end in `.fasta`. We use the bash wildcard `*` to represent zero or more characters.

If we run the script (after [making it executable](#section_running_a_shell_script)) in the directory that has multiple FASTA files, it would print all protein IDs from all FASTA files to screen.
```{code-block} bash
chmod +x extract_protein_ids_all_fasta_files.sh
```
```{code-block} bash
 ./extract_protein_ids_all_fasta_files.sh
```
``````

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 1.8 Simple `for` loops
```

(conditional_statements_section)=
### Conditional Statements
Conditional statements are used in scripts to let only a certain part of code be run if the condition is met. There are three conditional statements: `if`, `elif`, and `else`. We will illustrate them by altering `greeting.sh`, so the greeting is specific to the time of day.

Let's start with the basic structure of the program:

```{code-block} bash
:filename: greeting_daytime.sh
:linenos:
:emphasize-lines: 3,4,5,6
#!/bin/bash

HOUR=`date "+%H"`
NAME=`finger $USER | grep Name: | sed 's/.*Name:\s\+//'`
TIMEOFDAY="day"
echo Good $TIMEOFDAY $NAME, you look great today!
```
In line **3**, we save the hour of the day in a variable `HOUR` by using command `date` (look at the help to see what `+%H` does).\
In line **4**, we save the name of the user in a variable `NAME`.\
In line **5**, we set the `TIMEOFDAY` variable to `"day"`.\
In line **6**, we print to screen the greeting using the `TIMEOFDAY` variable and the `NAME` variable.

Running the script (after [making it executable](#section_running_a_shell_script)):
```{code-block} bash
./greeting_daytime.sh
```
Will give the output:
```{code-block} bash
:class: no-copybutton
Good day <YOUR NAME>,  you look great today!
```


An `if`-statement has the following basic structure:
```{code-block} bash
:class: no-copybutton
if [ condition ]; then
    action
fi
```


Now let's add an `if`-statement, so if it is before 12:00, we will greet with "Good morning":

```{code-block} bash
:filename: greeting_daytime.sh
:linenos:
:emphasize-lines: 6,7,8
#!/bin/bash

HOUR=`date "+%H"`
NAME=`finger $USER | grep Name: | sed 's/.*Name:\s\+//'`
TIMEOFDAY="day"
if [ $HOUR -lt 12 ]; then
        TIMEOFDAY="morning"
fi
echo Good $TIMEOFDAY $NAME, you look great today!
```

If you would run this script in the morning:
```{code-block} bash
./greeting_daytime.sh
```
It would give the output:
```{code-block} bash
:class: no-copybutton
Good morning <YOUR NAME>,  you look great today!
```

We can also add an `elif`-statement, that condition is only checked when the previous conditional statements were not met. Then the basic structure is:
```{code-block} bash
:class: no-copybutton
if [ condition ]; then
    action
elif [ condition ]; then
    action
fi
```

Let's add an `elif`-statement for when it is afternoon:

```{code-block} bash
:filename: greeting_daytime.sh
:linenos:
:emphasize-lines: 8,9
#!/bin/bash

HOUR=`date "+%H"`
NAME=`finger $USER | grep Name: | sed 's/.*Name:\s\+//'`
TIMEOFDAY="day"
if [ $HOUR -lt 12 ]; then
        TIMEOFDAY="morning"
elif [ $HOUR -lt 18 ]; then
    TIMEOFDAY="afternoon"
fi
echo Good $TIMEOFDAY $NAME, you look great today!
```

If you would run this script in the afternoon:
```{code-block} bash
./greeting_daytime.sh
```
It would give the output:
```{code-block} bash
:class: no-copybutton
Good afternoon <YOUR NAME>,  you look great today!
```

Last, we can add an `else`-statement, for when all previous conditions are not met. Here, we do not specify the condition, so in all other cases, this part of the code will be run:
```{code-block} bash
:class: no-copybutton
if [ condition ]; then
    action
elif [ condition ]; then
    action
else
    action
fi
```

For the remaining day-time, the evening, let's add the `else`-statement:
```{code-block} bash
:filename: greeting_daytime.sh
:linenos:
:emphasize-lines: 10,11
#!/bin/bash

HOUR=`date "+%H"`
NAME=`finger $USER | grep Name: | sed 's/.*Name:\s\+//'`
if [ $HOUR -lt 12 ]; then
        TIMEOFDAY="morning"
elif [ $HOUR -lt 18 ]; then
    TIMEOFDAY="afternoon"
else
    TIMEOFDAY="evening"
fi
echo Good $TIMEOFDAY $NAME, you look great today!
```
We have removed the initation of the `TIMEOFDAY` variable, because now all possible conditions are explored.


If you would run this script in the evening:
```{code-block} bash
./greeting_daytime.sh
```
It would give the output:
```{code-block} bash
:class: no-copybutton
Good evening <YOUR NAME>,  you look great today!
```


## Exercises
In the following exercises, we will create {term}`shell scripts <shell script>`. Easiest is to use the Linux text editor `nano`, as described [before](#section_basic_structure_of_a_shell_script).

### Organizing Text in a Script
``````{exercise} Turn the code to extract the words from The Origin of Species into a script
We will now turn the code you used to extract the words from The Origin of Species into a proper script. 

Use the Linux text editor `nano` to create a script (text file) called `wordlength.sh` using:

```{code-block} bash
nano wordlength.sh
```

Fill it with the following lines:
```{code-block} bash
:filename: wordlength.sh
:linenos:
:emphasize-lines: 2,3
#!/bin/bash
LEN=$1
TEXTFILE=$2
cat $TEXTFILE | sed "s/[^{A-Za-z'}]/\n/g" | grep -E "^\w{$LEN}$"
```
In line **2**, we store the length of the words we want to extract in the variable `LEN`.\
In line **3**, we store the filename in the variable `TEXTFILE`.


To close the editor and save the file, press: {kbd}`Ctrl` + {kbd}`x`, then {kbd}`Y` and press {kbd}`enter` to accept the filename.
``````

::::{exercise} Make `wordlength.sh` executable
The permissions can be changed with the `chmod` command, as seen [before](#section_running_a_shell_script). 

To give the owner execute permissions:
```{code-block} bash
chmod u+x wordlength.sh
```
::::

::::{exercise} Run the `wordlength.sh` script
Now that the script is executable, we can run it with:
```{code-block} bash
./wordlength.sh 18 TOoS2.txt
```
::::

### A Shell Script for Sequence Alignment
In these exercoes, we will make a function that takes an input sequence, finds the most similar sequences in a protein database using BLAST, and then makes a multiple sequence alignment.

First we need a protein database to search in, we can use the human proteins from the SwissProt database that we used before.

::::{exercise} Create a link to the human proteins from the SwissProt database
In the directory that you might have already created for today, create a **l**i**n**k (shortcut) to the `sp_human_single_line` FASTA file, for instance like this:
```{code-block} bash
cd ~/exercises/week1/day5
```
```{code-block} bash
ln -s ~/exercises/week1/day1_2/sp_human_single_line.fasta ./
```
:::{note} Note
You could also copy it, but for large files that is a waste of disk space.
:::

Since `ln` does not give an error if the source file does not exist, check that the file is there using:
```{code-block} bash
head -n 10 sp_human_single_line.fasta
```
::::

::::{exercise} Make a BLAST database
Remember how you created a BLAST database using `makeblastdb`? 

We now need to add an additional {term}`option` to make sure we can retrieve protein sequences from the database with protein IDs: `parse_seqids`

**Create the BLAST database**. For the next part it is useful to get the BLAST results in table format, which is achieved with the
{term}`option`: `-outfmt 7` (see [documentation](https://www.ncbi.nlm.nih.gov/books/NBK279684/table/appendices.T.options_common_to_all_blast/)).

**Test your BLAST database** by searching it with the `proteinX.fasta` that you used in [](#exc_cmdline_blast) from [](#basic_linux_commands_page). You can copy it to the current directory, or use it directly with its path, e.g: `../day1_2/proteinX.fasta`

Now you should see a table, with the BLAST hits in the rows and a number of columns with properties of the matches. As you may know. BLAST not only reports exact matches, but also similar sequences. The *bit score* column is a measure of the similarity between the query sequence and the matching sequence, and the *e-value* column gives an indication of the number of random hits we
would expect with that score. Therefore, BLAST matches with a high e-value are often not very useful, since they are likely to have been found by chance, so we usually filter these out. 

The default behavior of BLAST is to remove hits with e-values over 10.0, but here we want to be stricter and set that to 0.001 (also written as 1e-3). 

**Please add the appropriate {term}`option` and check that it works.**
::::

::::{exercise} Catch the protein IDs of the matching sequences
For the next steps we only need the IDs of the matching sequences, which are in the "subject accessions" column. 

To do this you should use this value for the output format {term}`option`: `"6 sacc"` (including the quotes).

Because we want to create a script to do the whole analysis, the results of the BLAST run should be stored in a Shell variable (much more about variables in the next weeks).

To catch the output in a new Shell variable called `BLASTHITS`, you can run it like this:
```{code-block} bash
BLASTHITS=`blastp -query proteinX.fasta -db sp_human -evalue 1e-3 -outfmt "6 sacc"`
```
:::{caution} Important
The quotes surrounding the whole command should be backticks. 
:::

You can view the resulting value of the `BLASTHITS` variable this way:
```{code-block} bash
echo $BLASTHITS
```
::::

::::{exercise} Extract the sequences for each hit from the `sp_human` BLAST database
The `BLASTHITS` is a list of subject accessions; to print them out individually use a so-called [`for`-loop](#section_ss_for_loop). Much more about `for`-loops in the [](#python_intro) block.

```{code-block} bash
for BLASTHIT in $BLASTHITS; do
    echo $BLASTHIT
done
```

Next, we can use the `blastdbcmd` command to extract the sequences for each hit from the `sp_human` BLAST database:
```{code-block} bash
for BLASTHIT in $BLASTHITS; do
    blastdbcmd -db sp_human -entry $BLASTHIT -long_seqids
done
```

And by [redirecting](#section_redirection) the output using the `>` character we can write these sequences to a FASTA file:

```{code-block} bash
for BLASTHIT in $BLASTHITS; do
    blastdbcmd -db sp_human -entry $BLASTHIT -long_seqids
done > blasthits.fasta
```

Last, you can use [](#sed_section) to beautify the IDs in the FASTA file (what does the `-i` {term}`option` do?)
```{code-block} bash
sed -i 's/>.*[|]/>/' blasthits.fasta
```
::::

