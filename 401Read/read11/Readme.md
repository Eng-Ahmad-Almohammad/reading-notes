# Table of contents
|Read No. | Name of chapter|
|:---------: |:--------------:|
|11|[What is Jupyter Lab](What-is-Jupyter-Lab.md)
|11|[NumPy](NumPy.md)


# What is Jupyter Lab
## Overview
### JupyterLab is a next-generation web-based user interface for Project Jupyter.

### JupyterLab enables you to work with documents and activities such as Jupyter notebooks, text editors, terminals, and custom components in a flexible, integrated, and extensible manner. 

### You can arrange multiple documents and activities side by side in the work area using tabs and splitters. Documents and activities integrate with each other, enabling new workflows for interactive computing, for example:

- Code Consoles provide transient scratchpads for running code interactively, with full support for rich output. A code console can be linked to a notebook kernel as a computation log from the notebook, for example.
- Kernel-backed documents enable code in any text file (Markdown, Python, R, LaTeX, etc.) to be run interactively in any Jupyter kernel.
- Notebook cell outputs can be mirrored into their own tab, side by side with the notebook, enabling simple dashboards with interactive controls backed by a kernel.
- Multiple views of documents with different editors or viewers enable live editing of documents reflected in other viewers. For example, it is easy to have live preview of Markdown, Delimiter-separated Values, or Vega/Vega-Lite documents.

### JupyterLab also offers a unified model for viewing and handling data formats. JupyterLab understands many file formats (images, CSV, JSON, Markdown, PDF, Vega, Vega-Lite, etc.) and can also display rich kernel output in these formats. 

## JupyterLab Releases

### Since JupyterLab 0.32 (February 2018), the releases of JupyterLab are suitable for general daily use by both Jupyter novices and users experienced with the Classic Notebook interface. As of the 1.0 release (June 2019), it is additionally ready for extension writers who wish to further customize the JupyterLab experience for others. Please review the JupyterLab Changelog for detailed descriptions of each release.

### The extension developer API is evolving, and we also are currently iterating on UI/UX improvements. We appreciate feedback on our GitHub issues page as we evolve towards a stable extension development API.

### JupyterLab will eventually replace the classic Jupyter Notebook. Throughout this transition, the same notebook document format will be supported by both the classic Notebook and JupyterLab.




# NumPy Tutorial

### NumPy is a commonly used Python data analysis package. By using NumPy, you can speed up your workflow, and interface with other packages in the Python ecosystem, like scikit-learn, that use NumPy under the hood.

### In this tutorial, we’ll walk through using NumPy to analyze data on wine quality. The data contains information on various attributes of wines, such as pH and fixed acidity, along with a quality score between 0 and 10 for each wine. 

### The data is in what I’m going to call ssv (semicolon separated values) format — each record is separated by a semicolon (;), and rows are separated by a new line. There are 1600 rows in the file, including a header row, and 12 columns.

## Lists Of Lists for CSV Data

### Before using NumPy, we’ll first try to work with the data using Python and the csv package. We can read in the file using the csv.reader object, which will allow us to read in and split up all the content from the ssv file.

### In the below code, we:

- Import the csv library.
- Open the winequality-red.csv file.
- With the file open, create a new csv.reader object.
- Pass in the keyword argument delimiter=";" to make sure that the records are split up on the semicolon character instead of the default comma character.

- Call the list type to get all the rows from the file.

- Assign the result to wines.

```python
import csv
with open('winequality-red.csv', 'r') as f:
    wines = list(csv.reader(f, delimiter=';'))
```

### The data has been read into a list of lists. Each inner list is a row from the ssv file. As you may have noticed, each item in the entire list of lists is represented as a string, which will make it harder to do computations.

###  We can find the average quality of the wines. The below code will:

- Extract the last element from each row after the header row.
- Convert each extracted element to a float.
- Assign all the extracted elements to the list qualities.
- Divide the sum of all the elements in qualities by the total number of elements in qualities to the get the mean.

```python
qualities =
[float(item[-1]) for item in wines[1:]]
sum(qualities) / len(qualities)
```

