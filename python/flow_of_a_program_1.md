---
title: Flow of a Program 1
label: flow_of_a_program_1
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

A Python program can be seen as a series of instructions. The interpreter executes the code sequentially. You can use a cooking recipe as an analogy for a program ([](#example_pancake_recipe_complete)).

(example_pancake_recipe_complete)=
::::{prf:example} Pancake recipe
:::{card}
:header: Ingredients:
- 1 cup flour
- 2 tablespoons sugar
- 1 teaspoon baking powder
- 1 cup milk
- 1 egg
- Butter for cooking
:::

:::{card}
:header: Instructions:
1. **Measure** flour and sugar and put them in a bowl.
2. **Add** baking powder and **mix** dry ingredients.
3. **Add** milk and egg to the bowl.
4. **Mix** *until batter is smooth*.
5. *If batter is too thick*, **add** a little more milk.
6. **Heat** a pan and **melt** a little butter.
7. **Pour** some batter into the pan.
8. **Wait** *until bubbles appear*, then **flip**.
9. **Cook** the other side *until golden*.
10. **Cook** 10 pancakes.
11. **Serve** warm and **enjoy**.
:::
::::

## General Linear Flow
The simplest form of a program is linear: one instruction is executed after the other. If we look at the pancake analogy, we can see that the first three instructions have a linear flow ([](#example_pancake_recipe_linear)).


(example_pancake_recipe_linear)=
::::{prf:example} Pancake recipe — Instructions with linear flow

:::{card}
:header: Instructions:
1. **Measure** flour and sugar and put them in a bowl.
2. **Add** baking powder and **mix** dry ingredients.
3. **Add** milk and egg to the bowl.\
...
:::
::::

## Modifying the Flow
We can modify the flow of a program (i.e. make it non-linear) by using control flow structures. The main ones discussed here are conditional branching and looping. They result in that some parts of the program are only executed when specific situations are met ([](#example_pancake_recipe_nonlinear)).

(example_pancake_recipe_nonlinear)=
::::{prf:example} Pancake recipe — Instructions with non-linear flow

:::{card}
:header: Instructions:
...\
4. **Mix** *until batter is smooth*.\
5. *If batter is too thick*, **add** a little more milk.\
...\
8. **Wait** *until bubbles appear*, then **flip**.\
9. **Cook** the other side *until golden*.\
10. **Cook** 10 pancakes\
...
:::
::::


### Conditional Branching
Conditional branching can be used when only part of the program should be executed if a condition is met. In the pancake recipe analogy that would be step 5 ([](#example_pancake_recipe_conditional_branching)). There, we will only add more milk if the batter is too thick.

(example_pancake_recipe_conditional_branching)=
::::{prf:example} Pancake recipe — Instructions with conditional branching

:::{card}
:header: Instructions:
...\
5. *If batter is too thick*, **add** a little more milk.\
...
:::
::::

In Python (similar to Bash ([](#conditional_statements_section))), we can use three keywords for conditional branching: `if`, `elif`, and `else`:
```{code-block} python
:class: no-copybutton
if <condition C1>:
    <do these lines when C1 True>
elif <condition C2>:
    <do these lines when C1 False and C2 True>
elif <condition C3>:
...
else:
    <do these lines when all conditions False>
```

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 3.6.1 Conditional Branching
```

(section_foap1_looping)=
### Looping
Another flow structure are loops. These are used when part of the program needs to be repeated. There are two variants: the `for` loop and the `while` loop. 



```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 3.6.2 Looping
```

#### `while` loop
In the pancake recipe analogy, we see some instructions should be repeated until a condition is met ([](#example_pancake_recipe_while)). These are typical instructions for which a `while` loop would be useful. 

(example_pancake_recipe_while)=
::::{prf:example} Pancake recipe — Instructions with while-loop behaviour
:::{card}
:header: Instructions:
...\
4. **Mix** *until batter is smooth*.\
...\
8. **Wait** *until bubbles appear*, then **flip**.\
9. **Cook** the other side *until golden*.\
...
:::
::::

In a `while` loop, we are repeatedly testing a condition, and only executing the code when the condition is met:
```{code-block} python
:class: no-copybutton
while <condition>:
    <execute code>
```
The `while` loop is controlled by a condition. This can be a Boolean formula, often including a comparison ([](#comparison_operators_section)). 

In a `while` loop, you need to define your own variables and bookkeeping. Something needs to change each iteration, otherwise the condition will never change from `True` to `False`. It is important to keep this in mind, because you want to prevent the case of infinite looping. You can use a counter for bookkeeping by initializing the counter before the loop and incrementing the counter inside the loop (usually at the end of the body) ([](#example_while_loop_counter))

(example_while_loop_counter)=
``````{prf:example} while loop with self-made counter for bookkeeping
```{code-block} python
:linenos:
:emphasize-lines: 1,4
counter = 0
while counter < 5:
    print(counter)
    counter += 1 
```
Will give the output:
```{code-block} bash
:class: no-copybutton
0
1
2
3
4
```

1: The variable `counter` is initialized outside the loop. \
4: The value of `counter` is incremented by `1` at the end of the loop body.
``````

(section_foap1_for_loop)=
#### `for` loop
If we have a known number of repetitions (at the start of the loop), we can use a `for` loop. In the pancake analogy, this would be step 10 ([](#example_pancake_recipe_for)).

(example_pancake_recipe_for)=
::::{prf:example} Pancake recipe — Instructions with for-loop behaviour
:::{card}
:header: Instructions:
...\
10. **Cook** 10 pancakes.\
...
:::
::::

In a `for` loop, Python does the bookkeeping:
```{code-block} python
:class: no-copybutton
for v in values:
    <execute code>
```
Between `for` and `in` you introduce a variable (name) for Python to use (here: `v`).

The loop is controlled by an iterable (here: `values`), which means an object which can return its elements one at a time, such as a list or {term}`string`. The standard function `range()` gives all {term}`integer` values up to a given number ([](#example_for_loop_range)).

(example_for_loop_range)=
``````{prf:example} for loop with range()
```{code-block} python
:linenos:
:emphasize-lines: 1
for i in range(5):
    print(i)
```
Will give the output:
```{code-block} bash
:class: no-copybutton
0
1
2
3
4
```
1: The variable `i` is "generated" by the loop: a new variable is created.  The values for `i` are 0, 1, 2, 3, and 4 (but not 5) for each iteration, consecutively.
``````

The advantage of a `for` loop is that you do not have to do your own bookkeeping.

## Indentation
As you may have noticed, when using control flow structures, the code that is executed is written after an indentation in the line. This indentation defines the structure for the program ([](#example_indentation)). Indentation is Python-specific: in almost all other programming languages special symbols are used to define structure. 

(example_indentation)=
``````{prf:example} Indentation determines what code is executed when
```{code-block} bash
if <condition C1>:
    while <condition C2>:
        <part of while loop>
    <no longer part of while loop, but still inside if>
<outside if>
```
``````

(section_foap1_flow_charts)=
## Flow Charts
To make the structure of a program clearer, you can turn it into a flowchart ([](#flow_charts_img)).

:::{figure} img/flow_charts_programming.svg
:label: flow_charts_img

Example structures of flow charts
:::

## Exercises
Most exercises of today are essentially taken from [Rosalind](https://rosalind.info/problems/locations/). Rosalind is a platform where you can learn bioinformatics via computational problem solving. You can sign up to the platform (if you want) to join the Rosalind competition. 

The title of an assignment from Rosalind starst with an abbreviation, this is the the identifier used by Rosalind. For example, yesterday we did one Rosalind problem already: (DNA) Counting DNA Nucleotides.

When doing these assignments at Rosalind, you will have to download a file containing the input, then run your script, and finally upload (or copy) your answer, all within a set time. For example, if you download the file for problem DNA (Counting DNA Nucleotides), the file is named `rosalind_dna.txt`.  If your script is in file `dna.py`, your can run the script on the given data by this command (in the terminal):  
```{code-block} python
python dna.py < rosalin_dna.txt
```
This will give the answer in the terminal. If you rather want the answer in a file again (e.g. `rosalind_dna.out`), you should redirect the output to file:
```{code-block} python
python dna.py < rosalind_dna.txt > rosalind_dna.out
```

Today, we will do three or four Rosalind assignments, with an introductory exercise before the final one. For the assignments, we supply the sample inputs as text files as well, so you can practice running the scripts.

The remainder of the text in this reader summarizes the exercises in the Jupyter notebook. The Jupyter notebook contains additional steps and hints.


``````{exercise} Start W2D2 Jupyter Notebook
Download the W2D2 Jupyter Notebook from Brightspace.

Just like yesterday ([](#exc_start_w2d1_notebook)), run the notebook with `jupyter notebook` in the terminal.
``````

### (RNA) Transcribing DNA into RNA

``````{exercise} (RNA) Transcribing DNA into RNA
Given a DNA string, write the transcribed RNA string. 

The transcribed RNA string is formed by replacing all occurrences of T in the DNA string by U in the RNA string.


Sample input:
```{code-block} bash
:class: no-copybutton
GATGGAACTTGACTACGTAAATT
```

Sample output:
```{code-block} bash
:class: no-copybutton
GAUGGAACUUGACUACGUAAAUU
```
``````
### (REVC) Complementing a Strand of DNA

``````{exercise} (REVC) Complementing a Strand of DNA
Given a DNA string, write the reverse complement of that string. The reverse complement of a DNA string is formed by reversing the symbols (A, C, G, T) and then taking the complement of each symbol. Complements of A, C, G, T are T, G, C, A, respectively.

Sample input: 
```{code-block} bash
:class: no-copybutton
AAAACCCGGT
```
Sample output:  
```{code-block} bash
:class: no-copybutton
ACCGGGTTTT
```
``````

### (SUBS) Finding a Motif in DNA

(exc_foap1_subs)=
``````{exercise} (SUBS) Finding a Motif in DNA
Given two DNA strings s and t (one line at a time), write all locations in s where t occurs as substring in t, counting from 1.

Sample input: 
```{code-block} bash
:class: no-copybutton
GATATATGCATATACTT
ATAT
```
Sample output:  
```{code-block} bash
:class: no-copybutton
2 4 10
```
``````

### (FIB) Fibonacci Numbers

``````{exercise} Introductory: Fibonacci Numbers
Leonardo of Pisa, later known as Fibonacci, introduced the problem of finding the number of rabbits (or rather pairs of rabbits) after $n$ months, if we start with one pair. 

Assume that each mature pair of rabbits produces a pair of rabbits every month. Newborn rabbits become mature after two months, i.e. they reproduce from the moment they are two months of age.

If we list the numbers of pairs of rabbits after each month, we obtain the so-called Fibonacci sequence $1, 1, 2, 3, 5, 8, 13, 21, ...$. \
The individual numbers are called Fibonacci numbers. They are usually denoted as $F_n$, so $F_n$ is the $n${sup}`th` Fibonacci number.


The formula for Fibonacci numbers is:  
$F_1 = 1$ (one immature pair)  
$F_2 = 1$ (one mature pair)  

And for $n>2$:  
$F_i = F_{i-1} + F_{i-2}$ (all pairs from previous month, plus a pair per mature pair)  

Some mathematicians start at zero:  
$F_0 = 0$ (then $F_2 = F_1 + F_0$)  

The assignment is to write a script that asks the user for a number $n$, and then writes the corresponding Fibonacci number $F_n$. 

For example, for input 7, the output should be 13 (look at the sequence above).

The intermediate results could be stored in a list, but we did not do lists yet. For now, you can keep the last two Fibonacci numbers in variables, and then compute the new Fibonacci number from those two. After computing a new Fibonacci number, move the values to the respective variables before the next step (this can be tricky).
``````


If you have time left, you can do the final exercise. 

``````{exercise} (FIB) Fibonacci Numbers
This is the actual exercise from Rosalind.

Instead of producing one pair of offspring, now each mature pair produces $k$ pairs of offspring every month.  

Copy your previous script, adapt it to ask for two numbers $n$ and $k$, and also adapt the formula for computing offspring.  

For $k=1$, the outcomes should be identical to the standard Fibonacci numbers.  
For $k=3$, the sequence becomes $1, 1, 4, 7, 19, ... $ 

Sample input: 
```{code-block} bash
:class: no-copybutton
5 3
```
Sample output:  
```{code-block} bash
:class: no-copybutton
19
```
``````

