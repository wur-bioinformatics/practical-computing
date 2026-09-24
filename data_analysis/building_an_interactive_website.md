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
- explain how HTML elements are used to structure the content of a web page
- create a simple web page using HTML
- build a simple interactive web application that retrieves and presents information from a database
```

## Introduction

## HTML
HTML is the standard markup language for creating Web pages. It describes the structure of the Web page. An HTML page consists of a series of elements and these elements tell the Web browser how to display the content. Elements are delimited by so-called HTML tags that are enclosed in < and > symbols. For instance, if a piece of text should be printed in bold, with HTML you can use the `<b>` tag and its accompanying closing tag `</b>`:
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
(example_flask_simple_page)=
``````{prf:example} Simple Flask page
With Flask we can quite easily start a webserver that shows web pages. This code will start a webserver listening on your computer, usually at network port 5000, that you can access with: [http://localhost:5000](http://localhost:5000/)
```{code-block} python
:filename: app.py
:linenos:
from flask import Flask

app = Flask(__name__)

@app.route("/")
def greet():
    return "Hello, World!"

if __name__ == "__main__":
    app.run()
```
``````

(example_flask_page_with_template)=
``````{prf:example} Flask using a template
With Flask we can make an HTML page dynamic by adding logic and filling in values. We start with an HTML file like before, but now we added code to it. We can include values from a variable using a pair of double curly braces `{{ }}` and we can add logic like an `if` block by enclosing it in `{% %}`
```{code-block} html
:filename: index.html
:linenos:
<html>
<head>
<title>My page</title>
</head>
<body>
{% if message %}
<h1> {{ message }} </h1>
{% endif %}
<form method="get" action="">
<input type="text" name="my_name">
<input type="submit" value="Greet!">
</form>
</body>
</html>
```

The block between `{% if message %}` and `{% endif %}` is only shown if the variable `message` has a value. Then the value of message is show as a large heading text.

The Python code below is responsible for passing the value of the `message` variable to the template, using Flasks `render_template()` function.
```{code-block} python
:filename: greeter.py
:linenos:
from flask import Flask, request, render_template

app = Flask(__name__)

@app.route('/')
def index():
    msg = ""
    if 'my_name' in request.args:
        name = request.args['my_name']
        msg = f'Hello {name}'
        
    return render_template('index.html',message=msg)

if __name__ == "__main__":
    app.run()
```


``````

## Exercises
