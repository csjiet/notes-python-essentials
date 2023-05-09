# Syntax:
```python
array_identifier[start: stop: step, ...]
```
- `start`: The 
- `stop`: 
- `step`: From the 0th item, store every item which is 3 strides away (left to right)
- `, ...` : By default, the process of indexing starts from the first element in the first axis ( e.g.: in 2D: the first row), each '`,`' specifies the indexing of the next axis (e.g.: in 2D: there are two axis - the rows, then columns).

> The `start`, `stop`, `step` sequence ALWAYS follow the "subsequent" sequence which is LEFT to RIGHT, hence, any start without specifying stop or step will continue to retrieve every element to the right before terminating the slice. (See example below with negative indexing)

## Slicing 1D numpy array
```python
import numpy as np
arr = np.array([1,2,3,4,5,6,7,8,9,10])
```

- **Stepping**
```python
arr[::3]
# Output:
# [ 1,  4,  7, 10]
```

## Slicing 2D numpy array
- ### '`,`'(comma)
	- All indexing starts from the first element, of the first axis. So how do we know where to index as the dimension of our array increase? Solution: '`,`' (comma), where the indexing syntax: `start: stop: step`  stated to the right of the '`,`' (comma) denotes indexing of the subsequent axis.
	- The reason it is brought up in this section is because array >1D dimension will have >1 axis.
	- [numpy array Axes](https://www.sharpsightlabs.com/blog/numpy-axes-explained/) for refresher.

- Extracting 1 element from a 2D array
```python
import numpy as np
arr = np.array([1,2,3,4,5], [6,7,8,9,10])
# Numpy method
arr[1,2]
# Output:
# 8

# OR

# Conventional method
arr[1][2]
# Output:
# 8
```

- Comma extracting >1 elements
```python
import numpy as np
arr = np.array([[1,2,3,4,5], [6,7,8,9,10]])
# Numpy method

########### Example 1 ###########
arr[0:1, 1:3]
# Output:
# [[2,3]] 

'''
# Explaination:

We start indexing at the first element in the first axis of dimension. (in 2D: 0th element (1), at axis 0 - 0th row ([1,2,3,4,5])), each ',' denotes the specification of the indexing in the next axis.

- arr[0:1
in axis 0 - which are elements '[1,2,3,4,5]','[6,7,8,9,10]', we want to index 0:1 , starting from 0th index, ends at index excluding 1 - which is element [1,2,3,4,5].

- ,1:3]
in axis 1 - which are elements '1', '2', '3', '4', '5', we want to index 1:3 , starting from the 1st index, ends at index excluding 3 - which are elements '2', '3'

Hence the output: 
[[2,3]]
'''

########### Example 2 ###########
arr[0:2, 1:3]
# Output:
# [[2,3]
#  [7,8]]	

########### Example 3 ###########
### Negative indexing
arr[:,-1:] # Get the last column

'''
# output:
array([[5],
	   [10]
])
'''

########### Example 4 ###########
arr[:,-2:]

'''
# output:
array([[4,5],
	   [9,10]
])

Notice the negative indexing starts from the "second last" column, AND takes everything to the RIGHT. Because it always uses a LEFT to RIGHT direction
'''
```

## Slicing 3D numpy array
```python
```

## Slicing nD numpy array
```python
```