### Although we were able to do the calculation we wanted, the code is fairly complex, and it won’t be fun to have to do something similar every time we want to compute a quantity. Luckily, we can use NumPy to make it easier to work with our data.

## Numpy 2-Dimensional Arrays

### With NumPy, we work with multidimensional arrays. We’ll dive into all of the possible types of multidimensional arrays later on, but for now, we’ll focus on 2-dimensional arrays. A 2-dimensional array is also known as a matrix, and is something you should be familiar with. In fact, it’s just a different way of thinking about a list of lists. A matrix has rows and columns. By specifying a row number and a column number, we’re able to extract an element from a matrix.

### In a NumPy array, the number of dimensions is called the rank, and each dimension is called an axis. So the rows are the first axis, and the columns are the second axis.

## Creating A NumPy Array

### We can create a NumPy array using the numpy.array function. If we pass in a list of lists, it will automatically create a NumPy array with the same number of rows and columns. Because we want all of the elements in the array to be float elements for easy computation, we’ll leave off the header row, which contains strings. One of the limitations of NumPy is that all the elements in an array have to be of the same type, so if we include the header row, all the elements in the array will be read in as strings. Because we want to be able to do computations like find the average quality of the wines, we need the elements to all be floats.

### In the below code, we:

- Import the numpy package.
- Pass the list of lists wines into the array function, which converts it into a NumPy array.
- Exclude the header row with list slicing.
- Specify the keyword argument dtype to make sure each element is converted to a float. We’ll dive more into what the dtype is later on.

```python
import csv
with open("winequality-red.csv", 'r') as f:
    wines = list(csv.reader(f, delimiter=";"))
import numpy as np
wines = np.array(wines[1:], dtype=np.float)
```

### Try running the above code and seeing what happens!

```python
array([[ 7.4 , 0.7 , 0. , ..., 0.56 , 9.4 , 5. ],
[ 7.8 , 0.88 , 0. , ..., 0.68 , 9.8 , 5. ],
[ 7.8 , 0.76 , 0.04 , ..., 0.65 , 9.8 , 5. ],
...,
[ 6.3 , 0.51 , 0.13 , ..., 0.75 , 11. , 6. ],
[ 5.9 , 0.645, 0.12 , ..., 0.71 , 10.2 , 5. ],
[ 6. , 0.31 , 0.47 , ..., 0.66 , 11. , 6. ]])
```

### We can check the number of rows and columns in our data using the shape property of NumPy arrays:
```python
wines.shape
```
```
(1599, 12)
```

## Alternative NumPy Array Creation Methods

### There are a variety of methods that you can use to create NumPy arrays. To start with, you can create an array where every element is zero. The below code will create an array with 3 rows and 4 columns, where every element is 0, using numpy.zeros:

```python
import numpy as np
empty_array = np.zeros((3,4)) empty_array
```

### You can also create an array where each element is a random number using numpy.random.rand. Here’s an example:
```python
np.random.rand(3,4)
```
```
array([[ 0.2247223 , 0.92240549, 0.14541893, 0.61731257],
[ 0.00154957, 0.82342197, 0.74044906, 0.11466845],
[ 0.6152478 , 0.14433138, 0.13009583, 0.22981301]])
```

## Using NumPy To Read In Files

### It’s possible to use NumPy to directly read csv or other files into arrays. We can do this using the numpy.genfromtxt function. We can use it to read in our initial data on red wines.

##3 In the below code, we:

- Use the genfromtxt function to read in the winequality-red.csv file.
- Specify the keyword argument delimiter=";" so that the fields are parsed properly.
- Specify the keyword argument skip_header=1 so that the header row is skipped.
```python

wines = np.genfromtxt("winequality-red.csv", delimiter=";", skip_header=1)

```

## Indexing NumPy Arrays

### We now know how to create arrays, but unless we can retrieve results from them, there isn’t a lot we can do with NumPy. We can use array indexing to select individual elements, groups of elements, or entire rows and columns. One important thing to keep in mind is that just like Python lists, NumPy is zero-indexed, meaning that the index of the first row is 0, and the index of the first column is 0. If we want to work with the fourth row, we’d use index 3, if we want to work with the second row, we’d use index 1, and so on.

