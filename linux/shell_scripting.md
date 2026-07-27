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
Now that you have got more experience with {ref}`Advanced_Linux_Commands` and {ref}`Pipelines`, it is fairly easy to turn them into a script. Scripts can be written in different programming and scripting languages, such as Python, Bash, and R. Each language has its own syntax, rules, and vocabulary.

File extensions are commonly used to indicate the language in which a script is written. For example, Python scripts usually have the `.py` extension, while R scripts usually have the `.R` extension and bash shell scripts often have the `.sh` extension.

On Windows, the file extension determines which program is used to open or run a script. On Linux, the extension is mainly informative. To specify which interpreter should execute the script, you can add a *shebang* as the first line of the file.

```{margin}
The shebang (`#!`) is a combination of the sharp or hash symbol (`#`) and an exclamation mark, also known as bang (`!`).
```

The advantages of turning pipelines into scripts are that your commands are saved into a file and can be executed any time on any (relevant) file. For example, if you have multiple FASTA files on which you want to perform the same operations, you don't have to rewrite your pipeline many times, you can just execute the script with those files. Additionally, if in 6 months you want to perform that same operation on a new FASTA file, you don't have to go through your notes to find the right pipeline. Instead, you can use your written script. 


### Basic Structure of a Shell Script
A {term}`shell script` is a (text) file containing a series of commands that the shell can interpret and execute [@geeksforgeeks_shellscripting_2026]. 

Let's build a simple {term}`shell script` that writes 'Hello World' to screen called `hello_world.sh`. 


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

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 1.7 Basic Scripting
```


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

```{tip}
The `.` represents the current directory. 
```
 
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
- The very first character (1) is `-` for normal files, and for instance `d` for **d**irectories. 
- Characters 2-4 show the permissions for the owner of the file (`user001`), who can **r**ead and **w**rite (`rw-`).
- Characters 5-7 show the permissions for users in the usergroup (`domain users`), who can only **r**ead (`r--`) 
- Characters 8-0 show the permissions for all other users on the system, who also can only **r**ead (`r--`)

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
In line **3** the variable is introduced. Note that there should be zero spaces around the '`=`' sign. By convention, variable names are written in all caps. Additionally, because variables can only contain one item, here string quotes are added because "Hello World" contains a space. In line **4** the variable is called by writing the dollar sign (`$`) before the variable name. 

We can also use variable calling when running a script with arguments. Instead of hard-coding *#! hardcoding a term?* the greeting into the file, we can supply it on the command line as an argument, making the script more flexible:

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

To apply the concept of variables to a more biological problem, in [](#pipe_grep_sed_script_example) we turn the pipeline from [](#pipe_grep_sed_example)` in @adv_linux_commands_pipes into a flexible {term}`shell script`.

(pipe_grep_sed_script_example)=
``````{prf:example} Script to print all protein identifiers in a FASTA file to screen
Let's turn first the pipeline from [](#pipe_grep_sed_example) in @adv_linux_commands_pipes into a shell script:

```{code-block} bash
:filename: extract_protein_ids_hardcoded.sh
#!/bin/bash
# Print all protein identifiers in plants.fasta to screen
grep ">" plants.fasta | sed 's/>.*|//'
```

We have now hard-coded the filename `plants.fasta` into the script, meaning that everytime we run the script, it will print the protein identifiers of `plants.fasta`. If we would want to do the same thing but for a different file (for example `trees.fasta` containing all protein sequences of your favourite tree), we would have to make a copy of the script and alter the FASTA filename. This is of course tedious and misses the point of creating {term}`shell scripts <shell script>`. 

Instead, we can supply the script with the FASTA file as an argument and use variable calling in the script.

```{code-block} bash
:filename: extract_protein_ids.sh
#!/bin/bash
# Print all protein identifiers in a fasta file to screen
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

### for loops
A `for` loop in a {term}`shell script` allows you to execute commands or pipelines repeatedly, for a specified amount of times, or for multiple files. The basic structure of a for loop in a {term}`shell script` is:

```{code-block} bash
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
```{code-block} bash

```

```{code-block} bash
:class: no-copybutton

```

``````

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 1.8 Simple `for` loops
```

### Conditional Statements
*#! if statements*

En wat inspiratie voor conditional statements:
 
printwelcome() {
    HOUR=`date "+%H"`
    NAME=`finger $USER | grep Fullname: | sed 's/Fullname:\s\+//'`
    if [ $HOUR -lt 12 ]; then
        TIMEOFDAY="morning"
    elif [ $HOUR -lt 18 ]; then
        TIMEOFDAY="afternoon"
    else
        TIMEOFDAY="evening"
    fi
 
    echo Good $TIMEOFDAY $NAME, you look great today!
}




## Exercises


