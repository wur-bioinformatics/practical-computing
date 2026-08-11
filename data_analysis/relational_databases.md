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
:::{figure} img/relational_databases_foreign_keys.svg
Query and target in the BLAST result table are foreign keys to items in the protein table
:::

This is the power of relational databases. Because items are identified using a key, we can combine information regarding the same item from different databases ([](#))



## SQL

## Exercises