### Let’s select the element at row 3 and column 4. In the below code, we pass in the index 2 as the row index, and the index 3 as the column index. This retrieves the value from the fourth column of the third row:

```python

wines[2,3]

```


## Slicing NumPy Arrays

### If we instead want to select the first three items from the fourth column, we can do it using a colon (:). A colon indicates that we want to select all the elements from the starting index up to but not including the ending index. This is also known as a slice:

```python
wines[0:3,3]
```
```
array([ 1.9, 2.6, 2.3])
```

## Assigning Values To NumPy Arrays

### We can also use indexing to assign values to certain elements in arrays. We can do this by assigning directly to the indexed value:

```python
wines[1,5] = 10
```

## 1-Dimensional NumPy Arrays
### One of the most common types of multidimensional arrays is the 1-dimensional array, or vector.

###  Each row and column in a 2-dimensional array is a 1-dimensional array. 

### Most NumPy functions that we’ve worked with, such as numpy.random.rand, can be used with multidimensional arrays. Here’s how we’d use numpy.random.rand to generate a random vector:

```python
np.random.rand(3)
```
```
array([ 0.88588862, 0.85693478, 0.19496774])
```

## N-Dimensional NumPy Arrays
### This doesn’t happen extremely often, but there are cases when you’ll want to deal with arrays that have greater than 3 dimensions. One way to think of this is as a list of lists of lists.

### Indexing and slicing work the exact same way with a 3-dimensional array, but now we have an extra axis to pass in. 

## NumPy Data Types

### As we mentioned earlier, each NumPy array can store elements of a single data type.

### You can find the data type of a NumPy array by accessing the dtype property:

```python
wines.dtype
```

```
dtype('float64')
```

### NumPy has several different data types, which mostly map to Python data types, like:

- float — numeric floating point data.
- int — integer data.
- string — character data.
- object — Python objects.

## Converting Data Types

### You can use the numpy.ndarray.astype method to convert an array to a different type. The method will actually copy the array, and return a new array with the specified data type.

### We can check the name property of the dtype of the resulting array to see what data type NumPy mapped the resulting array to:

```python
int_wines = wines.astype(int)
int_wines.dtype.name
```

## NumPy Array Operations

### NumPy makes it simple to perform mathematical operations on arrays. This is one of the primary advantages of NumPy, and makes it quite easy to do computations.

## Single Array Math

### If you do any of the basic mathematical operations (/, *, -, +, ^) with an array and a value, it will apply the operation to each of the elements in the array.

### Let’s say we want to add 10 points to each quality score. Here’s how we’d do that:

```python
wines[:,11] + 10
```

### Note that the above operation won’t change the wines array — it will return a new 1-dimensional array where 10 has been added to each element in the quality column of wines.

## Multiple Array Math

### It’s also possible to do mathematical operations between arrays. This will apply the operation to pairs of elements. For example, if we add the quality column to itself, here’s what we get:

```python
wines[:,11] + wines[:,11]
```

## Broadcasting

### Unless the arrays that you’re operating on are the exact same size, it’s not possible to do elementwise operations. In cases like this, NumPy performs broadcasting to try to match up elements. Essentially, broadcasting involves a few steps:

- The last dimension of each array is compared.
- If the dimension lengths are equal, or one of the dimensions is of length 1, then we keep going.
- If the dimension lengths aren’t equal, and none of the dimensions have length 1, then there’s an error.
- Continue checking dimensions until the shortest array is out of dimensions.

### For example, the following two shapes are compatible:


```python
A: (50,3)
B (3,)
```

### This is because the length of the trailing dimension of array A is 3, and the length of the trailing dimension of array B is 3. They’re equal, so that dimension is okay. Array B is then out of elements, so we’re okay, and the arrays are compatible for mathematical operations.


### These two arrays don’t match:
```python
A: (50,50)
B: (49,49)
```
### The lengths of the dimensions aren’t equal, and neither array has either dimension length equal to 1.

## NumPy Array Methods

