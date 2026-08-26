---
title: Practical Computing for Biologists
label: pcfb_home
abbreviations:
    DNA: Deoxyribonucleic acid
bibliography:
    .bib
---

## Introduction
This course offers a practical introduction to advanced computer use for the analysis of biological data. It is focused on technical aspects of handling large data files, working on remote computers running the Linux operating system using the command line (shell), and developing practical programming/scripting skills. There will be some emphasis on biological molecules (DNA, proteins, etc.), but the used methods are generally applicable to all biological fields.

```{important} Learning outcomes
After successful completion of this course students are expected to be able to:
- explain fundamental computational concepts like CPU, memory, network, file system, compression, indexing
- be proficient in command line (shell) usage
- analyse biological data using command line tools
- store biological data in appropriate data structures, like strings, lists and dictionaries
- apply simple algorithms to filter and simplify biological data
- write and modify simple computer scripts (in Python) for data analysis and visualization
```

## Reader Structure
This reader is organized to guide you step-by-step through the practical skills required for computing in bioinformatics.

### Section Layout
* **Learning Goals:** Each section begins with specific learning goals detailing what you should understand and be able to do by the end.
* **Theory & Examples:** Concepts are explained alongside hands-on code examples and practical demonstrations.
* **Exercises:** Every chapter/day ends with practical exercises designed to test your understanding and reinforce key concepts.

## Book
As reference we use the book (available from the WUR library as ebook):  
Computing Skills for Biologists – A Toolbox, Stefano Allesina & Madlen Wilmes. Paperback | 2019 ISBN: 9780691182759 | eBook | eISBN: 9780691183961.

https://computingskillsforbiologists.com/

## Reading Guide
The text in this reader is decorated with different colors and colored boxes to represent specific material. Here, we will clarify the meaning of these styles. 

Any link or cross-reference is colored blue: like the [](#glossary_md) page. Terms in the glossary are colored purple, like: {term}`hardware`. Hovering over the term will give the definition and clicking on the term will send you to the glossary. Abbreviations have a grey underline like: DNA. Hovering over the abbreviation will give you the full word or phrase. In-text code is depicted as pink in monospaced font like: `"Hello"`. 

Additionally, code is depicted in code blocks, which can be copied:

```{code-block} bash
echo "Hello World"
```
Or cannot be copied:
```{code-block} bash
:class: no-copybutton
Hello World
```
The latter is used to depict output from and usage of tools, programs, scripts, and functions for which it does not make sense to be used by you. 

If we write code in a file, it will be depicted with the filename on top of the code block as follows:

```{code-block} python
:filename: helloworld.py

print("Hello World")
```

The colored boxes and their function will be explain within each box:


:::{margin}
If something is written on the side, or the margin, this is extra information that is not part of the exam material but serves to give fun facts and more extensive information that is outside the scope of this course.
:::

:::{important} Learning outcomes
In this blue box with the lightning bolt icon, you will find the learning outcomes.
:::

:::{seealso} Further reading
In the purple box with the right arrow icon, you will find related chapters to the book, and sometimes additional links.
:::

:::{caution} Important
In the orange box with the exclamation mark icon, you will find important information that you should not skip. Information in this box usually tells you something that can have undesirable consequences when ignored or misused.
:::

:::{note} Note
In the blue box with the "i" icon, you will find additional or clarifying information.
:::

:::{tip} Tip
In the green box with a pen icon, you will find useful tips.
:::

:::{prf:example} This is an example
In the light green box, you will find (code) examples support the text.
:::

:::{exercise} This is an exercise
In the light blue box, you will find the exercises.
:::




## Lab journal
We highly recommend keeping a lab journal to record your exercise work:
- What did you do?
- Specify URLs, programs, settings, etc.
- What were the results?

You can simply use a text file, for instance a Word or Google docs document. You can also use more advanced software, like [Obsidian](https://obsidian.md/), [Microsoft OneNote](https://onenote.cloud.microsoft/) or [Notion](https://www.notion.com/).

It is a time investment which will pay off by solving the same problem twice or having to reconstruct what you did two weeks ago.