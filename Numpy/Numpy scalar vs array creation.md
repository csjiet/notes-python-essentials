
Numpy arrays deals with arrays of all dimensions, including scalars (0 dimension)

Scalars = 0-D arrays
```python
import numpy as np  
arr = np.array(42)  
print(arr)
```

- 0-dimensional array or scalar value may not conform to the strict definition of an array as a sequence of homogeneous items with a fixed size, but it comes with useful properties:
- For example, it can be used to:
	- represent a single value that needs to be broadcasted to other arrays of larger dimensions during mathematical operations, or 
	- to handle cases where a single value needs to be treated as an array for consistency in function signatures or API conventions.
	- Have better control of dtypes in scalars.

1-D arrays
```python
import numpy as np  
arr = np.array([1, 2, 3, 4, 5])  
print(arr)
```

- It is imperative that we specify the dimension using square brackets `[`, `]` when defining a >1-D array.