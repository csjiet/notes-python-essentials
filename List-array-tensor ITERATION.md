# List
### 1. Iterating one list
- **Loops**
```python
# Element-wise iteration 
for x in list_1:
	print(x)

# Index-wise iteration 
# (Read about "enumerate" with more elegant syntax)
for i in range(len(list_1))
	print(list_1[i])
```
- **Enumerate**
> Use case: Iteration requires tracking/ access to index
```python
for idx, x in enumerate(list_1):
	print(idx, x)
```
- **Iterator** (`<class 'iterator'>`)
> Use case: Usually for more minute control flow
> - Batch processing, 
> - Non-standard sources like sensor inputs, files or network streams, 
> - Create custom iterators to process the data as it arrives or is read, improve efficiency where elements are computed or fetched only when they're needed, 
> -  Concurrent or parallel programming, distribute tasks among workers
> - Python's generator functions use the `yield` keyword to create iterators that produce values on-the-fly.
```python
iter1 = iter(list1)
# next() function to return the next item in an iterator.
while True:
	try:
		item = next(iter1)
	except StopIteration:
		break

# Loop on iterator
for x in iter1:
	print(x)
```
### 2. Iterating >1 lists
- **Zip** (iterating >1 list)
```python
for x, y in zip(list_1, list_2):
	print(x,y)
```
### 3. List -> Operation -> List
- **List comprehensions**
> Use case: Make a new list by applying operations to elements in an existing list
```python
new_list = [func(x) for x in list_1]
```

------
# Numpy array
> ***All `list` operations above can be applied to `NumPy`!***

### 1. Same operations as lists
- **loop** - element-wise, index-wise
- **list comprehension**
- **enumerate**
- **iterator**
- **zip**

### 2. Array -> Operation -> Array 
> A list comprehension (one-liner) equivalent - but faster!
- ##### Direct operation!
	- FASTEST! - use arithmetic operation on numpy array
	- Can also be applied on a `matrix`.
``` python
x = np.array([1,2,3])

>> y = x + 2
# [2 3 4]
```
- ##### Direct function!
	- numpy array as argument 
	- Can also be applied on a `matrix`.
``` python
x = np.array([1,2,3])

func1 = lambda j: j+2
>> func1(x)
# [2 3 4]
```
> If x is a `list` , it will be an ERROR 
> `TypeError: unsupported operand type(s) for ** or pow(): 'list' and 'int'`
> **Fun fact**: (`*` operation on list = list extension!) If x is a `list` applies on a `*` operation, `*` will be treated as a list extension operation e.g.,: `x = [1,2,3]; func1=lambda j: j*2; func1(x)` will result in an output `[1,2,3,1,2,3]`

- ##### Direct indexing! ==(This can give you infinite combination of operations on specific elements within an array)==
	- ***numpy array as index to another numpy array***
	- Using an array as index: `array[array]`, instead of Using an integer as index: `array[idx]`.
```python
# Example 1: Single-dimensional Indexing
x = np.array([0,0,0,0,0])

x[np.array([0,1,2])] = np.array([9,9,9])

print(x)
'''
Output:
[9. 9. 9. 0. 0.]
'''
###############################################
# Example 2: Multi-dimensional Indexing
x = np.zeros((4,4), dtype=np.int64)
print(x)
'''
Output:
[[0 0 0 0] 
 [0 0 0 0] 
 [0 0 0 0] 
 [0 0 0 0]]
'''
x[np.arange(4), np.arange(4)] = 1
print(x)
'''
Output:
[[1 0 0 0] 
 [0 1 0 0] 
 [0 0 1 0] 
 [0 0 0 1]]
'''
```

### 3. Iterating multidimensional arrays (without hassle of unpacking nested arrays)
Resources:
- [GeeksForGeeks: numpy.nditer() iterator object](https://www.geeksforgeeks.org/numpy-iterating-over-array/)
> Normal `loop` operation accesses nested arrays, which has to be further unpacked with nested loops.

- ##### n-dimensional ITERATOR": [Docs](https://numpy.org/doc/stable/reference/generated/numpy.nditer.html)
``` python
np.nditer(
	{array}, 
	order = {'C'/ 'F'/ 'K' }), # ordering of ndarray (Default: 'K' - as close to the order the array elements appear in memory as possible)
	op_flags = ['readwrite'/ 'readonly'/ 'writeonly'] # operations allowed (Default: readonly)
```
- `nditer()` only allows readonly by default - no changes to array
``` python
x = np.array([
    [ 0, 1, 2, 3],
    [ 4, 5, 6, 7],
    [ 8, 9, 10, 11]])

# Example 1: Default ordering during reading
# Order of iteration is chosen to match the memory layout of an array, WITHOUT considering a particular ordering.
iter1 = np.nditer(x)
for j in iter1:
    print(j)
# OR
# for j in np.nditer(x):
#     print(j)
'''
Output: 
0 
1 
2 
3 
4 
5 
6 
7 
8 
9 
10 
11
'''
# Effects of default ordering
x = x.T # transpose
''' Matrix after transpose
[[ 0 4 8] 
 [ 1 5 9] 
 [ 2 6 10] 
 [ 3 7 11]]
'''
iter1 = np.nditer(x):
for j in iter1:
    print(j)

# Since array was originally row-wise ordering (C). Iteration order will be row-wise.
'''
Output: 
0 
1 
2 
3 
4 
5 
6 
7 
8 
9 
10 
11
'''

# Example 2: Control ordering - C (C ordering), F (Fortran ordering) during reading
iter1 = np.nditer(x, order = 'F')
for j in iter1:
    print(j)
'''
Output:
0 
4 
8 
1 
5 
9 
2 
6 
10 
3 
7 
11
'''

# ERROR Example 3: Writing to array without setting operation flag
iter1 = np.nditer(x, order = 'C')
for j in iter1:
    j[...] = j * 3 # Same as j[:,:] or j[:]
    # Meaning: Applies operation to all elements
    
'''
Output:
ValueError: assignment destination is read-only j[...] = j * 3
'''
```
> Read: [[Numpy Ellipsis indexing]]: `...`  as slicing operator for NumPy arrays.
- More arguments:
	- `nditer(op_flags = {['readwrite'/ 'readonly'/ 'writeonly']})`
``` python
x = np.array([
    [ 0, 1, 2, 3],
    [ 4, 5, 6, 7],
    [ 8, 9, 10, 11]])

# Example 1
iter1 = np.nditer(x, order = 'C', op_flags = ['readwrite'])

for j in iter1:
    j[...] = j * 3 
'''
Output:
[[ 0 3 6 9] 
 [12 15 18 21] 
 [24 27 30 33]]
'''

# Example 2: Allow write to occur at specific dimension
# E.g., This allows only the second dimension of index 1 to have 'readwrite' operations allowed. 
iter1 = np.nditer(x[:,1], order = 'C', op_flags = ['readwrite'])
for j in iter1:
    j[...] = j * 10
    
print(x)
# Notice operation only happens at the second dimension at column index 1
'''
Output: 
[[ 0 10 2 3] 
 [ 4 50 6 7] 
 [ 8 90 10 11]]
'''
```

------
# Pytorch Tensor