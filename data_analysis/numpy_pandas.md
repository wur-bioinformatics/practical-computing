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
:::{figure} img/python_data_science_ecosystem.png
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

(section_pandas_dataframe)=
### Pandas DataFrame
A pandas DataFrame is a two-dimensional data structure that has labeled axes (rows and columns). You can think of it as a table that you would use in for example Excel.

We will illustrate pandas' functionalities using the [Iris dataset](wiki:iris_flower_data_set). It contains information on the sepal and petal length and width (in cm) of three Iris species (*Iris setosa*, *Iris versicolor*, and *Iris virginica*). In [](#figure_pandas_df_iris), the dataset is loaded into a DataFrame. We can see that columns have a name and rows have an index, though they can also be named. Each row is an observation, whereas each column is a property of the obersvation. Values of different columns can have different data types, but all values in one column must be of the same data type. 

(figure_pandas_df_iris)=
:::{figure} img/df_iris.png
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
where `data_structure` can be a list, a NumPy array, or a dictionary of lists/NumPy arrays.


#### Exploring a Dataframe
Now that we have read in the table into a DataFrame, let's do some basic exploration of what is contained inside. The DataFrame is an object and on it we can call some explorative methods. We can use `.head()` and `.tail()` to show the first and last five (by default) rows, respectively ([](#example_df_head), [](#example_df_tail)). 


