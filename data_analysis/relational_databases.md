---
title: Relational Databases
label: relational_databases
abbreviations:
    RDBMS: Relational Database Management System
bibliography:
    .bib
---
```{important} Learning outcomes
After completing this section you should be able to:
- learning_outcome1
- learning_outcome2
```

## Introduction

## Relational Database Management System
A database management system (RDBMS) stores relational databases, provides access to databases and their tables, enforces data integrity, and is optimised for performance. 

Popular RDBMS are:
- Oracle Database
- MySQL
- Microsoft SQL Server
- PostgreSQL
- Microsoft Access
- SQLite

## Relational Database
In a relational database, data is organized in tables. Rows (or tuples, records) represent items, whereas columns represent attributes or fields. Rows can be inserted, removed, or selected based on their attributes using Structured Query Language or SQL. 

(example_relational_db_sql)=
``````{prf:example} Select records of which their description contains the word "caffeine"
Apply the following SQL query to a protein database:
```{code-block} sql
SELECT ID, description, sequence
FROM protein
WHERE description LIKE "%caffeine%";
```
Will give the output:
```{code-block} sql
:class: no-copybutton
+----------------------+---------------------------------------------------------------------+------------+
| ID                   | description                                                         | sequence   |
+----------------------+---------------------------------------------------------------------+------------+
| sp|Q8H0D3|CCS1_COFAR | Caffeine synthase 1 OS=Coffea arabica GN=CCS1 PE=1 SV=1             | MELQEVLHMN |
| sp|Q9AVK1|CS3_COFAR  | Probable caffeine synthase 3 OS=Coffea arabica GN=CS3 PE=2 SV=1     | MELQEVLHMN |
| sp|Q9AVL9|CS4_COFAR  | Probable caffeine synthase 4 OS=Coffea arabica GN=CS4 PE=2 SV=1     | MELQEVLHMN |
| sp|Q9FZN8|TCS1_CAMSI | Caffeine synthase 1 OS=Camellia sinensis GN=TCS1 PE=1 SV=1          | MELATAGKVN |
| sp|Q68CM3|TCS2_CAMSI | Probable caffeine synthase 2 OS=Camellia sinensis GN=TCS2 PE=2 SV=1 | MKEVKEALFM |
+----------------------+---------------------------------------------------------------------+------------+
```
``````

### Indices
With large tables, searching the complete table can take a long time. A specific index on one or more fields can dramatically speed up searches. Several kinds of indices are optimized for different kinds of queries (text, numeric, etc.)


### Keys
One attribute often is used to uniquely identify an item (row): the primary key. In a table with proteins the "protein ID" is a logical choice for the primary key.


