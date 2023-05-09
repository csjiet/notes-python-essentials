# Arrays
## Iterating two arrays simultaneously
> zip() function
> 	- It takes n distinct iterables, and iterate each element from n separate iterable in order, and place each n elements from n separate iterables in a tuple.
```python
# Use the zip() function
import itertools

num = [1, 2, 3]
color = ['red', 'while', 'black']
value = [255, 256]

# iterates over 3 lists and executes
# 2 times as len(value)= 2 which is the
# minimum among all the three
for a, b, c in zip(num, color, value):
	print(a, b, c)
```
Output: *Notice 3 and 'black' is omitted because value array has only 2 values*
>1 red 255
  2 while 256


-----------
## Convert two arrays to an array with x, y value pairs
> .T numpy transpose
```python
x = np.array([-1, 0, 1, 2])
y = np.array([-2, -1, 0, 1])

np.array((x,y))

''' Output
array([[-1,  0,  1,  2],
       [-2, -1,  0,  1]])

Notice this is a numpy array
'''

np.array((x,y)).T

''' Output
array([[-1, -2],
       [ 0, -1],
       [ 1,  0],
       [ 2,  1]])

Notice this is a numpy array
'''
```

> zip()
```python
zip(x,y)

''' Output
[(-1, -2), (0, -1), (1, 0), (2, 1)]

Notice, this is a normal python list
'''
```


## Indexing and Slicing in Python lists, numpy, pandas

**Indexing**: Accessing 1 element of an iterable.
**Slicing**: Accessing a subset of elements from an iterable.
**Extracting**: Pull out one column or row

Source: https://towardsdatascience.com/the-basics-of-indexing-and-slicing-python-lists-2d12c90a94cf

Indices and reverse indices

We will use the illustration below as our actual example
![[indexing_in_python.png]]

-----
Indexing syntax:
```python
the_list = ['a','b','c','d','e','f','g','h','i']
```

```python
the_list[index]
```
Slicing syntax:
```python
the_list[start_close_interval_index: stop_open_interval_index]
```
 - It uses a "half-closed interval" (an interval in which one endpoint is included but not the other) denoted by [a, b) or (a,b].

Extracting syntax:
```python
the_list[start_close_interval_index: ,column_to_extract]
```
- Simple example:https://stackoverflow.com/questions/9972391/python-array-slice-with-comma 

--------

 Examples
```python
the_list[5:]

# Output: ['f', 'g', 'h', 'i']

the_list[:4]

# Output: ['a', 'b', 'c', 'd']
```
- A "stepping" optional argument in slicers
```python
my_list[::2]

# Output: ['a', 'c', 'e', 'g', 'i']

my_list[1::2]
# Output: ['b', 'd', 'f', 'h']

# Negative slicer (reverse the direction in which the slicer iterates through the original list)
my_list[::-1]

# Output:['i', 'h', 'g', 'f', 'e', 'd', 'c', 'b', 'a'] 

my_list[5:3:-1]

# Output: [‘f’, ‘e’]

my_list[-2:-5:-1]

# Output:['h', 'g', 'f'] 

my_list[-1:-8:-3]

# Output:['i', 'f', 'c'] 

```

Example for extracting
```python
my_list = [[5,2,1,0],[-2,3,9,2],[3,1,4,-2],[6,1,3,3]]

my_list[::2]
# Output:array([[ 1, 4, -2],[ 1, 3, 3]]) 
```

Numpy slicing - [[Slicing numpy array]]


Broadcasting a function to all elements in a numpy array/ list:

```python
import numpy as np
data = np.array([[1,2,3,4,5], \
				 [6,7,8,9,10]])

my_func = lambda x: x*2

my_func(data)

# Output
'''
array([[ 2,  4,  6,  8, 10],
       [12, 14, 16, 18, 20]])
'''

```