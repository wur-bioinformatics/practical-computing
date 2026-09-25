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
In the previous section you stored BLAST results in a relational database and wrote Python functions to query it. However, not everyone who wants to look at these results can use the command line or Python. A web interface solves this: anyone with a web browser can search the data by simply selecting options and clicking buttons. Many biological databases, such as UniProt and NCBI, are used in exactly this way. This section introduces HTML, the language used to describe web pages, and Flask, a Python framework for building web applications. In the exercises you will combine these with your database functions to build a small website for browsing the BLAST results.

## HTML
HTML is the standard markup language for creating web pages. It describes the structure of the web page. An HTML page consists of a series of elements and these elements tell the web browser how to display the content. Elements are delimited by so-called HTML tags that are enclosed in `<` and `>` symbols. For instance, if a piece of text should be printed in bold, with HTML you can use the `<b>` tag and its accompanying closing tag `</b>`:

(example_bold_tag)=
``````{prf:example} Bold tag
This HTML:\
`print <b>this text</b> in bold`

Will be shown in the browser as:\
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
In line **1**: the `<html>` element is the root element of an HTML page\
In line **2**: the `<head>` element contains meta information about the HTML page\
In line **3**: the `<title>` element indicates the title of the HTML page\
In line **5**: the `<body>` element contains the page's body: it is a container for all visible content\
In line **6**: the `<h1>` element defines a large heading.
``````

