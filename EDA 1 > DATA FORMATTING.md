Formally: Data Understanding

> This document only focuses on **changing the presentation of dataframe** (creates a new dataframe temporarily) - show metrics, missing values,  duplicates, filtering, sorting

Visualizing data frame
## Functions: 
----
### Op: Find row x column of data frame 
``` python
df.shape
```
- Show row x column of data 
----
### Op: 
```python
df.head(n)
```
- Show first 'n' rows of data
- default: 5
----
### Op: 
```python
df.columns
```
- Show a list of column names
----
### Op: 
``` python
df.dtypes
```
- [[Pandas 'dtypes' (extension of numpy)]]
- Shows the column name and their data types
- Identifiers of data types and what are they?
----
### Op: 
```python
df.describe()
```
- Show statistic properties of ALL columns. 
	- Default: For mixed data types provided via a `DataFrame`, the default is to return only an analysis of ALL NUMERIC columns.
	- If the dataframe consists ONLY of object and categorical data without any numeric columns, the default is to return an analysis of both the OBJECT and CATEGORICAL columns.
	- If `include='all'` is provided as an option, the result will include a union of attributes of each type.
- [Examples](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.describe.html):
```python
df = pd.DataFrame(
{'categorical_col': pd.Categorical(['d','e','f']),
					'numeric_col': [1, 2, 3],
					'object_col': ['a', 'b', 'c']
				   })

df.describe()
#Notice all columns with NUMERIC data ONLY is outputted by DEFAULT 
#other words: df.describe() == df.describe(exclude=[np.number]) 
'''
# Output:
	   numeric_col
count      3.0
mean       2.0
std        1.0
min        1.0
25%        1.5
50%        2.0
75%        2.5
max        3.0
'''

df.describe(include='all')  
# Notice all 3 types of dtype - categorical dt, numeric dt, object ct, are outputted 
# Also notice that since 'categorical' and 'object' dtypes have no mean, std, min, ... (statistical values) it will be labeled as NaN
'''
# Output:
	   categorical_col numeric_col object_col
count            3      3.0      3
unique           3      NaN      3
top              f      NaN      a
freq             1      NaN      1
mean           NaN      2.0    NaN
std            NaN      1.0    NaN
min            NaN      1.0    NaN
25%            NaN      1.5    NaN
50%            NaN      2.0    NaN
75%            NaN      2.5    NaN
max            NaN      3.0    NaN
'''

df.describe(include=['category'])
'''
# Output:
	   categorical_col
count            3
unique           3
top              d
freq             1
'''

df.describe(exclude=[np.number]) #refer to link above  
# NOT: df.describe(exclude='numeric')
# Excludes only columns with numeric dt

df.describe(exclude=[object]) #refer to link above 
# Excludes only columns with object dt
```
- Statistical properties listed in `df.describe()`:
	- Types of data: Numerical, Object, Categorical (all Pandas data types - [[Pandas 'dtypes' (extension of numpy)]])
	- Statistical measures: count, mean, ... unique, top, freq(some specific to certain type of data)
	- Numeric data (e.g., int_, float_)
		- count 
		- mean
		- std
		- min
		- lower quartile (25%)
		- median (50%)
		- upper quartile (75%)
		- max 
	- Object data (Strings)
		- Count 
		- unique
		- top (mode) - breaks tie arbitrarily (if there is a tie, pick any one)
		- freq (mode's frequency)
	- Object data (Timestamps)
		- Count 
		- unique: Number of unique objects: e.g.,: strings
		- top (mode) - breaks tie arbitrarily
		- freq (mode's frequency)
		- first (first time item)
		- last (last time item)
	- Categorical data
		-  Count 
		- unique
		- top
		- freq
----
### Op: 
``` python
df.astype()
```
- Casting column data type in the data frame
- Functions: [[Pandas 'dtypes' (extension of numpy)]] 
----
### Op: 
``` python
df.loc[boolean_array]
```
- Locate the row with duplicates.  
----
### Op: 
``` python
df.iloc[boolean_array]
```
- Select row by index and column by position
----
### Op: 
```python
df.apply()
```
- Select rows using lambda function 
----

## Find Missing values
----
### Op: 
``` python
df.isna()
```
- List all rows/ entries and columns in the data frame and for each cell, print `True` if there are missing values/ NULL values - `None`, `NaN`, `NaT` in our dataframe, else print `False`.
----
### Op: 
```python 
df.isna().sum()
```
- Find the sum/ total number of rows with NULL values for each column.
- To drop na data, check data preparation document.
- [Types of missing value](https://www.linkedin.com/pulse/nan-nat-none-whats-difference-make-data-useful?trk=organization_guest_main-feed-card_feed-article-content)):
	- `None`: Missing Value
	- `NaN`: "Not a Number" - Columns with Numerical data type with missing value.
	- `NaT`: "Not a Time" - Columns with "DateTime" data type with missing value.

----
## Duplicates
- Resources
	- https://www.statology.org/pandas-find-duplicates/
	- https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.duplicated.html
----
### Op: 
```python
df.duplicated()
```
- Outputs a boolean list denoting duplicate rows.
- Parameters: 
	- `subset`: The subset of columns where we want to find the duplicates.
	- `keep`: Determine how duplicates should be kept.
- Example:
```python
df = pd.DataFrame({
     'brand': ['Yum Yum', 'Yum Yum', 'Yum Yum', 'Indomie', 'Indomie', 'Indomie'],
     'style': ['cup', 'cup', 'cup', 'cup', 'pack', 'pack'],
     'rating': [4, 4, 4, 3.5, 15, 5]
 })
 
print(df)

'''
     brand style  rating
0  Yum Yum   cup     4.0
1  Yum Yum   cup     4.0
2  Yum Yum   cup     4.0
3  Indomie   cup     3.5
4  Indomie  pack    15.0
5  Indomie  pack     5.0
'''

print(df.duplicated())

'''
0    False
1     True
2     True
3    False
4    False
5    False
dtype: bool
'''
# Notice the 2nd to nth occurence of the duplicate will return True.

# Parameter 2: Keep 
# Note: When we want to 'keep' something, we will assign it to False, to highlight that we are 'not interested' in it.

## Keep = 'False': Don't keep the duplicates, which will mark all your duplicates regardless of the sequence of occurence as True.(hence "revealed" when printed)
print(df.duplicated(keep= False)) # Notice this is a boolean

'''
0     True
1     True
2     True
3    False
4    False
5    False
dtype: bool
'''

## Keep = 'first': Keep the "first" occurence of the duplicate, which will not mark the first duplicate occurence as False, and other duplicates as True (hence "revealed" when printed).

df.duplicated(keep='first') # Notice this is a string
'''
0    False
1     True
2     True
3    False
4    False
5    False
dtype: bool
'''

## Keep = 'last': Keep the "last" occurence of the duplicate, which will not mark the last duplicate occurence as False, and other duplicates as True (hence "revealed" when printed).

df.duplicated(keep='last')
'''
0     True
1     True
2    False
3    False
4    False
5    False
dtype: bool
'''

```
----
### Op: 
```python
df.duplicated(subset=['col_name1', ...])
```
- Outputs a boolean list denoting duplicate rows at the specified named column.
- Example:
```python
df = pd.DataFrame({
     'brand': ['Yum Yum', 'Yum Yum', 'Indomie', 'Indomie', 'Indomie'],
     'style': ['cup', 'cup', 'cup', 'pack', 'pack'],
     'rating': [4, 4, 3.5, 15, 5]
 })

print(df)

'''
    brand style  rating
0  Yum Yum   cup     4.0
1  Yum Yum   cup     4.0
2  Indomie   cup     3.5
3  Indomie  pack    15.0
4  Indomie  pack     5.0
'''

# Parameter 1: subset
print(df.duplicated(subset=['brand']))

'''
0    False
1     True
2    False
3     True
4     True
dtype: bool
'''
```

----
### Op: 
```python
~df.duplicated()
```
- Output a boolean list where "UNIQUE rows" are **True** ("complement (tilde) of duplicates") in the table (notice the tilde ~)
----
### Op: 
```python
df[df.duplicated()] 
# OR
df[~df.duplicated()]
```
- Outputs the rows in data frame where the boolean list is True.
	- `df[df.duplicated()]` : Outputs data frame with duplicates.
	- `df[~df.duplicated()]`: Output data frame with unique rows.
```python
df = pd.DataFrame({
     'brand': ['Yum Yum', 'Yum Yum', 'Indomie', 'Indomie', 'Indomie'],
     'style': ['cup', 'cup', 'cup', 'pack', 'pack'],
     'rating': [4, 4, 3.5, 15, 5]
 })

print(df)

'''
    brand style  rating
0  Yum Yum   cup     4.0
1  Yum Yum   cup     4.0
2  Indomie   cup     3.5
3  Indomie  pack    15.0
4  Indomie  pack     5.0
'''

print(df[df.duplicated()])

'''
     brand style  rating
1  Yum Yum   cup     4.0
'''

```
----
### Op: 
- `df.reset_index(drop= False)`
	- Context: It arises when we remove rows (during data preparation). As we remove items from the data frame, the index of the removed row (by default is assigned to each row when we create a data frame) will be removed from the original data frame. Hence, the index will no longer be in uniform increments of 1 in the filtered data. In order to reset the index, we call `reset_index()`
	- Arguments: `drop=True`: When we reset index, the data frame will add a new column known as 'index' with uniform increment of integer at each row. To remove it from our resultant data frame, we should specify to `drop= True` the index column.
----
### Op: 
- `df.value_counts()`
	- Outputs the count of duplicates and its associated unique values.
	- By default, it outputs a sorted order of decreasing counts, with its associated unique value, and its duplicate counts.
	- `df['col_name1'].value_counts()`: 
		- This gives a vector/ "series" of values at 'col_name1', at counts each unique recurring values.

----
## Filtering

We can filter row using two strategies: 
1. Boolean indexing
2. Query

#### The main differences between the two approaches is in their **syntax**. 
- "Boolean indexing" is ***more flexible and allows for more complex conditions***, while 
- "`query`" has a more limited syntax that only allows for simple expressions. Another difference is that `query` ***can be faster than boolean indexing for large dataframes***, as it can leverage some performance optimizations.

- ### Boolean indexing - `df[]`
----
### Op: 
- `df[    [{col_names, ...}]    ]`
	- Show data frame of only the listed column names
	- Tip: We can get all column names using `df.columns` and comment out columns that we want to drop.
----
### Op: 
- `df[df.{column_name} {boolean_operator} {value}]`
```python
df[df.label_1 != 0]
```
- Boolean indexing Pandas functions that uses regex:
	- `count()`: Count occurrences of pattern in each string of the Series/Index 
	- `replace()`: Replace the search string or pattern with the given value 
	- (!) `contains()`: Test if pattern or regex is contained within a string of a Series or Index. Calls re.search() and returns a boolean 
	- `extract()`: Extract capture groups in the regex pat as columns in a DataFrame and returns the captured groups 
	- `findall()`: Find all occurrences of pattern or regular expression in the Series/Index. Equivalent to applying re.findall() on all elements 
	- (!) `match()`: Determine if each string matches a regular expression. Calls re.match() and returns a boolean
	- `split()`: Equivalent to str.split() and Accepts String or regular expression to split on 
	- `rsplit()`: Equivalent to str.rsplit() and Splits the string in the Series/Index from the end
----
### Op: 
- `df['col_name'].str.count(r'{regex}')`
	- Alternative:
		- `df.col_name.str.count(r'{regex}')`
----
### Op: 
- `df['col_name'].str.replace(r'{regex}')`
	- Alternative:
		- `df.col_name.str.replace(r'{regex}')`
----
### Op: 
- `df['col_name'].str.contain(r'{regex}')`
----
### Op: 
- `df['col_name'].str.extract(r'{regex}')`
----
### Op: 
- `df['col_name'].str.findall(r'{regex}')`
----
### Op: 
- `df['col_name'].str.match(r'{regex}')`
----
### Op: 
- `df['col_name'].str.split(r'{regex}')`
----
### Op: 
- `df['col_name'].str.rsplit(r'{regex}')`
----

- ### Queries - `query()`
----
### Op: 
- `df.query('query_syntax_expr_in_string', inplace=False, **kwargs)`
	- `query_syntax_expr` - expression takes conditions to query rorws
	- `inplace` - When set to True, it updates the referring DataFrame
	- `**kwargs` - keyword argyments that works with `eval()`
- Resources: 
	- https://sparkbyexamples.com/pandas/pandas-dataframe-query-examples/
	- [general dataframe filter functions](https://medium.com/gustavorsantos/pandas-query-the-easiest-way-to-filter-data-39e0163ef35a)
	- [dataframe regex](https://www.tutorialspoint.com/how-to-filter-rows-in-pandas-by-regex)
### Op: 
```python
df.query('label_name != 0')
```
- Query with math operators
	- write queries with the mathematical operators, such as `+ , — , *, /, <, >, **`
```python
df.query(' A+B > C+D')

'''
# Before query
+------+---+---+---+---+---+
| Name | A | B | C | D | E |
+------+---+---+---+---+---+
| Jack | 6 | 2 | 9 | 4 | 2 |
| John | 2 | 5 | 6 | 6 | 2 |
| Paul | 4 | 2 | 3 | 7 | 2 |
| Jack | 8 | 3 | 4 | 1 | 5 |
| Paul | 9 | 7 | 3 | 9 | 1 |
+------+---+---+---+---+---+

# After query
+------+---+---+---+---+---+
| Name | A | B | C | D | E |
+------+---+---+---+---+---+
| Jack | 8 | 3 | 4 | 1 | 5 |
| Paul | 9 | 7 | 3 | 9 | 1 |
+------+---+---+---+---+---+
'''
``` 
- Query with variables
	- use a variable within the evaluation expression to filter our dataframe. In that case, use the `@` sign before the variable.
```python
# Query with variable  
name = 'Jack'
df.query('Name == @name')

'''
# Before query
+------+---+---+---+---+---+
| Name | A | B | C | D | E |
+------+---+---+---+---+---+
| Jack | 6 | 2 | 9 | 4 | 2 |
| John | 2 | 5 | 6 | 6 | 2 |
| Paul | 4 | 2 | 3 | 7 | 2 |
| Jack | 8 | 3 | 4 | 1 | 5 |
| Paul | 9 | 7 | 3 | 9 | 1 |
+------+---+---+---+---+---+

# After query
+------+---+---+---+---+---+
| Name | A | B | C | D | E |
+------+---+---+---+---+---+
| Jack | 6 | 2 | 9 | 4 | 2 |
| Jack | 8 | 3 | 4 | 1 | 5 |
+------+---+---+---+---+---+
'''
```
----
- Query for NAs
### Op: 
```python
df.query('col_name != col_name')
```
- ### Regex queries in pandas
- Resources:
	- [How to use Regex in Pandas](https://kanoki.org/2019/11/12/how-to-use-regex-in-pandas/)
- Query if a regex is in strings 
	- Similar to the keyword `LIKE` in SQL.
```python
df.query('col_name.str.contains("J")', engine='python')
'''
# Before query
+------+---+---+---+---+---+
| Name | A | B | C | D | E |
+------+---+---+---+---+---+
| Jack | 6 | 2 | 9 | 4 | 2 |
| John | 2 | 5 | 6 | 6 | 2 |
| Paul | 4 | 2 | 3 | 7 | 2 |
| Jack | 8 | 3 | 4 | 1 | 5 |
| Paul | 9 | 7 | 3 | 9 | 1 |
+------+---+---+---+---+---+

# After query
+------+---+---+---+---+---+
| Name | A | B | C | D | E |
+------+---+---+---+---+---+
| Jack | 6 | 2 | 9 | 4 | 2 |
| John | 2 | 5 | 6 | 6 | 2 |
| Jack | 8 | 3 | 4 | 1 | 5 |
+------+---+---+---+---+---+
'''
```
### Op: 
- Query if string matches the regex 
```
df.
```
- Query values in a list
```python
# Using Lists  
df.query("Name in ['Paul','John'] & D < 9")
'''
# Before query
+------+---+---+---+---+---+
| Name | A | B | C | D | E |
+------+---+---+---+---+---+
| Jack | 6 | 2 | 9 | 4 | 2 |
| John | 2 | 5 | 6 | 6 | 2 |
| Paul | 4 | 2 | 3 | 7 | 2 |
| Jack | 8 | 3 | 4 | 1 | 5 |
| Paul | 9 | 7 | 3 | 9 | 1 |
+------+---+---+---+---+---+

# After query
+------+---+---+---+---+---+
| Name | A | B | C | D | E |
+------+---+---+---+---+---+
| John | 2 | 5 | 6 | 6 | 2 |
| Paul | 4 | 2 | 3 | 7 | 2 |
+------+---+---+---+---+---+
'''
```
-----
### Op: 
- `df.query(...).groupby()`:
			- 


## Sorting
- Resources:
	- https://www.geeksforgeeks.org/how-to-sort-pandas-dataframe/
	- https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.sort_values.html
- Parameters 
	- `by` :
	- `axis`:
	- `ascending`:
	- `inplace`:
	- `kind`:
	- `na_position`:
	- `ignore_index`:
	- `key`:
----
### Op: 
- `df.sort_values(by=[{col_1}, {col_2}, ..., {col_n}])`
	- `by`: (mandatory argument)
	- Sorting by named columns (number of columns to be sorted MUST range from 1 - n columns.)
```python
# importing pandas library
import pandas as pd
 
# creating and initializing a nested list
age_list = [['Afghanistan', 1952, 8425333, 'Asia'],
            ['Australia', 1957, 9712569, 'Oceania'],
            ['Brazil', 1962, 76039390, 'Americas'],
            ['China', 1957, 637408000, 'Asia'],
            ['France', 1957, 44310863, 'Europe'],
            ['India', 1952, 3.72e+08, 'Asia'],
            ['United States', 1957, 171984000, 'Americas']]
 
# creating a pandas dataframe
df2 = pd.DataFrame(age_list, columns=['Country', 'Year',
                                     'Population', 'Continent'])
 
display(df2)

'''
+---------------+------+----------------+-----------+
|    Country    | Year |   Population   | Continent |
+---------------+------+----------------+-----------+
|  Afghanistan  | 1952 |   8425333.0    |    Asia   |
|   Australia   | 1957 |   9712569.0    |  Oceania  |
|     Brazil    | 1962 |   76039390.0   | Americas  |
|     China     | 1957 |  637408000.0   |    Asia   |
|     France    | 1957 |   44310863.0   |  Europe   |
|      India    | 1952 |  372000000.0   |    Asia   |
| United States | 1957 |  171984000.0   | Americas  |
+---------------+------+----------------+-----------+
'''

df2.sort_values(by=['Continent'])

'''
+---------------+------+----------------+-----------+
|    Country    | Year |   Population   | Continent |
+---------------+------+----------------+-----------+
|     Brazil    | 1962 |   76039390.0   | Americas  |
| United States | 1957 |  171984000.0   | Americas  |
|  Afghanistan  | 1952 |   8425333.0    |    Asia   |
|     China     | 1957 |  637408000.0   |    Asia   |
|      India    | 1952 |  372000000.0   |    Asia   |
|     France    | 1957 |   44310863.0   |  Europe   |
|   Australia   | 1957 |   9712569.0    |  Oceania  |
+---------------+------+----------------+-----------+
'''
```

----
### Op: 
```python
df.sort_values(by=['col_1', ...], ascending=False/ True)
```
- `ascending = True`: sorts column by ascending order. (Default)
- `ascending = False`: sorts column by descending order.

```python
# importing pandas library
import pandas as pd
 
# creating and initializing a nested list
age_list = [['Afghanistan', 1952, 8425333, 'Asia'],
            ['Australia', 1957, 9712569, 'Oceania'],
            ['Brazil', 1962, 76039390, 'Americas'],
            ['China', 1957, 637408000, 'Asia'],
            ['France', 1957, 44310863, 'Europe'],
            ['India', 1952, 3.72e+08, 'Asia'],
            ['United States', 1957, 171984000, 'Americas']]
 
# creating a pandas dataframe
df2 = pd.DataFrame(age_list, columns=['Country', 'Year',
                                     'Population', 'Continent'])
 
display(df2)

'''
+---------------+------+----------------+-----------+
|    Country    | Year |   Population   | Continent |
+---------------+------+----------------+-----------+
|  Afghanistan  | 1952 |   8425333.0    |    Asia   |
|   Australia   | 1957 |   9712569.0    |  Oceania  |
|     Brazil    | 1962 |   76039390.0   | Americas  |
|     China     | 1957 |  637408000.0   |    Asia   |
|     France    | 1957 |   44310863.0   |  Europe   |
|      India    | 1952 |  372000000.0   |    Asia   |
| United States | 1957 |  171984000.0   | Americas  |
+---------------+------+----------------+-----------+
'''

df2.sort_values(by=['Year'], ascending=False)

'''
+---------------+------+----------------+-----------+
|    Country    | Year |   Population   | Continent |
+---------------+------+----------------+-----------+
|     Brazil    | 1962 |   76039390.0   | Americas  |
|   Australia   | 1957 |   9712569.0    |  Oceania  |
|     China     | 1957 |  637408000.0   |    Asia   |
|     France    | 1957 |   44310863.0   |  Europe   |
| United States | 1957 |  171984000.0   | Americas  |
|  Afghanistan  | 1952 |   8425333.0    |    Asia   |
|      India    | 1952 |  372000000.0   |    Asia   |
+---------------+------+----------------+-----------+
'''
```

----

### Op. Group rows with respect to unique values
```python
df.groupby('{Column_name}')
```

- Example of `df.groupby()`
```python
df = pd.DataFrame(data) # Group the DataFrame by the 'Category' column 
grouped = df.groupby('Category')

### Print 1
print(f'What dt is returned?: {grouped}')

# Iterate through the groups and print the group name and the corresponding data 
for name, group in grouped: 
	print(type(group)) 
	print(f"\nGroup Name: {name}") 
	print(group) 
```
- Output
```
What dt is returned>: <pandas.core.groupby.generic.DataFrameGroupBy object at 0x282cf3790>


<class 'pandas.core.frame.DataFrame'>
Group Name: A
  Category  Value
0        A     10
2        A     15
4        A     12

<class 'pandas.core.frame.DataFrame'>
Group Name: B
  Category  Value
1        B     20
3        B     25
5        B     18
```

