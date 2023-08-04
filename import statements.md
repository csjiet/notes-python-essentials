Depending on how you `import` modules, it will propagate the python namespace differently.
> Namespace: a container that holds a collection of names (identifiers) and associates them with corresponding objects or values. It provides a way to organize and differentiate names to avoid naming conflicts and to provide a unique context for each name.

What is the difference between files vs modules?
- Files and modules are the same thing, it is just that one is the subset of the other.
## File`.py`(s) $\subseteq$ Module
- Python module $\approx$ Directory
	-  A "module" (instead of a "directory") = a collection of files (`.py`) 
	- Module -> multiple Files - class/ functions/ variables only 
	- A `.py` file can either have: Variables only, Functions only, class
```python
# Variables only
###################################
# Untitled.py
var_a = "IMPORT STATEMENT failed!"
###################################

# Functions only
###################################
# Untitled.py
def error_func1():
	return "IMPORT STATEMENT failed!"
	
def error_func2():
	return "SYNTAX ERROR!"
###################################

# Class 
###################################
# Untitled.py
class ErrorClass:
	def __init__(self):
		self.flag_1 = 0
		self.flag_2 = 0
		
	def error_func1():
		if self.flag_1 = 1:
			return "IMPORT STATEMENT failed!"
###################################
```

# Importing module/ Importing multiple files
- Since modules are just the superset of files.
## `import {module}` vs `from {module} import *`
- ## `import {module}`
	- Imports the entire module into the current namespace, which means you can access the objects (fields, functions) ONLY AFTER prefixing them with the module name.
```python
import math

print(math.pi)
print(math.sqrt(25))
```

- ## `from {module} import *`
	- Imports objects within the module into the current namespace, which means you can access the objects (fields, functions) without using the module name as prefix.
	- This is DISCOURAGED because:
		- namespace pollution: Importing objects from the module instead of the module, may introduce naming conflicts - same name in multiple modules.
		- Uncertainty of code origin: Because it can be referred by object names directly, it will be less readable or cause unexpected behavior from conflicting invocation of objects.
	- ENCOURAGED code: 
		- `from {module} import {object_alias}, {object_alias}...`
		- Allowed because of its readability and clarity.
		- This occurs when you only want a few items from a module/ package.
		- E.g., `from math import pi, sqrt`
```python
from math import * # DISCOURAGED import statement

print(pi) # called directly without module name as prefix
print(sqrt(25))
```
```python
from math import pi, sqrt # encouraged 

print(pi) # called directly without module name as prefix
print(sqrt(25))
```

