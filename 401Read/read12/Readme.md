# Table of contents
|Read No. | Name of chapter|
|:---------: |:--------------:|
|12|[10 minutes to pandas](Pandas-in-10.md)










# 10 minutes to pandas
## Object creation:

### Creating a Series by passing a list of values, letting pandas create a default integer index:
```python
s = pd.Series([1, 3, 5, np.nan, 6, 8])

s
```
```
Out[4]: 
0    1.0
1    3.0
2    5.0
3    NaN
4    6.0
5    8.0
dtype: float64
```

### Creating a DataFrame by passing a NumPy array, with a datetime index and labeled columns:
```python
dates = pd.date_range('20130101', periods=6)

dates
```
```
 
DatetimeIndex(['2013-01-01', '2013-01-02', '2013-01-03', '2013-01-04',
               '2013-01-05', '2013-01-06'],
              dtype='datetime64[ns]', freq='D')
```python
df = pd.DataFrame(np.random.randn(6, 4), index=dates, columns=list('ABCD'))

df
```
```

                   A         B         C         D
2013-01-01  0.469112 -0.282863 -1.509059 -1.135632
2013-01-02  1.212112 -0.173215  0.119209 -1.044236
2013-01-03 -0.861849 -2.104569 -0.494929  1.071804
2013-01-04  0.721555 -0.706771 -1.039575  0.271860
2013-01-05 -0.424972  0.567020  0.276232 -1.087401
2013-01-06 -0.673690  0.113648 -1.478427  0.524988
```

## Viewing data
### Here is how to view the top and bottom rows of the frame:

```python
df.head()
df.tail(3)
```

### DataFrame.to_numpy() gives a NumPy representation of the underlying data. Note that this can be an expensive operation when your DataFrame has columns with different data types, which comes down to a fundamental difference between pandas and NumPy: NumPy arrays have one dtype for the entire array, while pandas DataFrames have one dtype per column. When you call DataFrame.to_numpy(), pandas will find the NumPy dtype that can hold all of the dtypes in the DataFrame. This may end up being object, which requires casting every value to a Python object.


## Selection

### Selecting a single column, which yields a Series, equivalent to df.A:
```python
df['A']
```

## Selection by label:
### For getting a cross section using a label:
```python
df.loc[dates[0]]
```

## Selection by position

### Select via the position of the passed integers:

```python
df.iloc[3]
```


## Boolean indexing¶
### Using a single column’s values to select data.
```python
df[df['A'] > 0]
```

## Setting

### Setting a new column automatically aligns the data by the indexes.
```python
s1 = pd.Series([1, 2, 3, 4, 5, 6], index=pd.date_range('20130102', periods=6))
```

## Missing data

### pandas primarily uses the value np.nan to represent missing data. It is by default not included in computations.

### Reindexing allows you to change/add/delete the index on a specified axis. This returns a copy of the data.

## Merge
### pandas provides various facilities for easily combining together Series and DataFrame objects with various kinds of set logic for the indexes and relational algebra functionality in the case of join / merge-type operations.

### Concatenating pandas objects together with concat().

## Grouping
### By “group by” we are referring to a process involving one or more of the following steps:

- Splitting the data into groups based on some criteria

- Applying a function to each group independently

- Combining the results into a data structure

## Plotting

### We use the standard convention for referencing the matplotlib API.

## Getting data in/out
### CSV

### Writing to a csv file.
```python
df.to_csv('foo.csv')
```
### Reading from a csv file.
```python
pd.read_csv('foo.csv')
```