### HTML elements
Elements can be nested: an element can contain other elements, as the `<body>` element contains the `<h1>` element in [](#example_html_simple_page). Many elements also have *attributes*, extra settings that are written inside the opening tag, such as `href` in `<a href="...">`. Below are the elements you will need to build a simple web page.

#### Headings and paragraphs
There are six levels of headings, from `<h1>` (largest) to `<h6>` (smallest). Normal text is put in paragraphs with `<p>`:
```{code-block} html
<h1>BLAST results</h1>
<h2>Plants vs human</h2>
<p>This is a paragraph.</p>
```

The browser ignores line breaks and extra spaces in the HTML file: text is only split into paragraphs where you use `<p>` (or a line break `<br>`).

#### Hyperlinks
A hyperlink is made with the `<a>` (anchor) element. The `href` attribute gives the address the link points to, and the text between the tags is what the user clicks on:
```{code-block} html
<a href="https://www.uniprot.org">this is a link to the UniProt website</a>
```

#### Lists
A bulleted list is made with `<ul>` (unordered list) and a numbered list with `<ol>` (ordered list). Each item in the list is enclosed in `<li>` tags:
```{code-block} html
<ul>
    <li>Arabidopsis thaliana</li>
    <li>Coffea arabica</li>
</ul>
```

#### Tables
A table is enclosed in `<table>` tags. Each row is defined by a `<tr>` (table row) element, which contains the cells of that row. Normal cells are defined by `<td>` (table data) and header cells by `<th>` (table header):
```{code-block} html
<table>
<tr>
    <th>query</th><th>target</th>
</tr>
<tr>
    <td>cell one of the first row</td><td>cell two of the first row</td>
</tr>
<tr>
    <td>cell one of the second row</td><td>cell two of the second row</td>
</tr>
</table>
```

#### Forms
A form lets the user enter data and send it to the web server. The `action` attribute of `<form>` gives the URL the data is sent to, and `method="get"` means that the data is added to that URL (as in `/results?target=...`). Inside the form you can put input elements, for example:
- `<input type="text">`: a text field
- `<select>` with `<option>` elements: a selection box (drop-down list) with the options to choose from
- `<input type="submit">`: a button that sends the form

The `name` attribute of an input element is the name under which its value is sent to the web server:
```{code-block} html
<form method="get" action="/results">
    <input type="text" name="cutoff">
    <select name="target">
        <option>sp|P62258|1433E_HUMAN</option>
        <option>sp|O43707|ACTN4_HUMAN</option>
    </select>
    <input type="submit" value="Search">
</form>
```
When the user selects the first option, types `0.001` in the text field and clicks the "Search" button, the browser opens this URL:\
`/results?cutoff=0.001&target=sp%7CP62258%7C1433E_HUMAN`\
(special characters such as `|` are encoded, in this case as `%7C`).

:::{tip} Tip
To see the HTML of any web page, right-click in your browser and choose "View page source".
:::

## Python Flask
(example_flask_simple_page)=
``````{prf:example} Simple Flask page
With Flask we can quite easily start a web server that shows web pages. This code starts a web server that listens on the network port given to `app.run()`:
```{code-block} python
:filename: app.py
:linenos:
from flask import Flask

app = Flask(__name__)

@app.route("/")
def greet():
    return "Hello, World!"

if __name__ == "__main__":
    app.run(port=5001)
```
If you run this on your own computer, you can access the page at [http://localhost:5001](http://localhost:5001/).

On a shared server like bork, only one program at a time can listen on a given port, so every user has to choose their own port number (between 1024 and 60000). To view the page from your laptop, you then need an SSH tunnel from port 5001 on your laptop to that port on the server, as you will do in the [exercises](#building_website_exercises).
``````

(example_flask_page_with_template)=
``````{prf:example} Flask using a template
With Flask we can make an HTML page dynamic by adding logic and filling in values. We start with an HTML file like before, but now we add code to it. We can include values from a variable using a pair of double curly braces `{{ }}` and we can add logic like an `if` block by enclosing it in `{% %}`.

Flask looks for templates in a directory called `templates` next to the Python script, so the files should be organised like this:
```{code-block} text
:class: no-copybutton
greeter/
├── greeter.py
└── templates/
    └── index.html
```

```{code-block} html
:filename: templates/index.html
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

The block between `{% if message %}` and `{% endif %}` is only shown if the variable `message` has a value. Then the value of `message` is shown as a large heading text.

The Python code below is responsible for passing the value of the `message` variable to the template, using Flask's `render_template()` function.
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

    return render_template('index.html', message=msg)

if __name__ == "__main__":
    app.run(port=5001)
```


``````

(building_website_exercises)=
## Exercises
In these exercises we will build a web interface to view the BLAST results of the plant vs human protein BLAST analysis that you stored in a database in [Relational Databases](#relational_databases). For this we will use the Python [Flask](https://flask.palletsprojects.com/) framework.

### Starting simple
``````{exercise} A first Flask application
Log in to bork and `cd` to the directory `~/exercises/blast_browser`. In that directory, create a file `blast_browser.py` with this content:
```{code-block} python
:filename: blast_browser.py
#!/usr/bin/env python3

from flask import Flask, request, render_template

# create web application
app = Flask(__name__)

port = <port> # choose a number between 1024 and 60000

@app.route('/')
def index():
    text_to_return = "BLAST Browser"
    return text_to_return


if __name__ == "__main__":
    # start the web application
    app.run(port=port)
```

Replace `<port>` with a number between 1024 and 60000. After you have saved the script, make it runnable by setting the execute permission in the shell:
```{code-block} bash
chmod a+x blast_browser.py
```

Check with `ls -l` that you see an `x` three times in the permissions block:
```{code-block} bash
:class: no-copybutton
-rwxr-xr-x 1 user001 domain users 852 Oct 1 14:00 blast_browser.py
```

Run the script like this:
```{code-block} bash
./blast_browser.py
```

This will start a simple web server on bork that listens on the port you chose. In the unlikely event that the port is already in use, choose another one and restart the script.

Your laptop cannot directly connect to the web server. Like you did for running notebooks on bork, you should now set up an SSH tunnel to be able to connect to the port. On your laptop, start a new terminal and run (replace `<port>` with the port you selected in the script):
```{code-block} bash
ssh -L 5001:localhost:<port> bork
```

Point a web browser to [http://127.0.0.1:5001](http://127.0.0.1:5001). You should now see a web page that says "BLAST Browser".
``````

``````{exercise} Adding a second page
On bork, stop the script by pressing {kbd}`Ctrl+C` in the terminal and add the following function to the `blast_browser.py` script:
```{code-block} python
@app.route('/results')
def show_results():
    text_to_return = "Results!"
    return text_to_return
```

Start the script again and point your web browser to [http://127.0.0.1:5001/results](http://127.0.0.1:5001/results). Now you should see "Results!".

:::{note} Note
`@app.route` is a so-called *decorator* that in this case specifies that the `/results` URL should be handled by the `show_results()` function. How decorators work is beyond the scope of this course; if you want to know more, see the [Python wiki](https://wiki.python.org/moin/PythonDecorators).
:::
``````

### Using an HTML template
The aim of the following exercises is to make a web page that displays a selection box with all human protein IDs from the `plants_vs_humans` BLAST results and, upon selection of a specific target, shows the BLAST hits for that target. For this we need two HTML pages: one with a form for selecting the target and another with a table for the output.

``````{exercise} Creating a template with a form
With Flask you can use so-called *template* HTML files to combine HTML with scripting. Inside the `blast_browser` directory, create a new directory called `templates` and, in that directory, create a text file called `index.html` with the following content:
```{code-block} html
:filename: templates/index.html
<html>
<head></head>
<body>
<h1>BLAST results plants vs human</h1>
  <form method="get" action="/results">
    <select name="target">
      <option>test1</option>
      <option>test2</option>
    </select>
    <input type="submit" value="Search">
  </form>
</body>
</html>
```

The HTML file starts with the `<html>` opening tag and ends with the `</html>` closing tag. Then there is a header section enclosed in `<head></head>` tags, followed by the body section enclosed in `<body></body>` tags. The body part of the HTML page contains the actual content.

First the title of the page is printed in large font (`<h1>`), and then a form block starts (enclosed in `<form></form>` tags). The form allows users to input data that is then sent back to the web server. The form contains a selection box defined by the `<select></select>` block; the options that can be selected are listed between `<option></option>` tags (currently there are two dummy options). The form also has a *submit* button defined by the `<input type="submit">` tag. Clicking that button submits the form, which in this case calls the [http://127.0.0.1:5001/results](http://127.0.0.1:5001/results) URL.

To make your script use this template file, change the return line of the `index()` function in `blast_browser.py` to:
```{code-block} python
return render_template('index.html', targets=["target1", "target2"])
```

The `targets` variable is passed on to the template, so it will be available in `index.html`. For now its value is a dummy list; later we will change that to the list of targets that you get from the database. You can remove the `text_to_return =` line now.

Test that the changes work by stopping and restarting `blast_browser.py` and then checking the web page in the browser (you should see the form).

To actually use the `targets` variable, we should add some code to the `index.html` file to put the targets in the select block. To do that, replace the two `<option>` lines with this `for` loop:
```{code-block} html
{% for target in targets %}
  <option>{{ target }}</option>
{% endfor %}
```

**Test it by stopping and restarting `blast_browser.py`. What has changed?**
``````

### Adding the list of targets
``````{exercise} Getting the targets from the database
To get the targets from the database, we can use the `db_functions.py` module you wrote in [Accessing SQLite from Python](#accessing_sqlite_from_python), or you can download the `db_functions.py` file from Brightspace to `~/exercises/blast_browser`. Your directory should now look like this (plus the data files from the previous exercises):
```{code-block} text
:class: no-copybutton
blast_browser/
├── blast_browser.py
├── db_functions.py
├── plants_vs_humans.db
└── templates/
    └── index.html
```

In `blast_browser.py`, add a line to import the required functions (somewhere below the first line of the file):
```{code-block} python
from db_functions import get_targets, get_rows_for_target
```

The next step is to pass a list of actual targets to the `index.html` template. Use the appropriate function from `db_functions` to get the list of targets and use that list as the value of `targets` in the `render_template()` call.

**Test that it works by stopping and restarting `blast_browser.py`. In the browser, select a target and press the Search button. What do you see in the URL bar?**
``````

### Processing the query
``````{exercise} Showing the results in a table
Next, we need to display the result. For that we should read the selected target that was sent by the form, query the database for the matching rows and then show those on a web page. Let's first create a new HTML template file called `results.html` in the `templates` folder that shows a table:
```{code-block} html
:filename: templates/results.html
<html>
<head></head>
<body>
<h1>BLAST results plants vs human</h1>
<table>
  <tr>
    <th>query</th>
    <th>target</th>
    <th>E-value</th>
    <th>Description of query</th>
  </tr>
</table>
</body>
</html>
```

The template contains a definition for the output table within the `<table></table>` tags. A row is defined by a `<tr></tr>` block, and a cell by a `<td></td>` block. In the first row you can also define header cells, which are enclosed in `<th></th>`. For now, this table only has a header row.

When you click the Search button in the form, the `/results` URL is called, which in the Flask Python code is linked to the `show_results()` function. In this function we should retrieve the BLAST results for the target protein ID that was selected in the form. So how do we get the value of the selected target? You should have seen it in the URL: `/results?target=some_target`. Arguments that are passed like that are available in the function in a dictionary called `request.args`. So you can add this line to `show_results()`:
```{code-block} python
target = request.args['target']
```

:::{warning} Warning
Never paste values from `request.args` directly into an SQL statement, for instance with an f-string. Anyone can type their own URL, such as `/results?target=' OR '1'='1`, and so change the meaning of your SQL statement. This is called *SQL injection*. Instead, use `?` placeholders and pass the values separately, as in:
```{code-block} python
cursor.execute("SELECT * FROM blast_results WHERE target = ?", (target,))
```
Check that your `get_rows_for_target()` function does this.
:::

Next, use this `target` as input for the appropriate function from `db_functions` to get the list of BLAST results for that target. Pass that list to the `results.html` template by changing the return statement of the `show_results()` function to:
```{code-block} python
return render_template('results.html', rows=BLAST_results)
```

In the `results.html` file, add the code below after the `</tr>` line:
```{code-block} html
{% for row in rows %}
  <tr>
  {% for cell in row %}
    <td>{{ cell }}</td>
  {% endfor %}
  </tr>
{% endfor %}
```

The outer `for` loop adds a new row to the table for each of the BLAST hits; the inner `for` loop fills in the values of the four columns.

**Test the script: does it work?**

:::{tip} Tip
If the results take some time to appear, it may help to add an [index](#relational_db_indices) to the SQLite database. Open the `plants_vs_humans.db` file in the `sqlite3` shell and run this SQL command to create an index on the `target` column of the `blast_results` table:
```{code-block} sql
CREATE INDEX idx_blast_results_target ON blast_results (target);
```
The `ID` column of the `plant_proteins` table does not need an extra index: SQLite automatically creates one for a `PRIMARY KEY`.
:::
``````

#### Extensions
If you have time left, you can improve the website with the challenges below.

``````{exercise} Challenge 1
Make the table look better by adding this block of style between the `<head></head>` tags in `results.html`:
```{code-block} html
<style>
table {
    font-family: arial, sans-serif;
    border-collapse: collapse;
    width: 100%;
}

td, th {
    border: 1px solid #dddddd;
    text-align: left;
    padding: 8px;
}

tr:nth-child(even) {
    background-color: #dddddd;
}
</style>
```
``````

``````{exercise} Challenge 2
Only show rows that have an E-value below a certain cut-off. For this, add an input field for the cut-off to the form in `index.html`:
```{code-block} html
<input type="text" name="cutoff">
```
In `show_results()`, read the value of the cut-off from `request.args`, like you did for the target. Note that all values in `request.args` are strings, so convert it to a number with `float()`. Then pass the cut-off to `get_rows_for_target()` (see Challenge 1 in [Accessing SQLite from Python](#accessing_sqlite_from_python)).

Bonus: make the page also work when the user leaves the cut-off field empty.
``````

``````{exercise} Challenge 3
Combine both Python functions (`index()` and `show_results()`) into one function that uses a single template file.
``````
