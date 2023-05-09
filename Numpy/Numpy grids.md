
`np.meshgrid()`

`np.mgrid[]`
```python
res = np.mgrid[0:5:6j,0:5:6j]
res

# Output
'''
array([[[0., 0., 0., 0., 0., 0.],
        [1., 1., 1., 1., 1., 1.],
        [2., 2., 2., 2., 2., 2.],
        [3., 3., 3., 3., 3., 3.],
        [4., 4., 4., 4., 4., 4.],
        [5., 5., 5., 5., 5., 5.]],

       [[0., 1., 2., 3., 4., 5.],
        [0., 1., 2., 3., 4., 5.],
        [0., 1., 2., 3., 4., 5.],
        [0., 1., 2., 3., 4., 5.],
        [0., 1., 2., 3., 4., 5.],
        [0., 1., 2., 3., 4., 5.]]])
'''

func = lambda x, y: x+y+1
np.array(list(map(func, res[0], res[1])))

# Output
'''
array([[ 1.,  2.,  3.,  4.,  5.,  6.],
       [ 2.,  3.,  4.,  5.,  6.,  7.],
       [ 3.,  4.,  5.,  6.,  7.,  8.],
       [ 4.,  5.,  6.,  7.,  8.,  9.],
       [ 5.,  6.,  7.,  8.,  9., 10.],
       [ 6.,  7.,  8.,  9., 10., 11.]])
'''

res[0] + res[1] + 2
'''
array([[ 2.,  3.,  4.,  5.,  6.,  7.],
       [ 3.,  4.,  5.,  6.,  7.,  8.],
       [ 4.,  5.,  6.,  7.,  8.,  9.],
       [ 5.,  6.,  7.,  8.,  9., 10.],
       [ 6.,  7.,  8.,  9., 10., 11.],
       [ 7.,  8.,  9., 10., 11., 12.]])
'''
```

`np.ogrid[]`
- `ogrid`: 
	- "open" grid is essentially the same as `mgrid`, but differ in the way of representation, where the grid is an "open" representation of the mesh grid, with minimal representation by removing repetitive values.
```python
res = np.ogrid[0:5:6j,0:5:6j]
res

# Output
'''
[array([[0.],
        [1.],
        [2.],
        [3.],
        [4.],
        [5.]]),
 array([[0., 1., 2., 3., 4., 5.]])]
'''

func = lambda x, y: x+y+1
np.array(list(map(func, res[0], res[1])))
'''
array([[1., 2., 3., 4., 5., 6.]])
'''

res[0] + res[1] + 2
'''
array([[ 2.,  3.,  4.,  5.,  6.,  7.],
       [ 3.,  4.,  5.,  6.,  7.,  8.],
       [ 4.,  5.,  6.,  7.,  8.,  9.],
       [ 5.,  6.,  7.,  8.,  9., 10.],
       [ 6.,  7.,  8.,  9., 10., 11.],
       [ 7.,  8.,  9., 10., 11., 12.]])
'''
# Notice when we compute arithmetic operations between generated open grid, it automatically broadcast the X,Y relation. This results in the same computation as seen above when arithmetic of mgrids are computed. This saves space complexity. (Given the resultant would be the same if map() function is not used, as the broadcasting feature would not be used.)

# RULE: Arithmetric operations between a column vector and a row vector will result in a grid.
```