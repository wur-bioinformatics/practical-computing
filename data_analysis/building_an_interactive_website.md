---
title: Building an Interactive Website
label: building_an_interactive_website
abbreviations:
    HTML: HyperText Markup Language
bibliography:
    .bib
---

```{important} Learning outcomes
After completing this section you should be able to:
- Understand what HTML is and how it is used to build web pages
- Understand how dynamic web pages can be built using Python
```

## Introduction

## HTML
HTML is the standard language for creating Web pages. It describes the structure of the Web page. An HTML page consists of a series of elements and these elements tell the Web browser how to display the content. Elements are delimited by so-called HTML tags that are enclosed in < and > symbols. For instance, if a piece of text should be printed in bold, with HTML you can use the `<b>` tag and its accompanying closing tag `</b>`:
(example_bold_tag)=
 ``````{prf:example} bold tag
 This HTML:  
 `print <b>this text</b> in bold`

Will be shown in the browser as:  
print <b>this text</b> in bold
``````

(example_html_simple_page)=
``````{prf:example} Simple HTML page
Given the contents of this simple HTML page:
```{code-block} html
:filename: hello.html
:linenos:
<html>
<head>
<title>My page</title>
</head>
<body>
<h1>Hello there!</h1>
</body>
</html>
```
In line **1**: the `<HTML>` element is the root element of an HTML page\
In line **2**: the `<head>` element contains meta information about the HTML page\
In line **3**: the `<title>` element indicates the title of the HTML page\
In line **5**: the `<body>` element contains the page's body: it is a container for all visible content
In line **6**: the `<h1>` element defines a large heading 
``````

### HTML elements



## Python Flask

## Exercises
