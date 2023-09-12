Depending on how you `import` modules, it will propagate the python namespace differently.
> Namespace: a container that holds a collection of names (identifiers) and associates them with corresponding objects or values. It provides a way to organize and differentiate names to avoid naming conflicts and to provide a unique context for each name.

What is the difference between files vs modules?
- `File` (a generic file denoted by any extension: `.txt`, ...)
- `Module` (a python file denoted by `.py`) $\rightarrow$ `Package` (Multiple `Module`(s))
	- Hence, a `Module` is just a file containing python code.

## What is in a `module`?
- A module =`.py` file that can either be structured as: Variables only, Functions only, class
```python
# Variables only
# untitled_variables_only.py
# ###################################
# var_a = "IMPORT STATEMENT failed!"
# ###################################


# Functions only
# untitled_functions_only.py
# ###################################
# def error_func1():
# 	return "IMPORT STATEMENT failed!"
# 	
# def error_func2():
# 	return "SYNTAX ERROR!"
# ###################################


# Class 
# untitled_class_or_classes.py
# ###################################
# class ErrorClass:
# 	def __init__(self):
# 		self.flag_1 = 0
# 		self.flag_2 = 0
# 		
# 	def error_func1():
# 		if self.flag_1 = 1:
# 			return "IMPORT STATEMENT failed!"
# ###################################
```

## What is in a package?
- A python package is a directory that has multiple python files.

```
my_package/
├── __init__.py
├── module1.py
├── module2.py
└── subpackage/
    ├── __init__.py
    ├── submodule1.py
    └── submodule2.py
```
- Each package 
	1) Contains python files (`.py`).
	2) Contains a `__init__.py` module, which tells Python Interpreter to initialize & register this "directory" as a Python package. Without this, Python will not recognize it as a package, and won't be able to import modules from that directory in code as a package.

-----
# Importing a `module` (a python file) vs importing a `package` (multiple python files in a directory)

### 1. Modules
 `import {module}` vs `from {module} import *`
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


## 2. Importing packages