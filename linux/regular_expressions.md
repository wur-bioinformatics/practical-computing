---
title: Regular Expressions
label: regular_expressions
abbreviations:
    RE: Regular Expression
bibliography:
    regular_expressions.bib
---

```{important} Learning outcomes
After completing this section you should be able to:
- be proficient in command line (shell) usage *#!this should be more specified I think*
```

## Introduction
In this section, you will learn about and practice with {term}`regular Expressions <Regular Expression>`, a powerful tool to find patterns in text. They are also called 'regex' or abbreviated as 'RE'.

*#! needs better introduction imo, also that it can be used on the cmdline and using python modules and that syntax can differ between languages*

## What are Regular Expressions and why use them?
```{seealso} Computing Skills for Biologists - a Tool box
- Chapter 5.1 What Are Regular Expressions?
- Chapter 5.2 Why Use Regular Expressions?
```

{term}`Regular Expressions <Regular Expression>` are a sequence of characters that define a search pattern, mainly for use in pattern matching with strings, or string matching, i.e. 'find and replace'-like operations [@wikipedia_regular_2026]. {term}`Regular Expressions <Regular Expression>` are often used to find (and replace) patterns in text, as can be seen in {numref}`Example %s <pattern_example>`.

``````{admonition} Patterns in text
:name: pattern_example
:numbered: true
:class: simple myst-example
:icon: false

In the following -omics fields notice the pattern in the text:

<span style="color: #17cc4d;"> Gen</span><span style="color: #fb0c0c;">omics</span>\
<span style="color: #17cc4d;"> Transcript</span><span style="color: #fb0c0c;">omics</span>\
<span style="color: #17cc4d;"> Prote</span><span style="color: #fb0c0c;">omics</span>

This pattern can be captured by the following {term}`Regular Expression`: \
<span style="color: #17cc4d;"> \\w+</span><span style="color: #fb0c0c;">omics</span>
``````

*#! Could be more about the "why"*


## Metacharacters
```{seealso} Computing Skills for Biologists - a Tool box
- Chapter 5.4.1 Literal Characters
```

{term}`Regular Expressions <Regular Expression>` make use of a syntax that describes the search pattern. The syntax is made up of literal characters ({numref}`Example %s <normal_char_example>`) and {term}`metacharacters <metacharacter>`. A {term}`metacharacter` is a symbol with a special, non-literal meaning. Here, we will discuss the most important {term}`metacharacters <metacharacter>`: {term}`wildcards <wildcard>`, boundaries, and quantifiers, *#! edit this has changed* and how to make them literal (by escaping). 

``````{admonition} Normal characters match themselves
:name: normal_char_example
:numbered: true
:class: simple myst-example
:icon: false
A normal, or literal, character matches itself:

`a` matches 'a'

``````

### Wildcards
```{seealso} Computing Skills for Biologists - a Tool box
- Chapter 5.4.2 Metacharacters\*
- Chapter 5.4.7 Raw String Notation and Escaping Metacharacters

\* Note: The book calls {term}`wildcards <wildcard>` "metacharacters", but we hold the definition that a {term}`metacharacter` is any symbol with a special, non-literal meaning and a {term}`wildcard` is a specific symbol that represents unknown or unimportant data.
```

{term}`Wildcards <wildcard>` match a range of different characters. An example of a {term}`wildcard` and what characters it matches is shown in {numref}`Example %s <word_char_example>`. 

```{admonition} Wildcard that matches any 'word' character
:name: word_char_example
:numbered: true
:class: simple myst-example
:icon: false
The {term}`wildcard` `\w` matches any 'word' character:
- `\w` matches 'a'
- `\w` matches 'b'
- `\w` matches 'A'
- `\w` matches '5'
```

The various {term}`wildcards <wildcard>` and the characters they match are listed in {numref}`wildcards_table`.

