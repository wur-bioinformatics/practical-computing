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
- explain the concept of pattern matching and identify scenarios where regular expressions are useful.
```

## Introduction
Biologists often work with large amounts of text-based data, including DNA and protein sequences, gene identifiers, sample names, annotation files, and experimental metadata. {term}`Regular Expressions <Regular Expression>` provide a powerful way to describe and search for patterns in such data. They can be used, for example, to find dates, extract gene identifiers, validate sequence formats, or identify motifs in strings of text. In this section, you will learn how to recognize and construct regular-expression patterns and apply them to biological data.

Many programming language can use {term}`Regular Expressions <Regular Expression>` and there can be slight differences in syntax. Here, we mainly use the Bash syntax (for [`grep`](#grep_section), [`awk`](#awk_section), and [`sed`](#sed_section)) and the Python syntax (*#! forward ref to python part*). 

## What are Regular Expressions and why use them?
{term}`Regular Expressions <Regular Expression>` are a sequence of characters that define a search pattern, mainly for use in pattern matching with {term}`strings <string>`, or {term}`string` matching, i.e. 'Find and Replace'-like operations [@wikipedia_regular_2026]. {term}`Regular Expressions <Regular Expression>` are also called 'Regex' or abbreviated as 'RE'. {term}`Regular Expressions <Regular Expression>` are often used to find (and replace) patterns in text, as can be seen in [](#example-patterns-in-text).

(example-patterns-in-text)=
``````{prf:example} Patterns in text
In the following -omics fields notice the pattern in the text:

<span style="color: #17cc4d;"> Gen</span><span style="color: #fb0c0c;">omics</span>\
<span style="color: #17cc4d;"> Transcript</span><span style="color: #fb0c0c;">omics</span>\
<span style="color: #17cc4d;"> Prote</span><span style="color: #fb0c0c;">omics</span>

This pattern can be captured by the following {term}`Regular Expression`: \
<span style="color: #17cc4d;"> \\w+</span><span style="color: #fb0c0c;">omics</span>
``````

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 5.1 What Are Regular Expressions?
- Chapter 5.2 Why Use Regular Expressions?
```


