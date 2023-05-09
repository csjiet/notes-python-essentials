
### Making a horizontal vector to a vertical vector - `arr.reshape()`
```python
'''
It seems transposing is the way to go
However, transposing a vector using conventional
'.T' or 'np.transpose()' DOES NOT SEEM TO MANIFEST THE INTENDED EFFECT

Where we want vector 
[1,2,3]
to become:
[[1],
 [2],
 [3]]
'''

# Solution - .reshape({shape})
import numpy as np
arr = np.array([1,2,3])

arr.reshape((3,1))

'''
# Output: 
array([[1],
	   [2],
	   [3]])
'''
```