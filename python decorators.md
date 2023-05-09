
`@{  }`

Use: To ENHANCE an existing function's definition.

Syntax:
```python
def function_which_takes_func_object_as_argument(func):
	def new_func():
		func()	
		print('added feature')
		
	return new_func

@function_which_takes_func_object_as_argument
def func():
	print('old feature')
	return None
	
# decorators without arguments are used without parentheses, whereas decorators with arguments require parentheses, even if you pass empty arguments. 
# So when using a decorator, you have to wonder whether it takes arguments or not. A bit more to think about everytime you use a decorator.

# The example decorator above does not take in arguments, where the function object does not count. Hence it can be defined by @{decorator_func_name} without parenthesis.
```
> Examples where decorator requires parenthesis [Example which is a little confusing](https://tech.people-doc.com/python-class-based-decorators.html#:~:text=decorators%20without%20arguments%20are%20used,if%20you%20pass%20empty%20arguments.)

You might ask, why not just define a new function with another identifier?
- Well the use of python decorator effectively reduces redefinition of code, and just allows the capability to build upon an existing function that was previously defined or maybe to maintain two version of functions another with more complex and enchanced implementation.
- The basic idea behind a decorator is to take a function, modify its behavior and then return the modified function. This can be useful in situations where we want to add functionality to a function or class, but don't want to modify the original source code.

Prerequisites:
- Python "Closure" concept:
	- Python closure is a "nested function" (e.g., `printer()`) that allows us to access variables (e.g., `greeting`, `message`) of the outer function (e.g., `print_msg`) even after it is done executing/ "closed" - hence the use of the name python "closure".
```python
def print_msg(message):
	greeting = 'Hello'

	def printer():
		print(greeting, message)

	return printer

# Notice when print_msg() is done executing, running the func() function in the next line, which is a function object still retrieves `greeting` and `message` values, even when print_msg() is already out of scope.
func = print_msg("Python is awesome")
func()

# Output:
# Hello Python is awesome
```

The codes below generates the same output, where one uses the python decorator, while one does not.

- Without @ (python decorator)
```python
def display_info(func):
	# inner function
	def new_printer():
		print("Executing", func.__name__, "function")
		func()
		print("Finished execution")
	return new_printer 

def printer():
	print("Hello world")

printer = display_info(printer)

# A function - `display_info()` "takes in another function as argument - `printer()`", to define a NEW function - `new_printer()`, usually to enhance the function's functionality, and returns it as a NEW python function object. Assigned and replacing the definition of existing/ old function identifier - printer().
# printer() now takes in a new function definition.
```
- With @ (python decorator)

## Python decorator taking 1 function object
```python
def display_info(func):
	# inner function
	def new_printer():
		print("Executing", func.__name__, "function")
		func()
		print("Finished execution")
	return new_printer 

@display_info
def printer():
	print("Hello world")

# Hence, when `printer()` function is being called, it effectively executes the function definition of the new function - `new_printer()`.

# The only difference:
# Effectively removing the last line of the code above, which requires a re-assignment to a new variable.
# It basically is the same as above - replacing/ enhancing the function definition of printer() to new_printer(). 
```

## Python decorator taking >1 function objects
-  It is possible, but not recommended.
- Conceptually, decorators are supposed to alter the functionality of a single function they decorate; a function that sequences two other functions on an equal footing may not make much sense as a decorator. ([Source](https://stackoverflow.com/questions/46018980/python-decorator-for-multiple-functions-as-arguments#:~:text=Conceptually%2C%20decorators%20are%20supposed%20to,much%20sense%20as%20a%20decorator.))
```python
# THIS CODE GENERATES AN ERROR:
def my_decorator(func1, func2):
    def wrapper():
        print("Before calling functions")
        func1()
        func2()
        print("After calling functions\n")
    return wrapper

@my_decorator
def my_function1():
    print("Function 1 called")

@my_decorator
def my_function2():
    print("Function 2 called")

my_function1()
my_function2()

# Output GENERATES AN ERROR
'''
TypeError: my_decorator() missing 1 required positional argument: 'func2'
'''

# It makes more sense not to use decorator syntax:
# E.g., 
def sequence(f, g):
   def sequenced_func():
       f()
       g()
   return sequenced_func

def func1():
    print('func1')

def func2():
    print('func2')

sequenced_func = sequence(func1, func2)
```

