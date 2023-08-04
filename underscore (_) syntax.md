Resources:
- [Naming with underscores in python](https://medium.com/python-features/naming-conventions-with-underscores-in-python-791251ac7097#:~:text=The%20underscore%20prefix%20is%20meant,is%20intended%20for%20internal%20use.)
- [Descriptive: Naming Styles, pep8](https://pep8.org/#descriptive-naming-styles)

Types:
- Single underscore
	- Standalone underscore: `_`
	- Leading single underscore: `_var`
	- Trailing single underscore: `var_`
- Double underscore
	- Leading double underscore: `__var`
	- Leading AND trailing double underscore: `__var__`

# Single underscore
1. `_`: empty variable (==Standalone single underscore==)
- Can be assigned by a value syntactically, but it is not stored in memory and cannot be retrieved. 
	```python
	# Valid for any variables in python
	
	# Example 1: Normal code 
	def my_method(var):
		return 1, 2, 5
	a, _ , _ = my_method(var_1) # you only want the first value
	print(a)
	
	# Example 2: Loops with local variable
	for _ in range(10):
		print("Test")
	```

2. `var_`: Avoids conflicts with python keywords (==Trailing single underscore==)
- [Python keyword examples](https://www.w3schools.com/python/python_ref_keywords.asp): `class`, `lambda`, `pass`, `return`, `yield`
	```python
	class_ = "Dog"
	```

3. `self._var/ _func()`: Declaring "weak-private variables" and "weak-private functions". (==Leading single underscore==)
> "Weak" because there are available workarounds to access BOTH "weak-private variables" and "weak-private functions". 

- "Weak-private" variables 
	- can be used: In any case. 
	```python
	# private fields
	class Python: 
		def __init__(self): 
			self.fee = 37 
			self._buzz = 76 # weak private variable
	obj = Python()
	print(obj._buzz)
	
	# Output:
	# 76
	```
- "Weak private functions" 
	- cannot be used: IF it "imports objects from module".  
	- can be used: IF it "imports module".
	- Difference between "import objects from module" vs "import module" - [[import statements]]
		- Assume: External file
		```python
		###########################################
		# Untitled.py
		def function(): 
			return "programming" 
			
		def _private_function(): 
			return 35
		
		###########################################
		```
		1. Import objects from module
		```python
		###########################################
		# main.py
		from Untitled import *
		
		_private_function() # Error
		
		# Traceback (most recent call last):
		# File "<stdin>", line 1, in <module>
		# NameError: name '_private_function' is not defined
		###########################################
		```
		2. Import module
		```python
		###########################################
		# main.py
		from Untitled 
		
		Untitled._private_function() 
		
		# Output
		# 35
		###########################################
		
		```

# Double underscore

1. `__var`: Names that will be "mangled" by the interpreter into a unique identifier. (==Leading double underscore==)
	- "mangle" (English): mutated/ disfigured into another form
	- _name mangling_ (Python) — the interpreter changes the name of the variable in a way that makes it harder to create collisions when the class is extended later.
		```python
		class Person:  
			def __init__(self):  
				self.name = 'Sarah'  
				self._age = 26  
				self.__id = 30
		
		p = Person()
		print(p.__id) # Error
		# AttributeError: 'Person' object has no attribute '__id'
		
		
		print(p._Person__id) # self.__id is name mangled to self._Person__id
		# Output:
		# 30
		```
		- In the example above: `__id` is mangled to `_Person__id`.
		- This is the _name mangling_ that the Python interpreter applies. It does this to protect the variable from getting overridden in subclasses.
2. `__var__`:  (==Leading AND trailing double underscores==)
- Read: [Medium: Naming with underscores in Python](https://medium.com/python-features/naming-conventions-with-underscores-in-python-791251ac7097#:~:text=The%20underscore%20prefix%20is%20meant,is%20intended%20for%20internal%20use.)



