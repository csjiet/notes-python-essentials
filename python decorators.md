
## Syntax
```
def decorate_function(decorated_function):
	def packaging_decorate_and_decorated_function():
		# Can be at any order
		# operation from decorate_function()
		# operation from decorated_function()
	
	return packaging_decorate_and_decorated_function	

@{decorate_function}
def decorated_function():
	pass
```
- The `decorate_function` (like sprinkles/ icing), the `decorated_function` (the muffin).
- Once the muffin is taken into the sprinkle/ icing factory (function), there is a (assembly function) - `packaging_decorate_and_decorated_function()`, which combines both functions together into a new, more complex operation.
- The "assembled" function - `packaging_decorate_and_decorated_function()` is returned as a function identifier.

> How to remember?
> - The `@decorate_function` is always taken into another function as argument (apparent from its explicit declaration as an argument) and combined with another function, using another nested function - e.g., `packaging_deorate_and_decorated_function()` declared within `decorate_function()`, where it is ultimately returned as a function signature/ identifier.

## Use: 
- To ENHANCE an existing function's definition.

> The two set of python code below performs the same operations, while demonstrates how the presence of decorators can be a replacement of longer code (without decorators). 

### Syntax without decorators:
```python
def my_decorator(function_to_be_decorated):

    def wrapper_function():
        print("This is some code before the decorated function")

        function_to_be_decorated()

        print("This is some code after the decorated function")

    return wrapper_function

def my_func():
    print("This is the function to be decorated")

decorated_function = my_decorator(my_func)

decorated_function()
```
- Output:
```
This is some code before the decorated function
This is the function to be decorated
This is some code after the decorated function
```
### Syntax with decorators
```python
def my_decorator(function_to_be_decorated):

    def wrapper_function():
        print("This is some code before the decorated function")

        function_to_be_decorated()

        print("This is some code after the decorated function")

    return wrapper_function

@my_decorator
def my_func():
    print("This is the function to be decorated")

my_func()
```
- Output
```
This is some code before the decorated function
This is the function to be decorated
This is some code after the decorated function
```

- Essentially, you just call the `decorated_function` and it does all the process of assembly (combining + returning the combined + call) for you.
- Notice we do not need to call `decorate_function()()`, where the first `()` returns a function identifier, and the next `()` calls it as a function.

------
> We can also extend Python decorators to applications which involves more than one function.

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