(example_df_head)=
``````{prf:example} Show the first 5 lines of a DataFrame
Assuming we have loaded in the Iris dataset into a DataFrame as in [](#example_pandas_read_csv_url), we can view the first 5 lines of the DataFrame with:
```{code-block} python
iris.head()
```
Will give the output:
```{code-block} python
:class: no-copybutton
   sepal_length  sepal_width  petal_length  petal_width species
0           5.1          3.5           1.4          0.2  setosa
1           4.9          3.0           1.4          0.2  setosa
2           4.7          3.2           1.3          0.2  setosa
3           4.6          3.1           1.5          0.2  setosa
4           5.0          3.6           1.4          0.2  setosa
```
``````

(example_df_tail)=
``````{prf:example} Show the last 5 lines of a DataFrame
Assuming we have loaded in the Iris dataset into a DataFrame as in [](#example_pandas_read_csv_url), we can view the last 5 lines of the DataFrame with:
```{code-block} python
iris.tail()
```
Will give the output:
```{code-block} python
:class: no-copybutton
     sepal_length  sepal_width  petal_length  petal_width    species
145           6.7          3.0           5.2          2.3  virginica
146           6.3          2.5           5.0          1.9  virginica
147           6.5          3.0           5.2          2.0  virginica
148           6.2          3.4           5.4          2.3  virginica
149           5.9          3.0           5.1          1.8  virginica
```
``````

We can also view properties of the Dataframe. To show the number of rows and columns we can use `.shape` ([](#example_df_shape)) and to list all column names we can use `.columns` ([](#example_df_columns)).


(example_df_shape)=
``````{prf:example} Show the number of rows and columns of a DataFrame
Assuming we have loaded in the Iris dataset into a DataFrame as in [](#example_pandas_read_csv_url), we can view the number of rows and columns of the DataFrame with:
```{code-block} python
iris.shape
```
Will give the output:
```{code-block} python
:class: no-copybutton
(150, 5)
```
The first element of the tuple are the rows and the second are the columns.
``````

(example_df_columns)=
``````{prf:example} List the column names of a DataFrame
Assuming you have loaded in the Iris dataset into a DataFrame as in [](#example_pandas_read_csv_url), we can view the column names of the DataFrame with:
```{code-block} python
iris.columns
```
Will give the output:
```{code-block} python
:class: no-copybutton
Index(['sepal_length', 'sepal_width', 'petal_length', 'petal_width',
       'species'],
      dtype='str')
```
It shows the column names and what data type the column names are.
``````

To produce a summary of the DataFrame, we can use the method `.info()` ([](#example_df_info)). This gives information on the data types in the columns and whether there are missing values. To produce summary statistics of numerical columns, we can use the `.describe()` method ([](#example_df_describe)).

(example_df_info)=
``````{prf:example} Show the summary of a DataFrame
Assuming we have loaded in the Iris dataset into a DataFrame as in [](#example_pandas_read_csv_url), we can view the summary of the DataFrame with:
```{code-block} python
iris.info()
```
Will give the output:
```{code-block} python
:class: no-copybutton
<class 'pandas.DataFrame'>
RangeIndex: 150 entries, 0 to 149
Data columns (total 5 columns):
 #   Column        Non-Null Count  Dtype
---  ------        --------------  -----
 0   sepal_length  150 non-null    float64
 1   sepal_width   150 non-null    float64
 2   petal_length  150 non-null    float64
 3   petal_width   150 non-null    float64
 4   species       150 non-null    str
dtypes: float64(4), str(1)
memory usage: 6.0 KB
```
``````

(example_df_describe)=
``````{prf:example} Show the summary statistics of a DataFrame
Assuming we have loaded in the Iris dataset into a DataFrame as in [](#example_pandas_read_csv_url), we can view the summary statistics of the DataFrame with:
```{code-block} python
iris.describe()
```
Will give the output:
```{code-block} python
:class: no-copybutton
       sepal_length  sepal_width  petal_length  petal_width
count    150.000000   150.000000    150.000000   150.000000
mean       5.843333     3.057333      3.758000     1.199333
std        0.828066     0.435866      1.765298     0.762238
min        4.300000     2.000000      1.000000     0.100000
25%        5.100000     2.800000      1.600000     0.300000
50%        5.800000     3.000000      4.350000     1.300000
75%        6.400000     3.300000      5.100000     1.800000
max        7.900000     4.400000      6.900000     2.500000
```
``````


#### Selecting Data from a Dataframe
We can select data from a DataFrame by indexing it with the column name of one column ([](#example_df_index_one_col)) or a list of column names for multiple columns ([](#example_df_index_multiple_col)).

(example_df_index_one_col)=
``````{prf:example} Select one column of a DataFrame
Assuming we have loaded in the Iris dataset into a DataFrame as in [](#example_pandas_read_csv_url), we select a column of the DataFrame with:
```{code-block} python
iris["species"]
```
Will give the output:
```{code-block} python
:class: no-copybutton
0         setosa
1         setosa
2         setosa
3         setosa
4         setosa
         ...
145    virginica
146    virginica
147    virginica
148    virginica
149    virginica
Name: species, Length: 150, dtype: str
```
``````

(example_df_index_multiple_col)=
``````{prf:example} Select multiple columns of a DataFrame
Assuming we have loaded in the Iris dataset into a DataFrame as in [](#example_pandas_read_csv_url), we select multiple columns of the DataFrame with:
```{code-block} python
iris[["species", "petal_length"]]
```
Will give the output:
```{code-block} python
:class: no-copybutton
       species  petal_length
0       setosa           1.4
1       setosa           1.4
2       setosa           1.3
3       setosa           1.5
4       setosa           1.4
..         ...           ...
145  virginica           5.2
146  virginica           5.0
147  virginica           5.2
148  virginica           5.4
149  virginica           5.1

[150 rows x 2 columns]
```
``````

To select the rows of a DataFrame, we can use the `.iloc` property. It allows us to use integers to index the DataFrame, similar to how we would [index or slice a list](#section_list_indexing_and_slicing). Instead of elements in lists, we select rows in an a DataFrame. To only select one row, we can index this property with the DataFrame index ([](#example_df_index_one_row)). To select multiple rows, we can provide it with a slice ([](#example_df_index_multiple_rows)).

(example_df_index_one_row)=
``````{prf:example} Select one row of a DataFrame
Assuming we have loaded in the Iris dataset into a DataFrame as in [](#example_pandas_read_csv_url), we select a row of the DataFrame with:
```{code-block} python
iris.iloc[0]
```
Will give the output:
```{code-block} python
:class: no-copybutton
sepal_length       5.1
sepal_width        3.5
petal_length       1.4
petal_width        0.2
species         setosa
Name: 0, dtype: object
```
This is the first row of the DataFrame, as we used `0` for the index
``````

(example_df_index_multiple_rows)=
``````{prf:example} Select multiple rows of a DataFrame (slicing)
Assuming we have loaded in the Iris dataset into a DataFrame as in [](#example_pandas_read_csv_url), we select multiple rows of the DataFrame with:
```{code-block} python
iris.iloc[0:5]
```
Will give the output:
```{code-block} python
:class: no-copybutton
   sepal_length  sepal_width  petal_length  petal_width species
0           5.1          3.5           1.4          0.2  setosa
1           4.9          3.0           1.4          0.2  setosa
2           4.7          3.2           1.3          0.2  setosa
3           4.6          3.1           1.5          0.2  setosa
4           5.0          3.6           1.4          0.2  setosa
```
These are the first five rows of the DataFrame.
``````

#### Filtering Data from a Dataframe
We cannot only select data from a DataFrame, we can also filter the observations while selecting. We do so by using [comparison operators](#comparison_operators_section) and [Boolean operators](#boolean_operators_section) when indexing on the DataFrame and using the result of that as an index again. This is illustrated in [](#example_df_filter_obsv_1) and [](#example_df_filter_obsv_2). The result of the comparison is actually a pandas Series (1-column DataFrame) with Boolean values: `True` when the comparison for that cell is true and `False` when false. When we use the pandas Series to index the DataFrame, we will only maintain the rows for which the series holds `True`.


(example_df_filter_obsv_1)=
``````{prf:example} Filter observations based on species 
Assuming we have loaded in the Iris dataset into a DataFrame as in [](#example_pandas_read_csv_url), we filter the DataFrame to only select observations from *setosa* with:
```{code-block} python
iris[iris["species"]=="setosa"]
```
Will give the output:
```{code-block} python
:class: no-copybutton
    sepal_length  sepal_width  petal_length  petal_width species
0            5.1          3.5           1.4          0.2  setosa
1            4.9          3.0           1.4          0.2  setosa
2            4.7          3.2           1.3          0.2  setosa
3            4.6          3.1           1.5          0.2  setosa
4            5.0          3.6           1.4          0.2  setosa
5            5.4          3.9           1.7          0.4  setosa
6            4.6          3.4           1.4          0.3  setosa
7            5.0          3.4           1.5          0.2  setosa
8            4.4          2.9           1.4          0.2  setosa
9            4.9          3.1           1.5          0.1  setosa
10           5.4          3.7           1.5          0.2  setosa
11           4.8          3.4           1.6          0.2  setosa
12           4.8          3.0           1.4          0.1  setosa
13           4.3          3.0           1.1          0.1  setosa
14           5.8          4.0           1.2          0.2  setosa
15           5.7          4.4           1.5          0.4  setosa
16           5.4          3.9           1.3          0.4  setosa
17           5.1          3.5           1.4          0.3  setosa
18           5.7          3.8           1.7          0.3  setosa
19           5.1          3.8           1.5          0.3  setosa
20           5.4          3.4           1.7          0.2  setosa
21           5.1          3.7           1.5          0.4  setosa
22           4.6          3.6           1.0          0.2  setosa
23           5.1          3.3           1.7          0.5  setosa
24           4.8          3.4           1.9          0.2  setosa
25           5.0          3.0           1.6          0.2  setosa
26           5.0          3.4           1.6          0.4  setosa
27           5.2          3.5           1.5          0.2  setosa
28           5.2          3.4           1.4          0.2  setosa
29           4.7          3.2           1.6          0.2  setosa
30           4.8          3.1           1.6          0.2  setosa
31           5.4          3.4           1.5          0.4  setosa
32           5.2          4.1           1.5          0.1  setosa
33           5.5          4.2           1.4          0.2  setosa
34           4.9          3.1           1.5          0.2  setosa
35           5.0          3.2           1.2          0.2  setosa
36           5.5          3.5           1.3          0.2  setosa
37           4.9          3.6           1.4          0.1  setosa
38           4.4          3.0           1.3          0.2  setosa
39           5.1          3.4           1.5          0.2  setosa
40           5.0          3.5           1.3          0.3  setosa
41           4.5          2.3           1.3          0.3  setosa
42           4.4          3.2           1.3          0.2  setosa
43           5.0          3.5           1.6          0.6  setosa
44           5.1          3.8           1.9          0.4  setosa
45           4.8          3.0           1.4          0.3  setosa
46           5.1          3.8           1.6          0.2  setosa
47           4.6          3.2           1.4          0.2  setosa
48           5.3          3.7           1.5          0.2  setosa
49           5.0          3.3           1.4          0.2  setosa
```
``````

(example_df_filter_obsv_2)=
``````{prf:example} Filter observations based on numerical value
Assuming we have loaded in the Iris dataset into a DataFrame as in [](#example_pandas_read_csv_url), we filter the DataFrame to only select observations with a petal length larger than 5 with:
```{code-block} python
iris[iris["petal_length"] > 5]
```
Will give the output:
```{code-block} python
:class: no-copybutton
    sepal_length  sepal_width  petal_length  petal_width     species
83            6.0          2.7           5.1          1.6  versicolor
100           6.3          3.3           6.0          2.5   virginica
101           5.8          2.7           5.1          1.9   virginica
102           7.1          3.0           5.9          2.1   virginica
103           6.3          2.9           5.6          1.8   virginica
104           6.5          3.0           5.8          2.2   virginica
105           7.6          3.0           6.6          2.1   virginica
107           7.3          2.9           6.3          1.8   virginica
108           6.7          2.5           5.8          1.8   virginica
109           7.2          3.6           6.1          2.5   virginica
110           6.5          3.2           5.1          2.0   virginica
111           6.4          2.7           5.3          1.9   virginica
112           6.8          3.0           5.5          2.1   virginica
114           5.8          2.8           5.1          2.4   virginica
115           6.4          3.2           5.3          2.3   virginica
116           6.5          3.0           5.5          1.8   virginica
117           7.7          3.8           6.7          2.2   virginica
118           7.7          2.6           6.9          2.3   virginica
120           6.9          3.2           5.7          2.3   virginica
122           7.7          2.8           6.7          2.0   virginica
124           6.7          3.3           5.7          2.1   virginica
125           7.2          3.2           6.0          1.8   virginica
128           6.4          2.8           5.6          2.1   virginica
129           7.2          3.0           5.8          1.6   virginica
130           7.4          2.8           6.1          1.9   virginica
131           7.9          3.8           6.4          2.0   virginica
132           6.4          2.8           5.6          2.2   virginica
133           6.3          2.8           5.1          1.5   virginica
134           6.1          2.6           5.6          1.4   virginica
135           7.7          3.0           6.1          2.3   virginica
136           6.3          3.4           5.6          2.4   virginica
137           6.4          3.1           5.5          1.8   virginica
139           6.9          3.1           5.4          2.1   virginica
140           6.7          3.1           5.6          2.4   virginica
141           6.9          3.1           5.1          2.3   virginica
142           5.8          2.7           5.1          1.9   virginica
143           6.8          3.2           5.9          2.3   virginica
144           6.7          3.3           5.7          2.5   virginica
145           6.7          3.0           5.2          2.3   virginica
147           6.5          3.0           5.2          2.0   virginica
148           6.2          3.4           5.4          2.3   virginica
149           5.9          3.0           5.1          1.8   virginica
```
``````

#### Summary Statistics
We saw [before](#example_df_describe) how to obtain the full summary statistics table from a DataFrame. To get individual summary statistics of a DataFrame such as the mean or standard deviation, we can call on those methods ([](#example_df_mean), [](#example_df_std)). 

(example_df_mean)=
``````{prf:example} Get the mean of the numeric columns in a DataFrame
Assuming we have loaded in the Iris dataset into a DataFrame as in [](#example_pandas_read_csv_url), we can get the mean of the numeric columns in the DataFrame with:
```{code-block} python
iris.mean(numeric_only=True)
```
Will give the output:
```{code-block} python
:class: no-copybutton
sepal_length    5.843333
sepal_width     3.057333
petal_length    3.758000
petal_width     1.199333
dtype: float64
```
``````

(example_df_std)=
``````{prf:example} Get the standard deviation of the numeric columns in a DataFrame
Assuming we have loaded in the Iris dataset into a DataFrame as in [](#example_pandas_read_csv_url), we can get the standard deviation of the numeric columns in the DataFrame with:
```{code-block} python
iris.std(numeric_only=True)
```
Will give the output:
```{code-block} python
:class: no-copybutton
   sepal_length  sepal_width  petal_length  petal_width species
0           5.1          3.5           1.4          0.2  setosa
1           4.9          3.0           1.4          0.2  setosa
2           4.7          3.2           1.3          0.2  setosa
3           4.6          3.1           1.5          0.2  setosa
4           5.0          3.6           1.4          0.2  setosa
```
``````


To obtain the individual summary statistics of each Iris species, we can use the method `.groupby()` ([](#example_df_groupby_mean)). Grouping allows us to split the data into categories, perform the same calculation for each category, and combine the results again. 


(example_df_groupby_mean)=
``````{prf:example} Get the mean of the numeric columns for each species in the Iris DataFrame
Assuming we have loaded in the Iris dataset into a DataFrame as in [](#example_pandas_read_csv_url), we can get the mean of the numeric columns for each species in the Iris DataFrame with:
```{code-block} python
iris.groupby("species").mean()
```
Will give the output:
```{code-block} python
:class: no-copybutton
            sepal_length  sepal_width  petal_length  petal_width
species
setosa             5.006        3.428         1.462        0.246
versicolor         5.936        2.770         4.260        1.326
virginica          6.588        2.974         5.552        2.026
```
We do not have to specify `numeric_only=True`, because we are calculating the mean on only numerical columns already. 
``````

#### Creating New Columns
Since DataFrames are mutable, we can create columns. This is especially useful if we want to perform calculations using existing columns ([](#example_df_new_col)). Then we can calculate new biological variables. We can simply add a column by indexing the DataFrame with a new

(example_df_new_col)=
``````{prf:example} Create a new column in a DataFrame by performing a calculation on existing columns
Assuming we have loaded in the Iris dataset into a DataFrame as in [](#example_pandas_read_csv_url), we can create a new column using a calculation with:
```{code-block} python
iris["petal_ratio"] = (iris["petal_length"] / iris["petal_width"])
```
```{code-block} python
iris.head()
```
Will give the output:
```{code-block} python
:class: no-copybutton
   sepal_length  sepal_width  petal_length  petal_width species  petal_ratio
0           5.1          3.5           1.4          0.2  setosa          7.0
1           4.9          3.0           1.4          0.2  setosa          7.0
2           4.7          3.2           1.3          0.2  setosa          6.5
3           4.6          3.1           1.5          0.2  setosa          7.5
4           5.0          3.6           1.4          0.2  setosa          7.0
```
``````


#### Missing Values
Sometimes we are presented with missing values in our data. These can cause problems in downstream analyses so it is best to account for them. To check how many missing values there are, we can use `.isna().sum()` ([](#example_df_isna_sum)). If there were any missing values we can either remove rows (or columns) containing missing values with `.dropna()` or replace them with `.fillna()`. Which one you choose depends on your specific case. 

(example_df_isna_sum)=
``````{prf:example} Count the amount of missing values in a DataFrame
Assuming we have loaded in the Iris dataset into a DataFrame as in [](#example_pandas_read_csv_url), we can count the amount of missing values in the dataframe with:
```{code-block} python
iris.isna().sum()
```
Will give the output:
```{code-block} python
:class: no-copybutton
sepal_length    0
sepal_width     0
petal_length    0
petal_width     0
species         0
petal_ratio     0
dtype: int64
```
There are no missing values!
``````

## Exercises
For these exercises, we will work with a Jupyter Notebook on a remote server.

``````{exercise} Jupyter Notebooks on a remote server
Follow the instructions on Brightspace "Starting a Jupyter Notebook on a remote server and connecting via an SSH tunnel"
``````

Again, the instructions are in the Jupyter Notebook.

### NumPy
``````{exercise} Explore basic properties of vectors and arrays
- Make a NumPy array
- Perform simple mathematical operations on arrays
- Compare NumPy arrays with lists
- Concatenating arrays
- Array indexing
- Perform simple mathematical operations on matrices
- Change values in an array
``````

``````{exercise} Selecting elements from arrays based on logic values
- Select an arbitrary selection of elements, based on supplying a vector (or array) of similar dimensions that contains Booleans `True` or `False` in the order of elements to be selected, or not selected.
- Transform NumPy arrays to standard Python lists and vice versa
- Use comparison operators to select values in a NumPy array
- Use Boolean operators to combine comparison operators to select values in a NumPy array
``````

``````{exercise} Getting Familiar with NumPy
- Create a NumPy array from a list
- Multiply the array with a vector to create a matrix
- Find out what methods you can apply to an array
- Create a truth table (array with True and False)
- Apply the truth table on the matrix to select values
``````

``````{exercise} The *Iris* dataset
- Load in the dataset
- Explore the dataset 
- Subset a vector to extract species name
- Explore the `iris.data` data structe
- Find a method that gives the shape of the data matrix
- Extraxt columns from the data matrix and find out their types
- Create subsets of the data using Boolean vectors
``````

``````{exercise} Euclidean distance of *Iris* flowers
- Calculate Euclidean distance between two *Iris* flowers by writing your own function
- Calculate the Euclidean distance using built-in functions
``````

(section_exc_pandas)=
### Pandas
``````{exercise} The Iris dataset as a DataFrame
- Explore a DataFrame
- Select data from a DataFrame
- Filter observations using comparison operators
- Summarize groups of observations by applying the same calculation to each group
- Add new columns to a DataFrame
- Check for missing values in a DataFrame
``````