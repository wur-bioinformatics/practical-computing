---
title: Regular Expressions
label: regular_expressions
abbreviations:
    RE: Regular Expression
    SNP: Singe Nucleotide Polymorphism
bibliography:
    regular_expressions.bib
---

```{important} Learning outcomes
After completing this section you should be able to:
- be proficient in command line (shell) usage *#!this should be more specified I think*
```

## Introduction
In this section, you will learn about and practice with {term}`Regular Expressions <Regular Expression>`, a powerful tool to find patterns in text. They are also called 'Regex' or abbreviated as 'RE'.


*#! needs better introduction imo, also that it can be used on the cmdline and using python modules and that syntax can differ between languages*

## What are Regular Expressions and why use them?
{term}`Regular Expressions <Regular Expression>` are a sequence of characters that define a search pattern, mainly for use in pattern matching with {term}`strings <string>`, or {term}`string` matching, i.e. 'find and replace'-like operations [@wikipedia_regular_2026]. {term}`Regular Expressions <Regular Expression>` are often used to find (and replace) patterns in text, as can be seen in [](#example-patterns-in-text).

(example-patterns-in-text)=
``````{prf:example} Patterns in text
In the following -omics fields notice the pattern in the text:

<span style="color: #17cc4d;"> Gen</span><span style="color: #fb0c0c;">omics</span>\
<span style="color: #17cc4d;"> Transcript</span><span style="color: #fb0c0c;">omics</span>\
<span style="color: #17cc4d;"> Prote</span><span style="color: #fb0c0c;">omics</span>

This pattern can be captured by the following {term}`Regular Expression`: \
<span style="color: #17cc4d;"> \\w+</span><span style="color: #fb0c0c;">omics</span>
``````

*#! Could be more about the "why"*

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 5.1 What Are Regular Expressions?
- Chapter 5.2 Why Use Regular Expressions?
```
## Metacharacters
{term}`Regular Expressions <Regular Expression>` make use of a syntax that describes the search pattern. The syntax is made up of literal characters ([](#normal_char_example)) and {term}`metacharacters <metacharacter>`. A {term}`metacharacter` is a symbol with a special, non-literal meaning. Here, we will discuss the most important {term}`metacharacters <metacharacter>`: {term}`character classes <character class>`, {term}`wildcard`, {term}`non-printable characters <non-printable character>`, {term}`quantifiers <quantifier>`, {term}`sets <set>`, anchors, and alternations, and how to make them literal (by {term}`escaping <escape>`). 


(normal_char_example)=
``````{prf:example} Normal characters match themselves
A normal, or literal, character matches itself:

`a` matches 'a'
``````

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 5.4.1 Literal Characters
```

### Character classes
{term}`Character classes <character class>` are {term}`metacharacters <metacharacter>` that represent a group of characters such as word characters ([](#word-char-example)) or digits. 

(word-char-example)=
```{prf:example} Character class metacharacter that matches any 'word' character
The {term}`character class` `\w` matches any 'word' character:
- `\w` matches 'a'
- `\w` matches 'b'
- `\w` matches 'A'
- `\w` matches '5'
```

The character classes and what they match are presented in [](#character_class_table).

```{list-table} Character classes
:header-rows: 1
:label: character_class_table
* - Character class
  - Matches ...
  - Further information
* - `\s`
  - any whitespace
  - tabs and spaces
* - `\w`
  - any 'word' character 
  - alphabet + digits *#! also underscore?*
* - `\d`
  - any digits
  - [0-9] *#! in slide says [1-9] but is zero not also a digit?*
* - `\W`
  - any non-word character
  - inverse of `\w`
* - `\D`
  - any non-digit character
  - inverse of `\d`
* - `\S`
  - any non-white space character
  - inverse of `\s`
```

When we combine normal characters and {term}`character classes <character class>`, we can create complex search patterns ([](#pattern_matching_example_1)).

(pattern_matching_example_1)=
```{prf:example} The bear likes blueberries
For the text:\
The bear likes blueberries

The pattern `b\w\wr` finds the following matches:\
The <span class="regex-match">bear</span> likes blue<span class="regex-match">berr</span>ies 

The pattern `\sb\w\wr\s` finds the following match:\
The<span class="regex-match">{sub}`_`bear{sub}`_`</span>likes blueberries
```

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 5.4.2 Metacharacters
```

### Wildcard
There is one {term}`metacharacter` that matches any character: the {term}`wildcard` `.` (dot) ([](#pattern_matching_example_2)). 

(pattern_matching_example_2)=
```{prf:example} The bear likes to be rewarded with honey
For the text:\
The bear likes to be rewarded with honey

The pattern `b\w\wr` finds the following match:\
The <span class="regex-match">bear</span> likes to be rewarded with honey

The pattern `b..r` finds the following matches:\
The <span class="regex-match">bear</span> likes to <span class="regex-match">be{sub}`_`r</span>ewarded with honey
```

But what if you want to explicitly match a {term}`wildcard`? In [](#escaping_wrong_example) it is shown what happens if we don't alter the search pattern to account for the {term}`wildcard`. 

(escaping_wrong_example)=
```{prf:example} The blueberries are eaten by the bear. — Incorrect
**For the following text, match `b\w\wr`, but only if it occurs at the end of a sentence:**\
The blueberries are eaten by the bear.

The pattern `b\w\wr.` finds the following match:\
The blue<span class="regex-match">berri</span>es are eaten by the <span class="regex-match">bear.</span>

This does not work as intended... 

**Why did this not work?**
```

Because the dot is a {term}`metacharacter`, it needs to be "escaped". {term}`Escaping <escape>` is when we prepend the character with a backslash (`\`) so it is interpreted as the literal character and not as the {term}`metacharacter`. [](#escaping_correct_example) shows the correct way to match the pattern including the dot at the end of the sentence. 

(escaping_correct_example)=
```{prf:example} The blueberries are eaten by the bear. — Correct
**For the following text, match `b\w\wr`, but only if it occurs at the end of a sentence:**\
The blueberries are eaten by the bear.

The pattern `b\w\wr\.` finds the following match:\
The blueberries are eaten by the <span class="regex-match">bear.</span>
```

```{exercise}
:label: escape_backslash
The backslash '`\`' is also a {term}`metacharacter`.

**How would you {term}`escape` the backslash?**
```

```{solution} escape_backslash
:class: dropdown
You can {term}`escape` the backslash by using another backslash: \
`\\`\
Or by using square brackets:\
`[\]`
```

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 5.4.2 Metacharacters
- Chapter 5.4.7 Raw String Notation and Escaping Metacharacters
```


### Non-printable characters
When writing or processing text, we also use characters that are not visibily seen but do exist to control the text. For example, when you press {kbd}`tab`, you have moved somehwat towards the right in the text but there are no visible characters written. Another example is when you press {kbd}`enter` in a text file, you have moved to the next line but nothing is visibly written in your document. There are actually characters representing this: the {term}`non-printable characters <non-printable character>`. In a text editor or processor, they can often be made visible (in Word: clicking ¶, or {kbd}`control`+{kbd}`shift`+{kbd}`8` (Windows) {kbd}`command`+{kbd}`8` (Mac)). The most commonly used ones are presented in [](#nonprintable_table).

```{list-table} Non-printable characters
:header-rows: 1
:label: nonprintable_table
* - Non-printable character
  - Matches ...
  - Further information
* - `\n`
  - newline 
  - Line Feed or hexadecimal code: X0A
* - `\r`
  - carriage return
  - hexadecimal code: X0D
* - `\t`
  - TAB character
  - as in tab-delimited files (.tsv), in some editors visualised as '→'
```

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 5.4.2 Metacharacters
```

### Quantifiers
Instead of using `\w\w` in the previous examples ([](#pattern_matching_example_1), [](#pattern_matching_example_2), [](#escaping_wrong_example), [](#escaping_correct_example)), we could have used a {term}`quantifier`. {term}`Quantifiers <quantifier>` are {term}`metacharacters <metacharacter>` that specify how often the previous character or {term}`group` of characters should occur [@w3schools_javascript_nodate]. The different {term}`quantifiers <quantifier>` are listed in [](#quantifiers_table).

```{list-table} Quantifiers
:header-rows: 1
:label: quantifiers_table
* - Quantifier
  - Matches the previous character / group  ...
* - `?`
  - zero or one time 
* - `*`
  - zero or more times
* - `+`
  - one or more times
* - `{n}`
  - exactly `n` times
* - `{n,}`
  - at least `n` times
* - `{n,m}`
  - at least `n` and at most `m` times 
```

Instead of how we wrote the first pattern in [](#pattern_matching_example_1), we could use a {term}`quantifier` as is shown in [](#quantifier_example_1).

(quantifier_example_1)=
```{prf:example} The bear likes blueberries
For the text:\
The bear likes blueberries

The pattern `b\w{2}r` finds the following matches:\
The <span class="regex-match">bear</span> likes blue<span class="regex-match">berr</span>ies 
```

It might not seem worth it to use a {term}`quantifier` when we try to match only two characters. However, if you want match longer words or patterns, not having to repeat the {term}`metacharacters <metacharacter>` or literal characters makes the pattern clearer and less prone to errors.

```{caution} Greediness
In [](#quantifier_example_1), we used the specific {term}`quantifier` `{2}`. This is because {term}`Regular Expressions <Regular Expression>` are, by default, {term}`greedy`. {term}`Greedy <greedy>` means that the pattern will search for the longest match. If, instead, we would have used the `+` {term}`quantifier`, the following would have matched:

For the text:\
The bear likes blueberries

The pattern `b\w+r` finds the following matches:\
The <span class="regex-match">bear</span> likes <span class="regex-match">blueberr</span>ies 
```

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 5.4.4 Quantifiers
```

### Sets
In certain cases, you might want to match specific characters or a range of characters ([](#set_example)). This is possible by using a {term}`set`. {term}`Sets <set>` are denoted by square brackets: `[`and `]`. When using a {term}`set`, it means that at that position in the pattern, any of the options denoted within the square brackets may occur. To illustrate, the {term}`set` `[0-9]` represents the same as the `\d` {term}`wildcard`: any digit between 0 and 9.

{term}`Sets <set>` may also be repeated by {term}`quantifiers <quantifier>`. For example, when searching for a protein string, one might only want to include the 20-letter amino acid alphabet instead of using `\w`. 

(set_example)=
```{prf:example} SNP in Sickle Cell Hemoglobin peptide
In a protein string, the amino acid at a certain position can be either glutamine or valine:\
VHLTPEEK\
VHLTPVEK

To capture both these peptides with a {term}`Regex <Regular Expression>` pattern, we could use a {term}`set`:\
`VHLTP[VE]EK`
```

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 5.4.3 Sets
```

### Anchors
If we want to match a pattern to the beginning or end of a {term}`string`, we can use an {term}`anchor`. The start of a line is represented by a hat (`^`), whereas the end of a line is represented by a dollar sign (`$`). This also means that if we want to match a line with a pattern at the beginning of the line, it should start with `^` ([](#anchor_start_example)), and when matching something at the end, the pattern ends with `$` ([](#anchor_end_example)).

(anchor_start_example)=
```{prf:example} Match fruits that start with an 'a'
In a file, where each line is a fruit:\
apple\
orange\
apricot\
banana\
pear\
guave

The pattern `^a\w+` matches only those lines with fruits that start with an 'a':\
<span class="regex-match">apple</span>\
orange\
<span class="regex-match">apricot</span>\
banana\
pear\
guave
```

(anchor_end_example)=
```{prf:example} Match fruits that end with an 'e'
In a file, where each line is a fruit:\
apple\
orange\
apricot\
banana\
pear\
guave

The pattern `^\w+e$` matches only those lines with fruits that end with an 'e':\
<span class="regex-match">apple</span>\
<span class="regex-match">orange</span>\
apricot\
banana\
pear\
<span class="regex-match">guave</span>
```

```{caution} The hat symbol (^) has different meaning depending on how it is used
The hat symbol means beginning of line when it is used plainly: \
`^a` means the pattern matches a line starting with an 'a' ([](#anchor_start_example)).

However, when the hat symbol is used in a {term}`set`, such as `[^a]`, it represents the negation of that set of characters. So, in this case, in that position in the pattern there would **not** be an 'a'.
```

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 5.4.5 Anchors
```

### Alternations
Sometimes the patterns we want to match contain either one pattern or another pattern ([](#alternation_example)). This can be achieved by the pipe symbol (`|`). 

(alternation_example)=
```{prf:example} Life sciences 1
In a file with the lines:\
While studying biology, she was majoring in zoology.\
While studying archeology, she was majoring in anthropology.\
While studying archeology, she was majoring in biology.

We want to capture the only the lines with life science subjects. 

The pattern `.+\W(bi|zo)ology.+` captures the lines:\
<span class="regex-match">While studying biology, she was majoring in zoology.</span>\
While studying archeology, she was majoring in anthropology.\
<span class="regex-match">While studying archeology, she was majoring in biology.</span>
```

```{caution} The pipe symbol occurs in some file formats
Because the pipe symbol (`|`) occurs in some file formats, such as the [FASTA format](wiki:fasta_format), remember to {term}`escape` it when you want to search for it literally!
```

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 5.4.6 Alternations
```


## Regex balancing act
Writing a good {term}`Regex <Regular Expression>` involves striking a balance among three concerns:
1. Matching what you want, but ONLY what you want
2. Keeping the {term}`Regex <Regular Expression>` manageable and understandable
3. Keep it computationally efficient (not of immediate concern)

*#! unsure whether it makes sense here*

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 5.8 The Quest for the Perfect Regular Expression
```

## Capturing (and Replacing)
Until now, we have only illustrated what text matches a {term}`Regex <Regular Expression>` pattern. But what makes {term}`Regex <Regular Expression>` so useful is that we can capture the match for further processing or that we can replace the match with something else. 

To capture a match we can use the {term}`group` {term}`metacharacters <metacharacter>`: `(` and `)` (parentheses). {term}`Groups <group>` are especially useful for when we want to capture only a specific part of a pattern ([](#capturing_example)).

(capturing_example)=
```{prf:example} Life sciences 2
For the text:\
While studying biology, she was majoring in zoology.

We want to capture the subjects. We can perform a Find & Replace as follows:\
**Find:** `.+\W(\w+ology).+\W(\w+ology).+`\
**Replace:** `\1 \2`\
**Result:** biology zoology

The `\1` and `\2` refer to the first and second {term}`group` captured, i.e. the text that matches the patterns within the parentheses. By stating the Replace as done here, we replace the original text with only the text matched for the {term}`groups <group>`. 
```

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 5.6 Groups in Regular Expressions
```

## Notes and Tips
We have introduced you to the basics of {term}`Regular Expressions <Regular Expression>`, but note that this is not an exhaustive explanation of the syntax. If you want to practice with simple exercises, you can go through the tutorial of [RegexOne](https://regexone.com/).

Performing Find-Replace operations can become complex. It might be necessary to perform them in multiple steps. It helps to make steps transparent (especially for yourself). Sometimes that results in making the search pattern more verbose than strictly necessary. Similarly, even if you can do something in one step, it is worth it for transparancy's sake to do it in multiple steps. When doing Find-Replace operations in a graphical text editor, this is extra work. However, on the command line you could have a sequence of as many Find-Replace terms as you like.

```{tip}
In an intermediate step, Replace with obviously non-existing symbols or sequences (e.g. `#&#`), but avoid {term}`metacharacters <metacharacter>`.
```

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 5.7 Verbose Regular Expressions
```

## Practical
### Programs and Resources
Graphical text editor

https://regex101.com/

### Exercises
*#! I would change the format of the practical so that the focus is not on what dataset is used (should ofc be specified) but what they are trying to achieve, so that it can be referred to more easily* 


Dataset 1: Hemoglobin
- find start codons
- remove newline characters
- find orfs

Dataset 2: Crane tracking data
- csv→tsv
- extract columns
- split column

Dataset 3: Human protein sequences
- convert PROSITE pattern to regular expression
- use of `^` in a regular expression

Dataset 4: OOS
- using meta characters to find 4-letter words
- use `\w` to find the longest word(s) in the text
- find a word that is repeated