### Relations
Primary keys are used to link different tables. In the "BLAST result" table, query and target are actually the IDs of an item in the protein table; query and target are so-called foreign keys ([](#figure_foreign_keys)).

(figure_foreign_keys)=
:::{figure} img/foreign_keys.svg
Query and target in the BLAST result table are foreign keys to items in the protein table
:::

This is the power of relational databases. Because items are identified using a key, we can combine information regarding the same item from different databases ([](#figure_relational_databases_example)).

(figure_relational_databases_example)=
:::{figure} img/relational_databases_example.svg
Data regarding the same protein can be stored across multiple databases (colors) and connected by a key
:::

## SQL and SQLite
SQLite has two types of commands:
- SQL commands to create, modify and filter tables, these are generally capitalized and have to be closed with a semicolon `;`
- SQLite commands, which start with a dot and should not be closed with a `;`

Creating a table in SQL uses the command `CREATE TABLE`, which can be a bit complicated to write. Fortunately, SQLite has a convenient `.import` command that directly creates a table and loads a data file into it. By default, this command uses the column headers of the data file to create a table with the same columns. The data type of all columns will always be `TEXT`, which limits how we can filter rows from the table on numeric values. Some columns actually contain `INTEGER` or `REAL` values (floating point values) instead.


## Exercises
In this exercise we will explore the use of a relational database, first through the SQLite command line (Today) and then from Python (Monday), and finally by building a website (Tuesday). 

As data we will use the results of searching for the human homologs of the plant proteins in the SwissProt database (determined with BLAST) that we have looked at before. *#! when?*

We will work on the server.

### SQLite
``````{exercise} Preparation
Make sure to create a new directory `~/exercises/blast_browser` and copy ([`cp`](#cp_section)) or link (`ln -s`) the `plantsvshuman_outmft6.csv` and the `plants.fasta` files in that directory. 

The first contains `blastp` matching plant proteins with human proteins, the second contains plant protein sequences in FASTA format (you can also find these files in `/mnt/local_scratch/BIF21806`)
``````
#### Creating an SQL Table
``````{exercise} Creating your first table
We will start with creating a table called `blast_results` and load the contents of `plantsvshuman_outmft6.csv` into it.

We will first use the `.import` command to have it generate the `CREATE TABLE` command for us, and then modify this to set the appropriate column data types.

**Run the `sqlite3` command in your terminal to start the SQLite shell.**
```{code-block} bash
sqlite3
```
You should see something like this:
```{code-block} bash
:class: no-copybutton
user001@bork:~/exercises/blast_browser$ sqlite3
SQLite version 3.41.2 2023-03-22 11:56:21
Enter ".help" for usage hints.
Connected to a transient in-memory database.
Use ".open FILENAME" to reopen on a persistent database.
sqlite>
```
To see the available SQLite commands, type: 
```{code-block} sql
.help
```

To get help for a specific command, try (for instance): 
```{code-block} sql
.help .import
```

Before we can import the data, we first should set which column separators our file has to make sure the import works. For the blast results, the columns are tab-separated, so please run (`\t` is the tab character):
```{code-block} sql
.separator \t
```
Now you can import the file into a new SQLite table with:
```{code-block} sql
.import plantsvshuman_outmft6.csv blast_results
```

This creates a table called `blast_results` and loads the contents of the file into it.

Run the .tables command to check that it worked.
```{code-block} sql
.tables
```
To see the rows in the table, you can use an SQL command called `SELECT`:
```{code-block} sql
SELECT * FROM blast_results LIMIT 5;
```
This should show the first five rows, without the column headers. 

To see the headers, run this SQLite command:
```{code-block} sql
.header on
```
and run the `SELECT` SQL command again to see the headers.


Now, check the `CREATE TABLE` statement that was used for the `blast_results` table using the SQLite command:
```{code-block} sql
.schema
```
To be able to edit this, copy the complete `CREATE TABLE `command (including the closing `;`) into a text editor and change the column names to:\
`query, target, perc_ident, align_length, mismatches, gap_opens, q_start, q_end, t_start, t_end, evalue, bit_score`. \
Also change the data type where appropriate from `TEXT` to `INTEGER` or `REAL`. To do this, check the values in the .csv file, or use the column type annotation on [this](https://scikit.bio/docs/latest/generated/skbio.io.format.blast6.html) page.


Now we want to recreate the `blast_results` table with the proper column names and data types, so first delete the current table by running the SQL command:
```{code-block} sql
DROP TABLE IF EXISTS blast_results;
```
Recreate the table by running your modified `CREATE TABLE` command.

:::{tip} Tip
Make sure to always include the semicolon at the end of an SQL command. SQLite will only process your SQL command when it encounters the` ;` symbol. The benefit of this is that you can spread the command over multiple lines. 
:::

Check that the create command worked: 
```{code-block} sql
.schema
```
You can rerun the `SELECT` command as well to see that the table is empty.

Now rerun the `.import` command (with arguments) like before. Because the `blast_results` table already exists, it will not create a new table but use the existing one with the updated column names and data types. If the import succeeded, you can view the contents of the table with this `SELECT` statement:
```{code-block} sql
SELECT query FROM blast_results LIMIT 5;
```
This shows query column for the top five rows and should look like this:
```{code-block} sql
query
Query_label
sp|P48347|14310_ARATH
sp|P93207|14310_SOLLC
sp|Q9S9Z8|14311_ARATH
sp|Q9C5W6|14312_ARATH
```

This looks good, until you realize that it there are two headers, the old one and the new one. What happened is that the `.import` command noticed that the table was already created and did not use the first row for column names. Instead, it put all rows in the file into the table. To remove this first row, use this SQL command:
```{code-block} sql
DELETE FROM blast_results WHERE query = "Query_label";
```
:::{note} Note
In SQL we use `=` for equals, instead of `==` in Python

:::

Congratulations, you have created your first SQL table. 🎉

Save the table to a database file using:
```{code-block} sql
.save plants_vs_humans.db
```
``````


``````{exercise} Searching the data in the database
Now you have the data in the table, you can use the `SELECT` command to analyse it. Try this to view the first 10 lines of the table:
```{code-block} sql
SELECT * FROM blast_results LIMIT 10;
```

The asterisk symbol `*` here indicates that we want to see all columns from the `blast_results` table. 

If you have difficulty telling where one column ends and another starts, you can change the column separator with this command:
```{code-block} sql
.separator " || "
```
(or use another separator string). 

Alternatively, you can change the output mode to `quote`, `list`, `line` and even `html`:
```{code-block} sql
.help .mode
```
Set the mode to `quote`:
```{code-block} sql
.mode quote
```
To only print the query and target columns, run this:
```{code-block} sql
SELECT query, target FROM blast_results LIMIT 10;
```
Counting the number of rows ("records" in SQL) works like this:
```{code-block} sql
SELECT COUNT(*) FROM blast_results;
```
Get the maximum E-value:
```{code-block} sql
SELECT MAX(evalue) FROM blast_results;
```
(this only works if you set the right data type for the `evalue` column)

**What do you think the E-value cut-off was set to in the BLAST run?**

Also try:
```{code-block} sql
SELECT evalue FROM blast_results ORDER BY evalue DESC LIMIT 10;
```
**What do you think this does?**

To filter the table to get only the records that meet a certain condition, you can use the `WHERE` keyword:
```{code-block} sql
SELECT * FROM blast_results WHERE evalue = 0;
```
This only shows records where the evalue column has the value `0`

Use a `SELECT` query to find the hits with a percentage identify above 98% and take a moment to be amazed that these proteins changed so little in more than a billion years of evolution.

You can combine two conditions using the `AND` keyword:
```{code-block} sql
SELECT * FROM blast_results WHERE evalue = 0 AND perc_ident < 30;
```

**Now think of a `SELECT` query that finds the records where the query and target length are the same (so not the start or the end, but the lengths)**. You have done a similar task using Python before.


The `blastp` analysis was run with a limit of only one target per query, but the same target can be reported for multiple queries. This is for instance the case for the protein "IRAK4_HUMAN, Interleukin-1 receptor-associated kinase 4". To find all hits for this protein use:
```{code-block} sql
SELECT * FROM blast_results WHERE target LIKE '%IRAK4_HUMAN';
```

The `LIKE` keyword accepts wildcards in a text query. The wildcard `%` represents zero or more characters (similar to the `*` in the shell).

**Now, compare the results from these two queries and try to explain the difference:**
```{code-block} sql
SELECT COUNT(query) FROM blast_results WHERE target LIKE '%IRAK4_HUMAN';
```
```{code-block} sql
SELECT COUNT(DISTINCT query) FROM blast_results WHERE target LIKE '%IRAK4_HUMAN';
```
This query might help:
```{code-block} sql
SELECT * FROM blast_results WHERE query LIKE '%LRKS2_ARATH';
```
``````


``````{exercise} Creating another table
Let's create table with protein information:
```{code-block} sql
CREATE TABLE plant_proteins (
"ID" TEXT,
"description" TEXT,
"sequence" TEXT
);
```

No `INTEGER` or `REAL` data types this time. 

To load the data, we need to convert the `plant_proteins.fasta` file to a comma-separated file, with all information per sequence (ID, description and sequence) in one row. Because the description of the protein can contain commas, we have to put quotes around the fields.

A python script to do this is shown below. Check carefully where it expects the input and how it produces the output.

```{code-block} python
:filename: fasta2csv.py
#!/usr/bin/env python
# fasta2csv script
from sys import argv

FASTA_file = open(argv[1])

ID_line = ""
sequence = ""

for line in FASTA_file:
    line = line.strip()

    if line[0] == '>':
        if ID_line != "":
            (identifier,description) = ID_line.split(' ',1)
            print('"%s","%s","%s"'%(identifier,description,sequence))
            ID_line = ""
            sequence = ""
        ID_line = line[1:]
    else:
        sequence += line

if ID_line != "":
    (identifier, description) = ID_line.split(' ', 1)
    print('"%s","%s","%s"' % (identifier, description, sequence))

FASTA_file.close()
#end script
```
(also in `/mnt/local_scratch/BIF21806/`)

Run the script on Linux (it is a Python script, so do not use SQLite for this 😊) and write the result to a file called `plant_proteins.csv`.

:::{tip} Tip
Redirect the output with `>`
:::

Check that the file indeed has lines with comma separated fields.


Now back to the SQLite shell. 

If you close it, you can reopen it directly with the right database using: 
```{code-block} bash
sqlite3 plants_vs_humans.db
```

The data are now comma separated, so before we can import the data, set the mode to csv:
```{code-block} sql
.mode csv
```

Load the data into the right table using:
```{code-block} sql
.import plant_proteins.csv plant_proteins
```


**Check the result using a `SELECT` command on the table and check that you have the right number of rows/records.**
``````

#### Joining Two SQL Tables
``````{exercise} Joining tables
Now we have two tables in the database, we can do a `SELECT` query that combines information from the two tables. For this we have to use the SQL statement `INNER JOIN` and specify which column in the first table corresponds to which table in the second table. In our case the `query` column of the `blast_results` table contains the plant protein identifiers and these correspond to the `ID` column in the `plant_proteins` table.

Now you can add the description from the `plant_proteins` table to the matching `query` and `target` from the `blast_results` table:
```{code-block} sql
SELECT query, target, evalue, description
FROM blast_results
INNER JOIN plant_proteins
ON blast_results.query = plant_proteins.ID;
```
``````



###  Accessing SQLite from Python
Last Friday, you created the `plants_vs_humans` SQLite3 Database containing results of searching for the human homologs of the plant proteins in the SwissProt database (determined with BLAST).

Here, we will create Python functions to query the `plants_vs_humans` SQLite3 database. This code will be used tomorrow to build a website via which a user can select a human protein ID and retrieve all BLAST matches for that protein with plant proteins.

``````{exercise} Start the W5D1 on the remote server
Copy this notebook in your `exercises/blast_browser` folder on bork and run it through an `ssh` tunnel like before ("Starting a Jupyter Notebook on a remote server and connecting via an SSH tunnel").
``````

Like before, the Jupyter Notebook contains all instructions.

We will use the `sqlite3` module. Online documentation can be found [here](https://docs.python.org/3/library/sqlite3.html).

#### Build a Module Containing Functions to Access an SQLite3 Database

::::{exercise} Create a function that returns a list of all targets from the `blast_results` table
Given the `get_targets()` function:
- fix the SQL statement (test this with SQLite3)
- change the code in the `for loop` to process the result of the query to fill the `targets` list
::::



::::{exercise} Create a function that takes a target as input and returns all matching rows from the `blast_results` table

In addition to the `query` and `target` fields, we also want to return the `evalue` and the `description` for the `target`. That information can be retrieved by linking the `blast_results` table with the `plant_proteins` table, using `INNER JOIN` (see also Fridays exercise). 

The function takes two arguments, the target identifier and an e_value threshold. For the latter we provide a default, so it can be left out when calling the function. 



Given the `get_rows_for_target()` function:
- Write the SQL statement. It is advised to first build the SQL statement using SQLite before testing it out in the Jupyter Notebook.
- Write Python code to fill the `rows` list
::::

::::{exercise} Create a Python file called `db_functions.py`
- Add the shebang line and the import statement for the `sqlite3` module:
  ```{code-block} python
  :filename: db_functions.py
  #!/usr/bin/env python3
  import sqlite3
  ```
- Save the file in the same directory as the W5D1 Jupyter Notebook
- Import the module and use its functions in the Jupyter Notebook
::::

#### Extensions
If you have time left, you can extend the functions with more features using the challenges.

::::{exercise} Challenge 1
Modify the `get_rows_for_target()` function to also filter for the provided e-value threshold, so that only rows are returned where the evalue column is `<=` the provided threshold
::::

::::{exercise} Challenge 2
Make the `get_rows_for_target()` function work for only the last part of the target ID, so instead of having to use the full `"sp|P62258|1433E_HUMAN"`, it should also work for `"1433E_HUMAN"` 

:::{tip} Tip
Look at the SQL `LIKE` keyword
:::
::::

::::{exercise} Challenge 3
Complete the `get_queries_sequence_for_target_seq()` function to take a (human) target as input and create a FASTA file with the sequences for the matching plant proteins. 

Additonal challenge: print only 60 nucleotides per line.
::::