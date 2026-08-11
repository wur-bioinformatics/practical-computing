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
First, we have to load the data. The Palmer Penguins dataset is already included in `seaborn`, so we can use the function `load_dataset()` to load it into a pandas DataFrame ([](#example_plotting_load_data))

(example_plotting_load_data)=
``````{prf:example} Load the Palmer Penguins data
```{code-block} python
penguins = sns.load_dataset("penguins")
```

To get a quick overview what is inside, use .head():
```{code-block} python
penguins.head()
```
Will give the output:
```{code-block} python
:class: no-copybutton
  species     island  bill_length_mm  bill_depth_mm  flipper_length_mm  body_mass_g     sex
0  Adelie  Torgersen            39.1           18.7              181.0       3750.0    Male
1  Adelie  Torgersen            39.5           17.4              186.0       3800.0  Female
2  Adelie  Torgersen            40.3           18.0              195.0       3250.0  Female
3  Adelie  Torgersen             NaN            NaN                NaN          NaN     NaN
4  Adelie  Torgersen            36.7           19.3              193.0       3450.0  Female
```
``````

### Histogram
To look at the distribution of data, we can use the `histplot()` function from `seaborn` ([](#example_plotting_histogram)).

(example_plotting_histogram)=
``````{prf:example} How are the body masses distributed?
Let's plot the body masses of all penguins in a histogram:
```{code-block} python
sns.histplot(data=penguins, x="body_mass_g", bins=20)
```
To show the plot:
```{code-block} python
plt.show()
```
![Distribution of body mass of Palmer Penguins](image.png)
``````

### Boxplot
To compare groups, we can make a boxplot using the `boxplot()` function from `seaborn` ([](#example_plotting_boxplot)).

(example_plotting_boxplot)=
``````{prf:example} Are Gentoo penguins heavier than Adelie and Chinstrap penguins?
Let's plot the body masses per penguin species in a boxplot:
```{code-block} python
sns.boxplot(data=penguins, x="species", y="body_mass_g")
```
To show the plot:
```{code-block} python
plt.show()
```
![Boxplot of body mass per Palmer Penguin species](image-1.png)
``````


### Scatterplots
To look at the relationship between variables, we can plot a scatterplot using the `scatterplot()` function from `seaborn` ([](#example_plotting_scatterplot)).

(example_plotting_scatterplot)=
``````{prf:example} Do Palmer penguins with longer bills also have deeper bills?
Let's plot the bill length and bill depth in a scatterplot:
```{code-block} python
sns.scatterplot(data=penguins, x="bill_length_mm", y="bill_depth_mm")
```
To show the plot:
```{code-block} python
plt.show()
```
![Scatterplot of bill length and bill depth of Palmer Penguins](image-2.png)
``````

### Adding Aesthetics
We have created some pretty basic plots in [](#example_plotting_histogram), [](#example_plotting_boxplot), and [](#example_plotting_scatterplot). Though, `seaborn` is known for its attractive graphics. In certain plots, we can specify the '`hue`' parameter, which maps a variable to a colour ([](#example_plotting_scatterplot_hue)). Additionally, we can specify the '`style`' parameter, which maps a variable to a marker shape or line style. Last, we can specify the '`size`' parameter, which maps a numerical variable to the size of the markers.

(example_plotting_scatterplot_hue)=
``````{prf:example} Do Palmer penguins with longer bills also have deeper bills?
Let's plot the bill length and bill depth in a scatterplot and colour by species:
```{code-block} python
sns.scatterplot(data=penguins, x="bill_length_mm", y="bill_depth_mm", hue="species")
```
To show the plot:
```{code-block} python
plt.show()
```
![Scatterplot of bill length and bill depth of Palmer Penguins coloured by species](image-3.png)
``````

### Pairplot

## Common Mistakes

## Exercises
