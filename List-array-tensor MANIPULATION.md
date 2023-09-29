Resources:
- [NumPy: Array manipulation routines](https://numpy.org/doc/stable/reference/routines.array-manipulation.html#)

Manipulation = changing array shape/ array morphology


# List


# NumPy array
### Shallow copy (default)
> ==Note==: Every numpy array assignment is a ***shallow copy*** . Assigning an object with shallow copy = assigning a new variable that references the same objects as the original. 
> - It is "***shallow***" in the sense that it doesn't go deep into the objects within the original data structure to copy each element within the array into a new location.
``` 
# Example of how shallow copy can be problematic 
x = np.array([
    [ 0, 1, 2, 3],
    [ 4, 5, 6, 7],
    [ 8, 9, 10, 11]])

print(x)
'''
Output:
[[ 0 1 2 3] 
 [ 4 5 6 7] 
 [ 8 9 10 11]]
'''

y = x
x[0][0]=999 # making changes to x

print(y) # also changes y
'''
Output:
[[999 1 2 3] 
 [ 4 5 6 7] 
 [ 8 9 10 11]]
'''
```

### Deep copy
To **deep copy** an array we can use: 
```python
y = np.copy(x)
# OR
y = x.copy()
```

#### ==Note: ALL Numpy functions can be called in two ways. Either as a function of module or array object.==
> 1. **Functional-style call**: `x = np.reshape(x, (2,3))`
> 	- **Benefits**:
> 		1. NumPy operations can be applied on `list` or `numpy.ndarray` 
> 1. **Method-style call**: `x = x.reshape(2,3)` 
> 	- **Benefits**:
> 		1. Reads like an operation performed on an object.
> 		2. More concise
> 		3. Allows sequential operations: e.g.,`a = np.arange(6).reshape((3, 2))` 

> Below we assume we will only be dealing with operations on NumPy arrays: Hence, we'll use "***method-style calls***". 

### Flexible reshapes (final shape has to be specified)
- ##### `.reshape()/ np.reshape()`
	- Parameters:
		- `{tuple_shape}`
``` python
x = np.array([1,2,3,4,5,6])
x = x.reshape((2,3)) 
# same as:
# x = np.reshape(x, (2,3))
print(x)
```
- Special reshapes:
	- `.reshape(-1)`: Flattens ndarray

### Known reshapes (don't need to specify final shape)
> Example fixed shapes:
> - flat
> - transpose

- ##### `.ravel()/ np.ravel()` ``: 
Use: Returns a SHALLOW COPY of flattened array. (no new memory is created) 
> How to remember?: `r`avel = pass by `r`eference/ copy only `r`eference/ shallow copy.
``` python
x = np.array([
    [ 0, 1, 2, 3],
    [ 4, 5, 6, 7],
    [ 8, 9, 10, 11]])

y = x.ravel() # Shallow copy
print(y)

'''
Output:
[ 0 1 2 3 4 5 6 7 8 9 10 11]
'''

y[0] = 999

print(x)
'''
Output:
[[999 1 2 3] 
 [ 4 5 6 7] 
 [ 8 9 10 11]]
'''
```
> Notice a change to the shallow copied array also changes the original array (they are of the same reference) 

- ##### `.flatten()/ np.flatten()`:
Use: Returns a DEEP COPY of flattened array.  (new memory is created)
``` python
x = np.array([
    [ 0, 1, 2, 3],
    [ 4, 5, 6, 7],
    [ 8, 9, 10, 11]])

y = x.flatten() # Deep copy
print(y)
'''
Output:
[ 0 1 2 3 4 5 6 7 8 9 10 11]
'''

y[0] = 999

print(x)
'''
Output:
[[ 0 1 2 3] 
 [ 4 5 6 7] 
 [ 8 9 10 11]]
'''
```

- ##### `.T`
> `.T` basically just flips the shape sequence around.
```python
# Example 1
x = np.array([
    [ 0, 1, 2, 3],
    [ 4, 5, 6, 7],
    [ 8, 9, 10, 11]])
print(x.shape) # Output: (3, 4)
x = x.T
print(x.shape) # Output: (4, 3)

# Example 2
x = np.arange(24).reshape((2,3,1,4))
print(x.shape) # Output: (2, 3, 1, 4)
x = x.T
print(x.shape) # Output: (4, 1, 3, 2)
```

- ##### `.transpose()`/ `np.transpose()`
	- Parameters:
		- `axes` - (tuple/ list/ ints) to interchange existing elements in a dimension to another dimension.
> `.transpose()` can specify which dimension is swapped.

> Tip: `.transpose` is sufficient to compute`.moveaxis()`, `rollaxis()`, `swapaxes()` operations, and provides more comprehensive control of axis/ dimension movement.

```python
x = np.array([
    [ 0, 1, 2, 3],
    [ 4, 5, 6, 7],
    [ 8, 9, 10, 11]])

x = x.transpose()
print(x)

'''
Output:
[[ 0 4 8] 
 [ 1 5 9] 
 [ 2 6 10] 
 [ 3 7 11]]
'''

# Example 2
a = np.arange(6).reshape((1,2,3))
print(a)
'''
Output:
[[[0 1 2] 
  [3 4 5]]]
'''
print(a.shape)
'''
Output:
(1, 2, 3)
'''
a = np.transpose(a, (1, 0, 2))
'''
- "Dimension 1 (axis 1)" should become the new first dimension.
- "Dimension 0 (axis 0)" should become the new second dimension.
- "Dimension 2 (axis 2)" remains as it is.
'''
print(a)
'''
Output:
[[[0 1 2]] 
  [[3 4 5]]]
'''
print(a.shape)
'''
Output:
(2, 1, 3)
'''
```

- ##### `.squeeze()/ np.squeeze()`
Eliminates axes of length 1.
``` python
# Example 1
y = np.ones((1,2,2))
print(y.shape)
'''
Output:
(1,2,2)
'''
y = y.squeeze()
print(y.shape)
'''
Output:
(2,2)
'''

# Example 2
y = np.ones((1,2,2,1,1,3))
print(y.shape)
'''
Output:
(1,2,2,1,1,3)
'''
y = y.squeeze()
print(y.shape)
'''
Output:
(2,2,3)
'''
```
# Tensor