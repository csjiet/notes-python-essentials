Understanding its operation can help us identify whether it can be useful in certain scenario to save computational time.

# Properties:
1. **Dot product**: Vector multiplication/ Matrix multiplication
	1. **Dot product for Vector multiplication constraints**:
		1. Vector must be the same length
	2. **Dot product for Matrix multiplication constraints**:
		1. Number of columns of the first matrix/ array matches Number of rows in the second matrix/ array.
		2. ***DOT PRODUCT CAN TAKE IN MATRICES. BUT BEHAVIOR WITH MATRICES WITH DIMENSION >2, DOES NOT RESULT IN THE CORRECT/ EXPECTED RESULT OF A MATRIX MULTIPLICATION OPERATION.***
2. Numpy operation for dot product: `a @ b` = `np.dot(a,b)`

# Operation in math:
$$
Test
$$

# Syntax for dot product of two vectors/ matrices (arrays):
```python
res = np.dot(arr1, arr2)

res = arr1.dot(arr2)
```

# Examples:
- ### Dot product of vectors 
	- Sum of the product
```python
import numpy as np

a = np.array([1,2,3,4])
b = np.array([1,2,3,4])

res = np.dot(a,b)
print(res)

# Output:
# (1*1) + (2*2) + (3*3) + (4*4)
# 1 + 4 + 9 + 16
# 30 # Scalar
```

- ### Dot product of matrices (NOT RECOMMENDED FOR MATRIX MULTIPLICATION)- See: link to another noteeeeee 
	- Sum of the product 
```python
import numpy as np
a = np.array([[1,1,1,1],
			  [0,0,0,0],
			  [1,1,1,1],
			  [1,1,1,1]
			 ])
b = np.array([[1,1,1,1],[1,1,1,1]]).T

##### OPTION 1 #####:
res = np.dot(a,b)
print(res)

# Output:
'''
[
	[1*1 + 1*1 + 1*1 + 1*1], [1*1 + 1*1 + 1*1 + 1*1],
	[0*1 + 0*1 + 0*1 + 0*1], [0*1 + 0*1 + 0*1 + 0*1],
	[1*1 + 1*1 + 1*1 + 1*1], [1*1 + 1*1 + 1*1 + 1*1],
	[1*1 + 1*1 + 1*1 + 1*1], [1*1 + 1*1 + 1*1 + 1*1]
]
'''
'''
array([[4, 4],
		[0,0],
		[4,4],
		[4,4],
]])
'''

##### OPTION 2 #####:
res = a @ b

print(res)

# Output:
'''
array([[4, 4],
		[0,0],
		[4,4],
		[4,4],
]])
'''
```