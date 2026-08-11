---
title: Plotting in Python
label: plotting_in_python
abbreviations:
    
bibliography:
    .bib
---

```{important} Learning outcomes
After completing this section you should be able to:
- understand why data visualization is an essential part of data analysis. 
- choose an appropriate plot for different types of biological data. 
- create common plots using Seaborn. 
- customize plots by changing colours, labels, legends, and themes. 
- interpret and communicate patterns in data using figures. 
```

## Introduction

## What Makes a Good Plot?
Figures in science serve the purpose of visually supporting text or showing results. A good figure should communicate your results in a few seconds. It  should answer a question and it should be easy to read. It is best to keep your plots simple and to label everything, so the reader knows what they are looking at. 

## Matplotlib vs. Seaborn
In Python, there are two main plotting libraries: [`matplotlib`](https://matplotlib.org/) and [`seaborn`](https://seaborn.pydata.org/#). `matplotlib` is the underlying plotting library. However, its syntax is not always straight forward. `seaborn` is built on top of `matplotlib`, with a simpler syntax and better organization. Consequently, `seaborn` can quickly generate plots from [pandas DataFrames](#section_pandas_dataframe).

We can import both libraries as follows:
```{code-block} python
import matplotlib.pyplot as plt
```
```{code-block} python
import seaborn as sns
```

## Plotting Biological Data
When plotting any data, it is best to choose a type of plot based on the type of question we are answering with our plot. In [](#table_plot_type_question), some types of questions and their suggested plot type are listed.

:::{list-table} Type of plot to be used for type of question
:header-rows: 1
:label: table_plot_type_question
* - Type of question
  - Type of plot
* - Distribution
  - Histogram
* - Compare groups
  - Boxplot
* - Relationship
  - Scatter
* - Correlation
  - Heatmap
:::

We will illustrate some of these plots here using the [Palmer Penguins dataset](https://allisonhorst.github.io/palmerpenguins/). This dataset contains data on 344 penguins from the Palmer Archipelago in Antartica. It comprises three species (Adélie, Chinstrap, and Gentoo) and their body measurements including sex and body mass, across three islands.



### Loading the Data

### Boxplots and Scatterplots

### Adding Aesthetics

### Pairplot

## Common Mistakes

## Exercises
