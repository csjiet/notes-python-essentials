Formally: "Data Preparation"

> This document focuses on **altering the data frame by value** (overwrites the existing dataframe) - add/ removal/ replace

Making changes to data frame
## Operations:
- Replace values

## Functions:
---- 
### Op: Replace values
```python 
df['col_name'] = df['col_name'].replace({value/ list_of_values}, {replaced_value/replaced_list_of_values})
```
- Resources:
	- https://datatofish.com/replace-values-pandas-dataframe/
- Replace existing values in a column to new values.

---- 
### Op. Remove columns
```python
df.drop({labels}, axis, index, columns, level, inplace, errors )
```
- Removes a list of "named" columns
- Arguments:
	- `labels`: \[`labels`\]; A list of columns with their identifiers/ names that we are attempting to 'drop' (remove the column from our data frame).
	- `axis`: `0 (default)` - drops row/ "index"  /`1` - drops columns
	- `index`: \[`labels`\] - It is equivalent to `(labels, axis= 0)`, more useful when we deal with Multiindex data frames.
	- `columns`: \[`labels`\] - It is equivalent to `(labels, axis=1)`, more useful when we deal with Multiindex data frames.
	- `level`: `None` (default), `int` / `level name` - The level (in a hierarchical multiindex) from which the labels will be removed.
		- [Level](https://stackoverflow.com/questions/45235992/what-are-levels-in-a-pandas-dataframe#:~:text=The%20levels%20are%20parts%20of,(level)%20of%20our%20choice.): The column 'number' (like an index, but for columns) 
	- `inplace`: `False` (default) - returns a copy of the DataFrame; `True` - updates the data frame used to reference the function, and returns `None`.
	- `errors`: `'raise'` (default) - allow error reporting, `'ignore'` - suppress error and only existing labels are dropped.
		- Errors: KeyError - If any of the labels is not found in the selected axis.
- Example
```python
df = pd.DataFrame(np.arange(12).reshape(3, 4),
                   columns=['A', 'B', 'C', 'D'])
# Output:
#    A  B   C   D
# 0  0  1   2   3
# 1  4  5   6   7
# 2  8  9  10  11

df.drop(columns=['B', 'C']) # Same output as below
df.drop(['B', 'C'], axis=1) # Same output as above
# Output:
#    A   D
# 0  0   3
# 1  4   7
# 2  8  11

df.drop([0, 1]) # Specifies the index (row)
# Output:
#    A  B   C   D
# 2  8  9  10  11

# Multiindex data frame
midx = pd.MultiIndex(levels=[['lama', 'cow', 'falcon'],
                              ['speed', 'weight', 'length']],
                      codes=[[0, 0, 0, 1, 1, 1, 2, 2, 2],
                             [0, 1, 2, 0, 1, 2, 0, 1, 2]])
df = pd.DataFrame(index=midx, columns=['big', 'small'],
                   data=[[45, 30], [200, 100], [1.5, 1], [30, 20],
                         [250, 150], [1.5, 0.8], [320, 250],
                         [1, 0.8], [0.3, 0.2]])

# Output: 
#                 big     small
# lama    speed   45.0    30.0
#         weight  200.0   100.0
#         length  1.5     1.0
# cow     speed   30.0    20.0
#         weight  250.0   150.0
#         length  1.5     0.8
# falcon  speed   320.0   250.0
#         weight  1.0     0.8
#         length  0.3     0.2

df.drop(index=('falcon', 'weight'))

# Output:
#                 big     small
# lama    speed   45.0    30.0
#         weight  200.0   100.0
#         length  1.5     1.0
# cow     speed   30.0    20.0
#         weight  250.0   150.0
#         length  1.5     0.8
# falcon  speed   320.0   250.0
#         length  0.3     0.2

df.drop(index='cow', columns='small')

# Output:
#                 big
# lama    speed   45.0
#         weight  200.0
#         length  1.5
# falcon  speed   320.0
#         weight  1.0
#         length  0.3

df.drop(index='length', level=1) # At column NUMBER (level) = 1 not column label, which if we were to list it in a vector Series: [speed, weight, length, speed, weight, length, speed, weight, length], we want to drop all index called 'length'.

# Output:
#                 big     small
# lama    speed   45.0    30.0
#         weight  200.0   100.0
# cow     speed   30.0    20.0
#         weight  250.0   150.0
# falcon  speed   320.0   250.0
#         weight  1.0     0.8
```

------
### Op. Rename columns
``` python
df.rename(columns={'old_name_0': 'new_name_0', ..., 'old_name_n':'new_name_n'})
```
- Renames specified columns specified by the key-value pair in the dictionary, which are just the old-new names to be updated respectively. 
- Because names might be too complex, long, ....
------
### Op. Drop N/A (not accessed) rows/columns
``` python
df.dropna(axis= 0, how= "any", thresh= None, subset= None, inplace= False)
```
- Arguments:
	- `axis`: `0 (default)` - row or `1` - column
	- `how`: `any (default)` - drops the row/ column if any of the values is `NA` or `all` - drops the row/ column if all of the values are `NA`.
	- (optional) `thresh`:  `None` (default) an integer value to specify the threshold count for the drop operation.
	- (optional) `subset`: `[]` An array of column name(s)/ label (s) where found `NA` are dropped.
	- `inplace`: `True` (data frame used to reference the function will be updated in place) or `False` (default) ( data frame used to reference the function will not be updated)
- [Examples](https://www.digitalocean.com/community/tutorials/pandas-dropna-drop-null-na-values-from-dataframe)
```python
d2 = {
'Name': ['Shark', 'Whale', 'Jellyfish', 'Starfish', pd.NaT],
'ID': [1, 2, 3, 4, pd.NaT],
'Population': [100, 200, np.nan, pd.NaT, pd.NaT],
'Regions': [1, None, pd.NaT, pd.NaT, pd.NaT],
'Endangered': [pd.NaT, pd.NaT, pd.NaT, pd.NaT, pd.NaT]
}

df2 = pd.DataFrame(d2)

# Output:
#     Name        ID     Population  Regions Endangered
# 0   Shark        1      100           1        NaT
# 1   Whale        2      200          None      NaT
# 2   Jellyfish    3      NaN          NaT       NaT
# 3   Starfish     4      NaT          NaT       NaT
# 4   NaT         NaT     NaT          NaT       NaT

########################################################################
# The code snippet below should not be run in sequence. Pretend it is
# run right after creating the DataFrame above, to see accurate output.
########################################################################
dfresult = df1.dropna()
# Exp: removes rows with missing value type - `None`, `NaN`, `NaT`. Since all rows has at least 1 missing value, no rows are generated.

# Output:
#     Name        ID     Population  Regions Endangered

dfresult = df1.dropna(axis=1)
# Exp: removes columns with missing value type - `None`, `NaN`, `NaT`. Since all columns has at least 1 missing value, no rows are generated.

# Output:
#     
# 0   
# 1   
# 2   
# 3   
# 4  

dfresult = df2.dropna(how='all')
# Exp: removes rows with all values being a missing value type - `None`, `NaN`, `NaT`. 

# Output:
#     Name        ID     Population  Regions Endangered
# 0   Shark        1      100           1        NaT
# 1   Whale        2      200          None      NaT
# 2   Jellyfish    3      NaN          NaT       NaT
# 3   Starfish     4      NaT          NaT       NaT

dfresult = df2.dropna(thresh=3)
# Exp: Removes any rows that DOES NOT have at least 3 non-NA

# Output:
#     Name        ID     Population  Regions Endangered
# 0   Shark        1      100           1        NaT
# 1   Whale        2      200          None      NaT

dfresult = df2.dropna(subset=['Population'])
# Exp: Removes any rows with missing value type - `None`, `NaN`, `NaT`, at column - 'Population'.

# Output:
#     Name        ID     Population  Regions Endangered
# 0   Shark        1      100           1        NaT
# 1   Whale        2      200          None      NaT

dfresult = df2.dropna(subset=[1, 2], axis=1)
# Exp: Removes any columns with missing value type - `None`, `NaN`, `NaT`, at row INDEX 1, 2

# Output:
#     Name        ID     
# 0   Shark        1     
# 1   Whale        2     
# 2   Jellyfish    3     
# 3   Starfish     4     
# 4   NaT         NaT    

df2.dropna(inplace=False)
df2
# Exp: After removing, DO NOT update df2 which is used to reference the function

# Output:
#     Name        ID     Population  Regions Endangered
# 0   Shark        1      100           1        NaT
# 1   Whale        2      200          None      NaT
# 2   Jellyfish    3      NaN          NaT       NaT
# 3   Starfish     4      NaT          NaT       NaT
# 4   NaT         NaT     NaT          NaT       NaT

df2.dropna(inplace=True)
df2
# Exp: After removing, update df2 which is used to reference the function

# Output:
#     Name        ID     Population  Regions Endangered

```

-----
### Op. Unit conversion (string -> datetime64)
```python
pd.to_datetime(df['data_col_name'])
```
- Type cast the column from 'object' to 'datetime64' data type.

-----
### Op. Unit conversation (string -> int64)
``` python 
pd.to_numeric(df['string_integers'])
```
- Type cast the column from 'string' data type to 'int64' data type.

