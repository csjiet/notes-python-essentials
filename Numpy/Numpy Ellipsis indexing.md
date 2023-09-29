Ellipsis (`...`) : array slicing operation.
``` python
import numpy as np

# Example 1: Simple example
x = np.array([
    [ 0, 1, 2, 3],
    [ 4, 5, 6, 7],
    [ 8, 9, 10, 11]])
    
# The below is equivalent to x[:,0] in slicing
print(x[...,0]) 
'''
Output: 
[0 4 8]
'''

# Example 2: Complex example
x = np.array(
[[[[1,2],
   [3,4]],

  [[5,6],
   [7,8]]],

 [[[9, 10],
   [11, 12]],

  [[13, 14],
   [15, 16]]]]
)
print(x.shape) # (2, 2, 2, 2)

# The below is equivalent to - x[:, :, :, 0] during slicing
print(x[..., 0]) 

'''
Output: 
[[[ 1 3] 
  [ 5 7]] 
  
  [[ 9 11] 
  [13 15]]]
'''
```

