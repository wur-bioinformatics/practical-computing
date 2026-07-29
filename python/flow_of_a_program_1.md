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
Conditional branching can be used when only part of the program will be executed if a condition is met. In the pancake recipe analogy that would be step 5 ([](#example_pancake_recipe_conditional_branching)). There, we will only add more milk if the batter is too thick.

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

### Looping
Another flow structure are loops. These are used when part of the program needs to be repeated. There are tow variants: the `for` loop and the `while` loop. 



```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 3.6.2 Looping
```

#### `while` loop
In the pancake recipe analogy, we see some instructions should be repeated until a condition is met ([example_pancake_recipe_while](#)). These are typical instructions for which a `while` loop would be useful. 

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

In a `while` loop, you need to define your own variables and bookkeeping. Something needs to change each iteration, otherwise the condition will never change from True to False. It is important to keep this in mind, because you want to prevent the case of infinite looping. You can use a counter for bookkeeping by initializing the counter before the loop and incrementing the counter inside the loop (usually at the end of the body) ([](#))

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


#### `for` loop
If we have a known number of repetitions (at the start of the loop), we can use a `for` loop. In the pancaka anlogy, this would be step 10 ([](#example_pancake_recipe_for)).

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

## Flow Charts

## Exercises
