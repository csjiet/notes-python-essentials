1. What is a data frame?
	1. 2D labeled data structure with columns with specific data types.
2. How are data frames stored in a computer?
	1. Key (column identifiers) - value (array of values with specific data types)
	2. Syntax 
```python
pandas.DataFrame(data, index, columns, dtype, copy)
```
- Arguments:
	- `data`: 
		- ndarray: 
			- structured (different types, nested) 
			- homogeneous
		- Iterable:
		- dict: E.g.,:`{'col_name': {pandas.Series, array, constant, class, list}, ...}`
		- DataFrame:
	- `index`:
		- Default: Range index
		- Categorical index
		- Multi index
		- Interval index
		- Datetime index
		- Timedelta index
		- period index
	- `columns`:
		- Default: range index, search for existing column labels (if exists)
	- `dtype`:
		- Default: `infer` 
		- Data type to force 
	- `copy`:
		- Default: 
			- data = dict, then `copy= True`: 
			- data = DataFrame/ 2D ndaray, then `copy= False`:
			- data = dict containing one or more Series of possibly different types, then `copy= False`:

# Types of data frame:
1) Uniindex data frames
	1) Accessing data: [[Pandas Uni-index Dataframe Indexing]]
2) Multiindex data frames
	1) Accessing data: [[Pandas Multi-index Dataframe Indexing or Hierarchical indexing]]


## 1) Uniindex data frames
	3. Example of how Pandas Data Frame represent data:
```python
########## EXAMPLE 1 
# data = dict, index = Range index; default (monotonic integer) 
d = {'col1': [1, 2], 'col2': [3, 4]}
df = pd.DataFrame(data=d)

# Output:
#    col1  col2
# 0     1     3
# 1     2     4

########## EXAMPLE 2: 
# data = ndarray
df2 = pd.DataFrame(np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]]),
                    columns=['a', 'b', 'c'])
# Output
#    a  b  c
# 0  1  2  3
# 1  4  5  6
# 2  7  8  9

########## EXAMPLE 3: 
# data = dict, index = Date time index (datatime64)
df = pd.DataFrame(  
{'temp': [12.1, 11, 13],  
'rain': [9.2, 10.0, 2.2] },  

index=pd.DatetimeIndex(
	['2020-10-12',  
	'2020-10-13',  
	'2020-10-14'],  
	
	name='date'
	)  
)

# Output
#		       temp   rain 
# date
# 2020-10-12   12.1   9.2
# 2020-10-13   11.0   10.0
# 2020-10-14   13.0   2.2


########## EXAMPLE 4: 
# data = dict with (ndarray, Pandas.Series), index = 
d = {'col1': [0, 1, 2, 3], 'col2': pd.Series([2, 3], index=[2, 3])}
pd.DataFrame(data=d, index=[0, 1, 2, 3])

# Output
#    col1  col2
# 0     0   NaN
# 1     1   NaN
# 2     2   2.0
# 3     3   3.0


```

## 2) Multiindex data frames

```python

```

3. How are data frames different from normal matrix arrays? 


Resources:
- [Type of DataFrame index arguments](https://sparkbyexamples.com/pandas/pandas-index-explained-with-examples/#:~:text=Pandas%20Index%20is%20an%20immutable,labeled%20axis%20rows%2C%20and%20columns.)

