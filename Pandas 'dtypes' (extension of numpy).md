
Table of contents
1. SHOW data types in each column of Pandas DataFrame
2. TYPES of data types in Pandas DataFrame 
3. CAST data type of a column in the Pandas Data Frame

Why do we care about data type in our Pandas DATAFRAME?
- Column arithmetic 
	- (e.g., if columns should be added, 2 numerical would compute "addition", but 1 numerical and 1 object will result in a "concatenation" (string operation))
- Specifying dtypes saves memory usage by using data types that are better suited for representation of data.

# 1)
pandas dtypes extend Numpy's data type. (We can also create and extend our own data types from Numpy)
Pandas dataframe: `df.dtypes` to list the data types used to represent each column in the data frame.
```python
In[349]: df.dtypes
Out[349]: 
col_A           float64
col_B             int64
col_C            object
col_D    datetime64[ns]
col_E           float32
col_F              bool
col_G              int8
dtype: object

# Notice 'object' dtype is displayed. Because there is no way to represent float64, int64, object, datetime64[ns], float32, bool, int8, but as strings (object)
```

# 2)
# Dtypes in Pandas (data types only found in Pandas): [Doc](https://pandas.pydata.org/pandas-docs/stable/user_guide/basics.html?highlight=basics#dtypes)
1. **Object**: `object`
	1. Most generic data type, chosen if a Pandas Series, contains data with *multiple*  different dtypes in a single column (and no single dtype can define it)/ like an array which stores different data types.
		```python
		# these ints are coerced to floats
		In [351]: pd.Series([1, 2, 3, 4, 5, 6.0])
		Out[351]: 
		0    1.0
		1    2.0
		2    3.0
		3    4.0
		4    5.0
		5    6.0
		dtype: float64
		
		# string data forces an ``object`` dtype
		In [352]: pd.Series([1, 2, 3, 6.0, "foo"])
		Out[352]: 
		0      1
		1      2
		2      3
		3    6.0
		4    foo
		dtype: object
		 
		```
2. **tz-aware datetime**: `'datetime64[ns, <tz>]'`
3. **categorical**: ``'category'``
	1. Variables that takes on a limited, and usually fixed, number of possible values. (E.g., gender, social class, blood type, country affiliation)
	2.   Benefits:
		- A string variable consisting of only a few different values. Converting such a string variable to a categorical variable will save some memory.
		- The lexical order of a variable is not the same as the logical order (“one”, “two”, “three”). By converting to a categorical and specifying an order on the categories, sorting and min/max will use the logical order instead of the lexical order.
		- As a signal to other python libraries that this column should be treated as a categorical variable (e.g. to use suitable statistical methods or plot types). 
	- It can be created using
		- `pandas.Categorical(values, categories, ordered)`
		- `pd.Series(["a","b","c","a"], dtype="category")`
	- [Examples](https://www.tutorialspoint.com/python_pandas/python_pandas_categorical_data.htm): 
	```python
	# In[2]: 
	s = pd.Series(["a", "b", "c", "a"], dtype="category")
	s
	
	# Out[2]: 
	# 0    a
	# 1    b
	# 2    c
	# 3    a
	# dtype: category
	# Categories (3, object): ['a', 'b', 'c']
	
	# In[3]:
	cat = pd.Categorical(['a', 'b', 'c', 'a', 'b', 'c'])
	cat
	
	# Out[3]:
	# [a, b, c, a, b, c]
	# Categories (3, object): [a, b, c]

	# In[4]:
	cat = cat=pd.Categorical(['a','b','c','a','b','c','d'],\
		['c', 'b', 'a'],ordered=True)

	# Out[4]:
	# [a, b, c, a, b, c, NaN]
	# Categories (3, object): [c < b < a]

	df = pd.DataFrame({'categorical': pd.Categorical(['d','e','f']),
	                    'numeric': [1, 2, 3],
	                    'object': ['a', 'b', 'c']
	                   })
	# Out[5]:
	#  	        categorical  numeric object
	# 0                d      1        a
	# 1                e      2        b
	# 2                f      3        c
	```
4. **period** (time spans): `'period[<freq>]'`
5. **sparse**: `'Sparse'`, `'Sparse[int]'`, `'Sparse[float]'`
6. **intervals**: `'interval'`, `'Interval'`, `'Interval[<numpy_dtype>]'`, `'Interval[datetime64[ns, <tz>]]'`, `'Interval[timedelta64[<freq>]]'` 
7. **nullable integer**: `'Int8'`, `'Int16'`, `'Int32'`, `'Int64'`, `'UInt8'`, `'UInt16'`, `'UInt32'`, `'UInt64'`
8. **Strings**: `'string'`
9. **Boolean**: `'boolean'`


# 3)
# Casting dtype in DataFrame

THREE ways to cast column data types in Pandas DataFrame
1. `df.astype(dtype, copy=True, errors='raise')`
2. `pd.to_numeric()`, `pd.to_datetime()` [usage](https://pbpython.com/pandas_dtypes.html)
3. [Create custom convertion functions](https://pbpython.com/pandas_dtypes.html)


Assume:
```python
d = {'col1': [1, 2], 'col2': [3, 4]}
df = pd.DataFrame(data=d)
df.dtypes

# Output:
# col1    int64
# col2    int64
# dtype: object
```
- Casting ALL columns
```python
df.astype('int32').dtypes

# Output: 
# col1    int32
# col2    int32
# dtype: object
```
- Casting SPECIFIC columns
```python
df.astype({'col1': 'int32'}).dtypes

# Output: 
# col1    int32
# col2    int64
# dtype: object

df['col_1'].astype('int32')

# Output: 
# col1    int32
# col2    int64
# dtype: object

```

- Casting MULTIPLE SPECIFIC columns
```python
public = pd.read_csv("categories.csv")

public.dtypes
# Output: 
# parks          object
# playgrounds    object
# sports         object
# roading        object               
# resident       int64
# children       int64

for col in ['parks', 'playgrounds', 'sports', 'roading']:
	# Notice we are accessing only the column of the data frame
    public[col] = public[col].astype('category')
    
```




