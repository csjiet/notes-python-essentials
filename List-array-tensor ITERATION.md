# List
### Iterating one list
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
### Iterating >1 lists
- **Zip** (iterating >1 list)
```python
for x, y in zip(list_1, list_2):
	print(x,y)
```
### List -> Operation -> List
- **List comprehensions**
> Use case: Make a new list by applying operations to elements in an existing list
```python
new_list = [func(x) for x in list_1]
```

# Numpy array
> All list iteration operations above can be applied to numpy! 

This includes:
- loop - element-wise, index-wise
- list comprehension
- enumerate
- iterator
- zip

### Array -> Operation -> Array 
> ***A list comprehension (one-liner) equivalent - but faster!***
- Direct operation! - FASTEST! - use arithmetic operation on numpy array
``` python
x = np.array([1,2,3])

>> y = x ** 2
# [1 4 9]
```
- Direct function! - numpy array as argument 
``` python
x = np.array([1,2,3])

func1 = lambda j: j**2
>> func1(x)
# [1 4 9]
```
> The operation cannot be done if we are using a`list`. Example error: `TypeError: unsupported operand type(s) for ** or pow(): 'tuple' and 'int'`.

# Pytorch Tensor