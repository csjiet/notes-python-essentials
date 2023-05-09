`np.append(arr1, values, axis = None)`

Rules:
- '`arr1`'  and '`values`' should be the same shape

Parameters:
- `axis = None/ int`
	- `None`: If axis is not given, BOTH arr and values are flattened before use.


```python
# axis not specified
np.append([1, 2, 3], [[4, 5, 6], [7, 8, 9]])

# Output
# array([1, 2, 3, ..., 7, 8, 9])


# axis specified
np.append([[1, 2, 3], [4, 5, 6]], [[7, 8, 9]], axis=0)

'''
Output
array([[1, 2, 3],
       [4, 5, 6],
       [7, 8, 9]])
'''

np.append(np.arange(8).reshape(2,4), np.arange(8,16).reshape(2,4), axis=1)
'''
2D arr1 : 
 [[0 1 2 3]
 [4 5 6 7]]
Shape :  (2, 4)

2D arr2 : 
 [[ 8  9 10 11]
 [12 13 14 15]]
Shape :  (2, 4)

Appended arr3 with axis 1 : 
 [[ 0  1  2  3  8  9 10 11]
 [ 4  5  6  7 12 13 14 15]]
'''
```