```{list-table} Wildcards
:header-rows: 1
:label: wildcards_table
* - Wildcard
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
* - `\s`
  - any whitespace
  - tabs and spaces
* - `\w`
  - any 'word' character 
  - alphabet + digits
* - `\d`
  - any digits
  - [0-9] *#! in slide says [1-9] but is zero not also a digit?*
* - `.`
  - any character
  - not `\n` or `\r` unless RE modified
* - `\W`
  - any non-word character
  - 
* - `\D`
  - any non-digit character
  - 
* - `\S`
  - any non-white space character
  - 
```

When we combine normal characters and {term}`wildcards <wildcard>`, we can create complex search patterns. Some examples are shown in {numref}`Example %s <pattern_matching_example_1>` and {numref}`Example %s <pattern_matching_example_2>`.

```{admonition} The bear likes blueberries
:name: pattern_matching_example_1
:numbered: true
:class: simple myst-example
:icon: false

For the text:\
The bear likes blueberries

The pattern `b\w\wr` finds the following matches:\
The <span class="regex-match">bear</span> likes blue<span class="regex-match">berr</span>ies 

The pattern `\sb\w\wr\s` finds the following match:\
The<span class="regex-match">{sub}`_`bear{sub}`_`</span>likes blueberries
```

```{admonition} The bear likes to be rewarded with honey
:name: pattern_matching_example_2
:numbered: true
:class: simple myst-example
:icon: false

For the text:\
The bear likes to be rewarded with honey

The pattern `b\w\wr` finds the following match:\
The <span class="regex-match">bear</span> likes to be rewarded with honey

The pattern `b..r` finds the following matches:\
The <span class="regex-match">bear</span> likes to <span class="regex-match">be{sub}`_`r</span>ewarded with honey
```

But what if you want to explicitly match a {term}`wildcard`? In {numref}`Example %s <escaping_wrong_example>` it is shown what happens if we don't alter the search pattern to account for the {term}`wildcard`. 


```{admonition} The blueberries are eaten by the bear. — Incorrect
:name: escaping_wrong_example
:numbered: true
:class: simple myst-example
:icon: false

**For the following text, match `b\w\wr`, but only if it occurs at the end of a sentence:**\
The blueberries are eaten by the bear.

The pattern `b\w\wr.` finds the following match:\
The blue<span class="regex-match">berri</span>es are eaten by the <span class="regex-match">bear.</span>

This does not work as intended... 

**Why did this not work?**
```