### In addition to the common mathematical operations, NumPy also has several methods that you can use for more complex calculations on arrays. An example of this is the numpy.ndarray.sum method. This finds the sum of all the elements in an array by default.

### The total of all of our quality ratings is 154.1788. We can pass the axis keyword argument into the sum method to find sums over an axis. If we call sum across the wines matrix, and pass in axis=0, we’ll find the sums over the first axis of the array. This will give us the sum of all the values in every column. This may seem backwards that the sums over the first axis would give us the sum of each column, but one way to think about this is that the specified axis is the one “going away”. So if we specify axis=0, we want the rows to go away, and we want to find the sums for each of the remaining axes across each row:
```python
wines.sum(axis=0)
```
```
array([ 13303.1 , 843.985 , 433.29 , 4059.55 ,
139.859 , 25384. , 74302. , 1593.79794,
5294.47 , 1052.38 , 16666.35 , 9012. ])
```

### There are several other methods that behave like the sum method, including:
- numpy.ndarray.mean — finds the mean of an array.
- numpy.ndarray.std — finds the standard deviation of an array.
- numpy.ndarray.min — finds the minimum value in an array.
- numpy.ndarray.max — finds the maximum value in an array.


## NumPy Array Comparisons

### NumPy makes it possible to test to see if rows match certain values using mathematical comparison operations like <, >, >=, <=, and ==. For example, if we want to see which wines have a quality rating higher than 5, we can do this:

```python
wines[:,11] > 5

```

```
array([False, False, False, ..., True, False, True], dtype=bool)
```

## Subsetting

### One of the powerful things we can do with a Boolean array and a NumPy array is select only certain rows or columns in the NumPy array. For example, the below code will only select rows in wines where the quality is over 7:

```python
high_quality = wines[:,11] > 7
wines[high_quality,:][:3,:]

```

### We select only the rows where high_quality contains a True value, and all of the columns. 

## Reshaping NumPy Arrays

### We can change the shape of arrays while still preserving all of their elements. This often can make it easier to access array elements. The simplest reshaping is to flip the axes, so rows become columns, and vice versa. We can accomplish this with the numpy.transpose function:
```python
np.transpose(wines).shape
```

### We can use the numpy.ravel function to turn an array into a one-dimensional representation. It will essentially flatten an array into a long sequence of values:

```python
wines.ravel()
```

### Finally, we can use the numpy.reshape function to reshape an array to a certain shape we specify. The below code will turn the second row of wines into a 2-dimensional array with 2 rows and 6 columns:
```python
wines[1,:].reshape((2,6))
```

## Combining NumPy Arrays

### With NumPy, it’s very common to combine multiple arrays into a single unified array. We can use numpy.vstack to vertically stack multiple arrays. Think of it like the second arrays’s items being added as new rows to the first array. We can read in the winequality-white.csv dataset that contains information on the quality of white wines, then combine it with our existing dataset, wines, which contains information on red wines.

### In the below code, we:

- Read in winequality-white.csv.
- Display the shape of white_wines.
```python
white_wines = np.genfromtxt("winequality-white.csv", delimiter=";", skip_header=1)
white_wines.shape
```
```
(4898, 12)
```
### As you can see, we have attributes for 4898 wines. Now that we have the white wines data, we can combine all the wine data.

### In the below code, we:

- Use the vstack function to combine wines and white_wines.
- Display the shape of the result.
```python
all_wines = np.vstack((wines, white_wines))
all_wines.shape
```
```
(6497, 12)
```
### As you can see, the result has 6497 rows, which is the sum of the number of rows in wines and the number of rows in red_wines.

### If we want to combine arrays horizontally, where the number of rows stay constant, but the columns are joined, then we can use the numpy.hstack function. The arrays we combine need to have the same number of rows for this to work.

### Finally, we can use numpy.concatenate as a general purpose version of hstack and vstack. If we want to concatenate two arrays, we pass them into concatenate, then specify the axis keyword argument that we want to concatenate along. Concatenating along the first axis is similar to vstack, and concatenating along the second axis is similar to hstack:
```python
np.concatenate((wines, white_wines), axis=0)
```