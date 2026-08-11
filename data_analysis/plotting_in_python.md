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
:::{figure} img/histogram.png

:::
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
:::{figure} img/boxplot.png

:::
``````


### Scatterplots
To look at the relationship between variables, we can plot a scatterplot using the `scatterplot()` function from `seaborn` ([](#example_plotting_scatterplot)).

(example_plotting_scatterplot)=
``````{prf:example} Do Palmer penguins with longer bills also have deeper bills?
Let's plot the bill length and bill depth in a scatterplot:
```{code-block} python
sns.scatterplot(data=penguins, 
                x="bill_length_mm", 
                y="bill_depth_mm")
```
To show the plot:
```{code-block} python
plt.show()
```
:::{figure} img/scatterplot.png

:::
``````

### Adding Aesthetics
We have created some pretty basic plots in [](#example_plotting_histogram), [](#example_plotting_boxplot), and [](#example_plotting_scatterplot). Though, `seaborn` is known for its attractive graphics. In certain plots, we can specify the '`hue`' parameter, which maps a variable to a colour ([](#example_plotting_scatterplot_hue)). Additionally, we can specify the '`style`' parameter, which maps a variable to a marker shape or line style. Last, we can specify the '`size`' parameter, which maps a numerical variable to the size of the markers.

(example_plotting_scatterplot_hue)=
``````{prf:example} Do Palmer penguins with longer bills also have deeper bills?
Let's plot the bill length and bill depth in a scatterplot and colour by species:
```{code-block} python
sns.scatterplot(data=penguins, 
                x="bill_length_mm", 
                y="bill_depth_mm", 
                hue="species")
```
To show the plot:
```{code-block} python
plt.show()
```
:::{figure} img/scatterplot_hue.png

:::
``````

### Pairplot
Instead of creating separate plots for each variable comparison, we can create a pairplot using the `pairplot()` function from `seaborn` that shows the pairwise relationships between all variables ([](#example_plotting_pairplot)).

(example_plotting_pairplot)=
``````{prf:example} Pairwise relationships between Palmer Penguin measurements
Let's plot all pairwise relationships in a pairplot:
```{code-block} python
pair_plot = sns.pairplot(
    data=penguins,
    vars=[
        "bill_length_mm",
        "bill_depth_mm",
        "flipper_length_mm",
        "body_mass_g"
    ],
    hue="species",
    corner=True,
    diag_kind="hist"
)
```
To show the plot:
```{code-block} python
plt.show()
```
:::{figure} img/pairplot.png

:::

On the diagonal, we show the distribution of each variable with a histogram (`diag_kind="hist"`). 
``````

## Common Mistakes
Now that we have shown the basics of how to create pretty plots using `searborn`, here are some common mistakes to avoid:
- **Using rainbow colors or too many colors**: Makes it hard to read, because it is not always clear if you use a lot of colors which data point belongs to which group and can result in a misleading emphasis.
- **Using 3D effects for 2D data**: Plotting 2D data (two variables) with 3D effects is confusing because it distorts the perception.
- **Missing labels**: Not using labels makes it unclear what is shown, think of axis labels or the legend when data is colored by a group.
- **Using tiny font size**: Makes it difficult to read.
- **Truncating axes**: Exaggerates differences that are not true or relatistic.
- **Using too much decoration**: Distracting.
- **Using too much text**: Only use text for what is necessary to understand the plot (labels!).

## Exercises
For these exercises, we will work with a Jupyter Notebook on a remote server.

``````{exercise} Start the Jupyter Notebook on the remote server
We are using the same Jupyter Notebook as yesterday.

Similar to yesterday, follow the instructions on Brightspace "Starting a Jupyter Notebook on a remote server and connecting via an SSH tunnel".
``````

Again, the instructions are in the Jupyter Notebook.

### Matplotlib

``````{exercise} matplotlib basics
For this exercise, we continue with the DataFrame created [yesterday](#section_exc_pandas).

- Make a scatterplot of the *Iris* dataset petal length and width
- Make a histogram of the petal length
- Change the amount of bins used in the histogram
``````

### Seaborn
``````{exercise} Seaborn with Iris
For this exercise, we continue with the DataFrame created [yesterday](#section_exc_pandas).

- Make a scatterplot of the *Iris* dataset petal length and width and color by species
- Make a boxplot comparing sepal with among species
- Make a pairplot of all numerical values
``````

``````{exercise} Exploring a more realistic dataset: Palmer Penguins
We now switch to the **Palmer Penguins** dataset. It contains measurements from Adelie, Chinstrap, and Gentoo penguins, as well as categorical variables and some missing observations.

- Inspect the dataset
- Make a histogram of the distribution of body masses
- Color the histogram based on species
- Make a boxplot of flipper length by species
- Make a scatterplot of bill length and bill depth
- Remove the colouring and inspect the difference
- Make a scatter plot of flipper length and body mass
- Use a pairplot to inspect several relationships at once

``````

### Choosing the right plot
``````{exercise} Create a suitable Seaborn plot for each biological question
Create a suitable Seaborn plot for each question below. Add informative axis labels and a short title, and write one sentence describing the main pattern.

1. How is flipper length distributed?
2. Does body mass differ between male and female penguins?
3. Is body mass related to bill length, and does this differ among species?

:::{note} Remember that the purpose of a figure is to answer a question clearly
Adding more aesthetics does not automatically make a better plot.
:::
``````