Because the dot is a {term}`metacharacter`, it needs to be "escaped". Escaping is when we prepend the character with a backslash (`\`) so it is interpreted as the literal character and not as the {term}`metacharacter`. {numref}`Example %s <escaping_correct_example>` shows the correct way to match the pattern including the dot at the end of the sentence. 


```{admonition} The blueberries are eaten by the bear. — Correct
:name: escaping_correct_example
:numbered: true
:class: simple myst-example
:icon: false

**For the following text, match `b\w\wr`, but only if it occurs at the end of a sentence:**\
The blueberries are eaten by the bear.

The pattern `b\w\wr\.` finds the following match:\
The blueberries are eaten by the <span class="regex-match">bear.</span>
```

```{exercise}
:label: escape_backslash
The backslash '`\`' is also a metacharacter.

**How would you escape the backslash?**
```

```{solution} escape_backslash
:class: dropdown
You can escape the backslash by using another backslash: \
`\\`
```

### Quantifiers
```{seealso} Computing Skills for Biologists - a Tool box
- Chapter 5.4.4 Quantifiers
```
Instead of using `\w\w` in the previous examples (), we could have used a {term}`quantifier`. {term}`Quantifiers <quantifier>` are metacharacters that specify how often the previous character or group of characters should occur [@w3schools_javascript_nodate]. The different quantifiers are listed in {numref}`quantifiers_table`.

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

Instead of how we wrote the first pattern in {numref}`Example %s <pattern_matching_example_1>`, we could use a quantifier as is shown in {numref}`Example %s <quantifier_example_1>`

```{admonition} The bear likes blueberries
:name: quantifier_example_1
:numbered: true
:class: simple myst-example
:icon: false

For the text:\
The bear likes blueberries

The pattern `b\w{2}r` finds the following matches:\
The <span class="regex-match">bear</span> likes blue<span class="regex-match">berr</span>ies 
```

It might not seem worth it to use a quantifier when we try to match only two characters. However, if you want match longer words or patterns, not having to repeat the metacharacters or literal characters makes the pattern clearer and less prone to errors.

```{caution} Greediness
In {numref}`Example %s <quantifier_example_1>`, we used the specific quantifier `{2}`. This is because {term}`Regular Expressions <Regular Expression>` are, by default, greedy. Greedy means that the pattern will search for the longest match. If, instead, we would have used the `+` quantifier, the following would have matched:

For the text:\
The bear likes blueberries

The pattern `b\w+r` finds the following matches:\
The <span class="regex-match">bear</span> likes <span class="regex-match">blueberr</span>ies 
```


### Alternations
Sometimes the patterns we want to match contain either one pattern or another pattern. 
*#! should this be included?*

*#! maybe as example protein seq?*

*#! what about sets and anchors?*



## Regex balancing act
```{seealso} Computing Skills for Biologists - a Tool box
- Chapter 5.8 The Quest for the Perfect Regular Expression
```
Writing a good {term}`Regex <Regular Expression>` involves striking a balance among three concerns:
1. Matching what you want, but ONLY what you want
2. Keeping the {term}`Regex <Regular Expression>` manageable and understandable
3. Keep it computationally efficient (not of immediate concern)

*#! unsure whether it makes sense here*

## Capturing (and Replacing)
```{seealso} Computing Skills for Biologists - a Tool box
- Chapter 5.6 Groups in Regular Expressions
```
Until now, we have only illustrated what text matches a {term}`Regex <Regular Expression>` pattern. But what makes {term}`Regex <Regular Expression>` so useful is that we can capture the match for further processing or that we can replace the match with something else. 

To capture a match we can use the group {term}`metacharacters <metacharacter>`: `(` and `)` (parentheses). Groups are especially useful for when we want to capture only a specific part of a pattern ({numref}`Example %s <capturing_example>`).

```{admonition} While studying biology, she was majoring in zoology.
:name: capturing_example
:numbered: true
:class: simple myst-example
:icon: false

For the text:\
While studying biology, she was majoring in zoology.

We want to capture the subjects. We can perform a Find & Replace as follows:\
**Find:** `.+\W(\w+ology).+\W(\w+ology).+`\
**Replace:** `\1 \2`\
**Result:** biology zoology

The `\1` and `\2` refer to the first and second group captured, i.e. the text that matches the patterns within the parentheses. By stating the Replace as done here, we replace the original text with only the text matched for the groups. 
```

## Notes and Tips
```{seealso} Computing Skills for Biologists - a Tool box
- Chapter 5.7 Verbose Regular Expressions
```
We have introduced you to the basics of {term}`Regular Expressions <Regular Expression>`, but note that this is not an exhaustive explanation of the syntax. If you want to practice with simple exercises, you can go through the tutorial of [RegexOne](https://regexone.com/).

Performing Find-Replace operations can become complex. It might be necessary to perform them in multiple steps. It helps to make steps transparent (especially for yourself). Sometimes that results in making the search pattern more verbose than strictly necessary. Similarly, even if you can do something in one step, it is worth it for transparancy's sake to do it in multiple steps. When doing Find-Replace operations in a graphical text editor, this is extra work. However, on the command line you could have a sequence of as many Find-Replace terms as you like.

```{tip}
In an intermediate step, Replace with obviously non-existing symbols or sequences (e.g. `#&#`), but avoid metacharacters.
```




## Glossary
```{glossary}
Regular Expression
: a sequence of characters that define a search pattern, mainly for use in pattern matching with strings, or string matching, i.e. 'find and replace'-like operations.

metacharacter
: a symbol with a special, non-literal meaning.

wildcard
: a specific symbol that represents unknown or unimportant data.

quantifier
: symbol that specifies how often the previous character (or group or character class) must occur
```