## Metacharacters
{term}`Regular Expressions <Regular Expression>` make use of a syntax that describes the search pattern. The syntax is made up of literal characters ([](#normal_char_example)) and {term}`metacharacters <metacharacter>`. A {term}`metacharacter` is a symbol with a special, non-literal meaning. Here, we will discuss the most important {term}`metacharacters <metacharacter>`: {term}`character classes <character class>`, {term}`wildcard`, {term}`non-printable characters <non-printable character>`, {term}`quantifiers <quantifier>`, {term}`sets <set>`, {term}`anchors <anchor>`, and alternations, and how to make them literal (by {term}`escaping <escape>`). 


(normal_char_example)=
``````{prf:example} Normal characters match themselves
A normal, or literal, character matches itself:

`a` matches 'a'
``````

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 5.4.1 Literal Characters
```

(character_classes_section)=
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

The {term}`character classes <character class>` and what they match are presented in [](#character_class_table).

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
Instead of using `\w\w` in the previous examples ([](#pattern_matching_example_1), [](#pattern_matching_example_2), [](#escaping_wrong_example), [](#escaping_correct_example)), we could have used a {term}`quantifier`. {term}`Quantifiers <quantifier>` are {term}`metacharacters <metacharacter>` that specify how often the previous character, {term}`character group` or {term}`character class` should occur [@w3schools_javascript_nodate]. The different {term}`quantifiers <quantifier>` are listed in [](#quantifiers_table).

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

(greediness_caution)=
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
In certain cases, you might want to match specific characters or a range of characters ([](#set_example)). This is possible by using a {term}`set`. {term}`Sets <set>` are denoted by square brackets: `[`and `]`. When using a {term}`set`, it means that at that position in the pattern, any of the options denoted within the square brackets may occur. To illustrate, the {term}`set` `[0-9]` represents the same as the `\d` {term}`character class`: any digit between 0 and 9.

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

(anchors_section)=
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

## Capturing (and Replacing)
Until now, we have only illustrated what text matches a {term}`Regex <Regular Expression>` pattern. But what makes {term}`Regex <Regular Expression>` so useful is that we can capture part of the match for further processing or that we can replace parth of the match with something else. 

To capture part of a match, we can enclose it in parentheses (`(` and `)`). {term}`Groups <group (regex)>` are especially useful for when we want to capture only a specific part of a pattern ([](#capturing_example)).

(capturing_example)=
```{prf:example} Life sciences 2
For the text:\
While studying biology, she was majoring in zoology.

We want to capture the subjects. We can perform a Find & Replace as follows:\
**Find:** `.+\W(\w+ology).+\W(\w+ology).+`\
**Replace:** `\1 \2`\
**Result:** biology zoology

The `\1` and `\2` refer to the first and second {term}`group <group (regex)>` captured, i.e. the text that matches the patterns within the parentheses. By stating the Replace as done here, we replace the original text with only the text matched for the {term}`groups <group (regex)>`. 
```

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 5.6 Groups in Regular Expressions
```

## Notes and Tips
We have introduced you to the basics of {term}`Regular Expressions <Regular Expression>`, but note that this is not an exhaustive explanation of the syntax. If you want to practice with simple exercises, you can go through the tutorial of [RegexOne](https://regexone.com/).

Writing a good {term}`Regex <Regular Expression>` involves striking a balance among three concerns:
1. Matching what you want, but ONLY what you want
2. Keeping the {term}`Regex <Regular Expression>` manageable and understandable
3. Keep it computationally efficient (not of immediate concern)

Performing Find-Replace operations can become complex. It might be necessary to perform them in multiple steps. It helps to make steps transparent (especially for yourself). One way to do that is, as an intermediate step, Replace with obviously non-existing symbols or sequences (e.g. `#&#`), but avoid {term}`metacharacters <metacharacter>`. That way, you can make it cleary visible what is being replaced and assess whether that is what you expected. 

Additionally, it can help to make the search pattern more verbose than strictly necessary. Sometimes {term}`Regular Expressions <Regular Expression>` become very hard to read. Explicitly stating what each part of the {term}`Regular Expression` matches, with for example comments (`#`), can aid readability and reusability. 

```{seealso} Further Reading
Computing Skills for Biologists - a Tool box
- Chapter 5.7 Verbose Regular Expressions
- Chapter 5.8 The Quest for the Perfect Regular Expression
```

## Exercises
For some of the following exercises, it is recommended to use a graphical text editor. The options for your {term}`operating system` and their functions for either Find or Find/Replace operations are summarized in [](#graphical_text_editors_table).

(graphical_text_editors_table)=
```{list-table} Graphical text editors for Find/Replace
:header-rows: 1
* - Graphical text editor
  - Operating system
  - Find operation settings
  - Find/Replace operation settings
* - [Notepad++](https://notepad-plus-plus.org/)
  - Windows
  - Use the 'Mark' option under 'Find'
  - Under 'Find and Replace', select the 'Search mode' as 'Regular expression'
* - [BBEdit](https://www.barebones.com/products/bbedit/)
  - macOS
  - Use the 'Find All' option
  - Under 'Find and Replace', select 'Grep'
* - [Gedit/Text Editor](https://gedit-text-editor.org/install.html)
  - macOS, Linux, Windows
  - Use  the 'Find...' option
  - Under 'Find and Replace', select the 'Search mode' as 'Regular expression'
```

For other exercises, you can use the [regex101](https://regex101.com/). This site is very handy for experimenting with {term}`Regular Expressions <Regular Expression>`. At the left side of the page, you can select the {term}`regex <Regular Expression>` 'Flavor'. For these exercises select 'Python' as 'Flavor'. At the top of the page, you can type your {term}`Regular Expression`. This is followed by the `"` character after which you can add "modifiers" to the {term}`Regular Expression`. For these exercises, type `'g'` as the modifier, so that any {term}`Regular Expression` you make will become "global". 


### Finding ORFs in Sequences
For these exercises, you will use the dataset `HemoglobinAs.fa`, containing Hemoglobin subunit A1 coding sequences (RefSeq) for human, cow, and mouse. Load the file in your graphical text editor.

(exc_hemoglobin_start_codon_1)=
```{exercise} Find potential start codon (ATG) 1
Find potential start codon (ATG). Use the Find operation settings for your graphical text editor ([](#graphical_text_editors_table)).

**How many potential start codons do you find?**
```

(exc_hemoglobin_remove_newlines)=
```{exercise} Remove newlines from HemoglobinAs.fa
Because of the newlines in the file it is quite possible that one of the potential start codons was missed. To fix this you can remove the newlines from the file. Use the Find/Replace operation settings for your graphical text editor ([](#graphical_text_editors_table)).

Now you should be able to search and replace all newlines (`\r\n` in this file).
```

(exc_hemoglobin_add_newlines)=
```{exercise} (Optional) Add newlines back to HemoglobinAs.fa to create separate entries
When you did the Find/Replace operation in [](#exc_hemoglobin_remove_newlines), the three sequences will be all on the same line, including their description lines. 

Use the Find/Replace functions of the editor to insert newlines so that the sequences are separated from the description lines, for instance using unique characters or words at the start and end of these lines. 

You should end up with a file with 6 lines, 2 lines for each sequence entry in the file.
```

(exc_hemoglobin_start_codon_2)=
```{exercise} Find potential start codon (ATG) 2
Repeat the search for start codons as was done in [](#exc_hemoglobin_start_codon_1). 

**How many do you find now?**\
**Did you miss any in your first attempt in [](#exc_hemoglobin_start_codon_1)?**
```

```{exercise} Find Open Reading Frames (ORFs)
Go to [regex101](https://regex101.com/). As 'Test String', put the sequence (without newlines) for just the Homo sapiens hemoglobin subunit alpha 1 mRNA.

Now try to match a complete open reading frame (ORF), starting with a start codon and ending with a stop codon (nb. the sequence actually contains two ORFs).

For an ORF, combine in order:
1. a start codon (ATG)
2. zero or more codons that are not stop codons (start codons are allowed, they just code for methionine). Watch out for [greediness](#greediness_caution)...!
3. a stop codon (TAG, TGA or TAA)
```

### Working with Column Data
Load in `first_and_last_100_lines_crane_data.csv` in your editor.

```{exercise} Convert from CSV to TSV
Convert from comma-delimited to tab-delimited using Find/Replace. You can use no more than three sequential Find/Replaces.
```

(cranes_extract_columns)=
``````{exercise} Extract columns
Extract only the 1{sup}`st` and 3{sup}`rd` column of the original file, using Find/Replace (for the time being, you don't need to be concerned with the header line).

Result should look like this (for all lines):
```{code-block} bash
:class: no-copybutton
250386109,2013-07-12 04:10:14
250386110,2013-07-12 04:24:05
...
```
``````

``````{exercise} Extract and split columns
From the original file, repeat [](#cranes_extract_columns), but now format column 3 by making separate columns for date and time. 

Result should look like this:
```{code-block} bash
:class: no-copybutton
250386110,2013-07-12,04:24:05
250386111,2013-07-12,04:38:51
...
```
``````

### Converting a PROSITE Pattern to a Regular Expression
Load the file `sp_human_single_line.fasta` in your editor. Use the Find/Replace settings of your specific editor ([](#graphical_text_editors_table)) for the following exercises.

This file contains the human proteins that are in the SwissProt section of the UniProt database. The SwissProt section contains manually curated protein sequences and is considered more reliable than the trEMBL section, which contains protein sequences
obtained by translating predicted open reading frames. The newlines were removed from the sequences to facility pattern matching.

Look up the [PROSITE consensus pattern for ACTINS_1](https://prosite.expasy.org/PDOC00340).

``````{exercise} Convert PROSITE pattern to Regular Expression
Convert the PROSITE pattern to a {term}`Regular Expression`. 

The syntax is quite similar, but PROSITE patterns:
- have a '`-`' to separate elements in
- use an '`x`' to indicate any amino acid
- use parentheses '`()`' instead of curly braces '`{}`' to indicate repetition. 

You are advised to first test the {term}`Regular Expression` on [regex101](https://regex101.com/) with the "sp|P62736|ACTA_HUMAN Actin" sequence. 

When that works, use the {term}`Regular Expression` in the whole file to find the human proteins that belong to the actin family. 

**How many do you find?**
``````

``````{exercise} Use an anchor in a Regular Expression
**How many protein sequences in the file do not have an M as the first amino acid?**

```{tip}
Check the two functions of the `^` character in {term}`Regular Expression` ([](#anchors_section))
```
``````


### Finding Words in a Text File
Open the file that contains the first 2000 characters of chapter 13 of "The Origin" in a text editor (`Origin_of_Species_2000chars.txt`), and subsequently paste the content into [regex101](https://regex101.com/).

``````{exercise} Use metacharacters to find 4-letter words
Using only the {term}`metacharacters <metacharacter>` covered today, make a {term}`Regular Expression` to find all 4-letter words. 

**How many matches did you get?** \
**Did you find all of them?** 

**If not, what kind of {term}`wildcard` or {term}`metacharacter` would you require to make this search more precise?**
``````

Download the complete text of ["The Origin of Species by Means of Natural Selection by Charles Darwin" in utf-8]( https://www.bioinformatics.nl/courses/BIF-50806/pg2009.txt).

``````{exercise} Find the longest word(s)
Find the longest word(s) in the text, for instance using `\w` ([](#character_classes_section))
``````

``````{exercise} Find repeated words
Try to find a word that is (accidentally?) repeated in the text, separated by a space, so like this: \
"try to find a word **that that** is repeated"
``````

