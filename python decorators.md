
Python decorators:
- Use: allows a user to **add new functionality** ("decorate") to an existing core function without modifying its structure.

## Syntax
``` python
# Core function --- func()
@decorator_function_name
def func(arg1, arg2):
    return anything 

# Modification to the Core function using decorators, while keeping core function's core structure
def decorator_function_name(func):
    def wrapper_function(arg1, arg2):

        '''
        additional decorator code 1
        '''

        func(arg1, arg2)

        '''
        additional decorator code 2
        '''
        return anything

    return wrapper_function

# Calling function
func() # will execute 1) the decorator function first before 2) the core function 

```

## Use: 
- To EXTEND/ ENHANCE an existing core function, without adding code to the existing core function.
    - It does so by automatically invoking the decorator function, when the existing core function's signature is invoked. It first runs the code in the decorator function that wraps code around the existing core function's code.
> Applications (extensions/ enhancements that are practical):
> - Logging: You can create a decorator to log information about function calls, such as the input parameters, execution time, or any other relevant details.
> - Authorization and Authentication: Decorators can be used to check whether a user is authorized to access a particular resource or perform a specific action.
> - Caching: You can create a decorator to cache the results of function calls, which can be especially useful for computationally expensive functions.
> - Timing and Profiling: Decorators can be employed to measure the execution time of functions or to profile their performance.
> - Retry Mechanism: You can implement a decorator to automatically retry a function in case of failures or exceptions.


## Examples:
Syntax without decorators:
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
Syntax with decorators
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
(Optional) Unconventional uses: 
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

