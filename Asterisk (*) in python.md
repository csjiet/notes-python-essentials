Resources:
- https://peps.python.org/pep-3132/

1. [Iterable unpacking syntax](https://peps.python.org/pep-3132/)

## Iterable unpacking: iterables
- Examples are from: [Stack abuse](https://stackabuse.com/unpacking-in-python-beyond-parallel-assignment/)
```python
a, *b, c = range(5)
print(a)
# Outputs:
# 0
print(c)
# Outputs:
# 4
print(b)
# Outputs:
# [1, 2, 3]

# Example 2: 
a, *b = 1, 2, 3 
print(a)
# 1 
print(b)
# [2, 3]

# Example 3: 
*a, b = 1, 2, 3 
print(a)
# [1,2]
print(b)
# 3

# Example 4: 
*a, b, c = 1, 2, 3 
print(a)
# [1]
print(b)
# 2
print(c)
# 3

# Example 4: 
*a, b, c, d = 1, 2, 3
print(a)
# []
print(b)
# 1
print(c)
# 2
print(d)
# 3
```
- Caveat:
	- An error to use the starred expression as a lone assignment target
		```python
		*a = range(5) # Error
		```
		- Valid syntax `*a, = range(5)`.
			```python
			*a , = 1, 2 
			print(a)
			
			# Output:
			# [1, 2]
			```
	- An error
		```python
		*a, b, c, d, e = 1, 2, 3
		# ValueError: not enough values to unpack (expected at least 4, got 3)
		```

## Iterable unpacking: Keyword arguments
- Recall keyword arguments (``**kwargs`)
> Keyword arguments: Function arguments that has to be assigned explicitly when invoked.

- Simple example (non-unpacking)
```python
def team(name, project):
	print(name, project)

team(project = "Edpresso", name = 'FemCode')

# Output:
# FemCode Edpresso
```

- Harder examples (unpacking)
	- Unpacking: Mapping arguments automatically.
```python
# --------------------------------------------
# Valid example 1:
# When unpacking keyword arguments in a function, the key will match the variable identifiers of function arguments!
kvp = {"data1": 1, "data2": "2", "data3": 5}

def foo(data1, data2, data3):
    print(data1, data2, data3)

foo(**kvp)
# Output:
# 1 2 5

# Error example 1:
kvp = {"data1": 1, "data2": "2", "data3": 5}

def foo(data10, data2, data3):
    print(data10, data2, data3)

foo(**kvp)
# TypeError: foo() got an unexpected keyword argument 'data1'

# --------------------------------------------
# Valid example 2:
kvp = {"data1": 1, "data2": "2", "data3": 5}

def func(**var):
    print(var)

func(**kvp)
# Output:
# {'data1': 1, 'data2': '2', 'data3': 5}
```

- Placeholding keyword arguments
```python
# Valid example 1, 2
def foo2(data1, data2, data3,**datas):
    print(data1, data2, data3, datas)
    
def foo3(data1, data2, data3,**_):
    print(data1, data2, data3)
    
kvp2 = {"data1": 1, "data2": 2, "data3": 3, "data4": 4}

foo2(**kvp2)
# Output
# 1 2 3 {'data4': 4}

foo2(**kvp2)
# Output
# 1 2 3
```

