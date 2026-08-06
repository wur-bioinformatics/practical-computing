---
title: NumPy and Pandas
label: numpy_pandas
abbreviations:
    
bibliography:
    .bib
---

```{important} Learning outcomes
After completing this section you should be able to:
- understand why NumPy exists
- understand what a dataframe is
- load biological datasets into pandas
- inspect and summarize data in a pandas dataframe
- select rows and columns from a pandas dataframe
- filter observations in a pandas dataframe
- calculate new variables in a pandas dataframe
- prepare data for visualization
```

## Introduction

(figure_python_data_science_ecosystem)=
:::{figure} img/python_data_science_ecosystem
:::

## NumPy
[Previously](#section_ds_lists), we have seen that Python has a list object, that serves the function of an array in other programming lanugages. However, lists are relatively slow to process. [NumPy](https://numpy.org/) introduced a data oject called an `ndarray` (**n**-**d**imensional **array**) that is fast and efficient to process and it included tools to manipulate and use mathematical operations on said arrays. 

NumPy is the foundation for many scientific Python libraries.

We can import NumPy as follows:
```{code-block} python
import numpy as np
```

### Lists vs. Arrays
A list in Python is an ordered collection of elements. Lists can contain different data types. On the other hand, NumPy arrays only contain numerical data. Just like lists, arrays can be multi-dimensional. We can create an array from a list ([](#example_array_from_list)).

(example_array_from_list)=
``````{prf:example} Create a NumPy array from a Python list
We can define a list:
```{code-block} python
lengths = [5.1, 4.9, 4.7, 4.6]
```
```{code-block} python
:class: no-copybutton
lengths
```
Will give the output:
```{code-block} python
:class: no-copybutton
[5.1, 4.9, 4.7, 4.6]
```

We can turn the list into an array:
```{code-block} python
lengths = np.array([5.1,4.9,4.7,4.6])
```
```{code-block} python
lengths
```
Will give the output:
```{code-block} python
:class: no-copybutton
array([5.1, 4.9, 4.7, 4.6])
```
Let's check the type:
```{code-block} python
type(lengths)
```
Will give the output:
```{code-block} python
:class: no-copybutton
<class 'numpy.ndarray'>
```
``````

One of the main benefits of arrays is that we can perform element-wise operations on an array, whereas this is not possible on lists ([](#example_list_vs_array_element_wise_operations))

(example_list_vs_array_element_wise_operations)=
``````{prf:example} Perform element-wise operations on a list and an array
Define a list and an array:
```{code-block} python
mylist = [1,2,3]
myarray = np.array([1,2,3])
```

If we try to perform element-wise operations on a list:
```{code-block} python
mylist * 3
```
Will give the output:
```{code-block} python
:class: no-copybutton
[1, 2, 3, 1, 2, 3, 1, 2, 3]
```
The result is a list with three times the elements in `mylist`.

Instead, if we perform element-wise operations on an array:
```{code-block} python
myarray * 3
```
Will give the output:
```{code-block} python
:class: no-copybutton
array([3, 6, 9])
```
The result is an array with the elements from `myarray` multiplied by `3`.
``````


### Multi-Dimensional Arrays
Arrays have dimensions and can be multi-dimensional ([](#figure_nd_arrays)). 

(figure_nd_arrays)=
:::{figure} img/multi-dimensional_arrays.png
n-dimensional arrays and their real-world applications
:::

*#! example?*

### Basic NumPy Operations
NumPy can perform operations on entire arrays. No loops are needed, making it very fast. We can perform element-wise operations on arrays such as multiplying the elements in an array with a number ([](#example_numpy_array_multiplication)) or adding a number to each element in the array ([](#example_numpy_array_addition)). Additionally, NumPy contains built-in functions for performing mathematical operations on arrays, such as taking the mean ([](#example_numpy_array_mean)), sum ([](#example_numpy_array_sum)) or max ([](#example_numpy_array_max)).


(example_numpy_array_multiplication)=
``````{prf:example} Perform element-wise multiplication on an array
Define an array:
```{code-block} python
x = np.array([1,2,3,4])
```

```{code-block} python
x * 2
```

Will give the output:
```{code-block} python
:class: no-copybutton
array([2, 4, 6, 8])
```
``````

(example_numpy_array_addition)=
``````{prf:example} Perform element-wise addition on an array
Define an array:
```{code-block} python
x = np.array([1,2,3,4])
```

```{code-block} python
x + 5
```

Will give the output:
```{code-block} python
:class: no-copybutton
array([6, 7, 8, 9])
```
``````


(example_numpy_array_mean)=
``````{prf:example} Taking the mean of an array
Define an array:
```{code-block} python
x = np.array([1,2,3,4])
```

```{code-block} python
x.mean()
```

Will give the output:
```{code-block} python
:class: no-copybutton
np.float64(2.5)
```
``````

(example_numpy_array_sum)=
``````{prf:example} Sum all the elements in an array
Define an array:
```{code-block} python
x = np.array([1,2,3,4])
```

```{code-block} python
x.sum()
```

Will give the output:
```{code-block} python
:class: no-copybutton
np.int64(10)
```
``````

(example_numpy_array_max)=
``````{prf:example} Taking the max element of an array
Define an array:
```{code-block} python
x = np.array([1,2,3,4])
```

```{code-block} python
x.max()
```

Will give the output:
```{code-block} python
:class: no-copybutton
np.int64(4)
```
``````

:::{note} NumPy has its own data types
As you might noticed in [](#example_numpy_array_mean), [](#example_numpy_array_sum), and [](#example_numpy_array_max), NumPy has its own data types (`np.float64`, `np.int64`). You don't need to know the difference between NumPy data types and standard Python data types and on the surface they behave similarly. If you are interested you can read about it [here](https://numpy.org/doc/stable/user/basics.types.html).
:::


## Pandas
NumPy is great for numerical data. Eventhough you can represent strings in a NumPy array, you cannot represent tables containing different data types. Biological data do not often contain only one data type, they are messy.

This is were the [pandas](https://pandas.pydata.org/) library comes in: it is a powerful data manipulation tool that introduces a data structure called a DataFrame that can handle tabular data with multiple data types.

We can import pandas as follows:
```{code-block} python
import pandas as pd
```


### Pandas DataFrame
A pandas DataFrame is a two-dimensional data structure that has labeled axes (rows and columns). You can think of it as a table that you would use in for example Excel.

We will illustrate pandas' functionalities using the [Iris dataset](wiki:iris_flower_data_set). It contains information on the sepal and petal length and width (in cm) of three Iris species (*Iris setosa*, *Iris versicolor*, and *Iris virginica*). In [](#figure_pandas_df_iris), the dataset is loaded into a DataFrame. We can see that columns have a name and rows have an index, though they can also be named. Each row is an observation, whereas each column is a property of the obersvation. Values of different columns can have different data types, but all values in one column must be of the same data type. 

(figure_pandas_df_iris)=
:::{figure} img/df_iris
The Iris dataset as a pandas DataFrame
:::


### Pandas Operations 
Apart from representing data in a DataFrame, we can perform operations on it to preprocess, clean and transform the data.

#### Loading Data
First, we need to load the data into a DataFrame. Pandas contains useful functions, such as `read_csv()` to read in tables from a URL([](#example_pandas_read_csv_url)). With `read_csv()` you can also read in tables stored on your machine. It also supports reading in tab-delimited files, then you will have to add `sep='\t'` (by default it is a comma). It has even more parameters that can be useful, the full documentation can be found [here](https://pandas.pydata.org/docs/reference/api/pandas.read_csv.html).

(example_pandas_read_csv_url)=
``````{prf:example} Read in a table into a DataFrame
We can read in a table from a repository by storing the URL in a string:
```{code-block} python
url = "https://raw.githubusercontent.com/mwaskom/seaborn-data/master/iris.csv"
```
Using `read_csv()` with the url as argument, we can read it into a DataFrame:
```{code-block} python
iris = pd.read_csv(url)
```
```{code-block} python
type(iris)
```
Will give the output:
```{code-block} python
:class: no-copybutton
<class 'pandas.DataFrame'>
```
``````

Alternatively, we can create DataFrames from other data structures as:
```{code-block} python
:class: no-copybutton
df = pd.DataFrame(data_structure)
```
where `data_structure` can be a list, Numpy arrays, or a dictionary of lists/arrays.


#### Exploring a Dataframe

#### Selecting Data from a Dataframe

#### Filtering Data from a Dataframe

#### Summary Statistics

#### Creating New Columns

#### Missing Values



### Subsection header 1.1

## Exercises
