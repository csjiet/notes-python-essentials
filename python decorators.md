Types of decorators:
[All decorators in python](https://wiki.python.org/moin/Decorators)

## Types of decorators

Function decorators


= `@decorator`

= `@decorator(arg1, arg2)`

Built-in decorators
= `@property`

= `@classmethod`

= `@staticmethod`

Class decorators





## Function decorators

### 1.a `@decorator`
- Use: allows a user to **add new functionality** ("decorate") to an existing core function without modifying its structure.

**Syntax**
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

**Use**: 

- To EXTEND/ ENHANCE an existing core function, without adding code to the existing core function.
    - It does so by automatically invoking the decorator function, when the existing core function's signature is invoked. It first runs the code in the decorator function that wraps code around the existing core function's code.
> Applications (extensions/ enhancements that are practical):
> - Logging: You can create a decorator to log information about function calls, such as the input parameters, execution time, or any other relevant details.
> - Authorization and Authentication: Decorators can be used to check whether a user is authorized to access a particular resource or perform a specific action.
> - Caching: You can create a decorator to cache the results of function calls, which can be especially useful for computationally expensive functions.
> - Timing and Profiling: Decorators can be employed to measure the execution time of functions or to profile their performance.
> - Retry Mechanism: You can implement a decorator to automatically retry a function in case of failures or exceptions.


**Examples**:

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


### 1.b Decorators with arguments
xxx

----

## 2. Built-in decorators
### 2.a Property decorators

Definition: When @property is placed before a method, it transforms that method into a special class attribute that can be accessed and modified like any other class attribute without the need for explicit method calls to distinct getter, setter, or delete functions that performs these operations on the attribute. We can do so either by: 
1. `@property`, `@<property_name>.setter`,`@<property_name>.getter`, and `@<property_name>.deleter`, 
2. or using the in-built Python `property()` function --- see how we can ["transform a method into a special class attribute using either `property()` or `@property`"](https://www.geeksforgeeks.org/python-property-function/). 

Example: --- [Long winded video example](https://www.youtube.com/watch?v=8BbngXWouzo)
```python
# Python program to explain property()
# function using decorator

class Alphabet:
	def __init__(self, value):
		self._value = value

	# getting the values
	@property
	def value(self):
		print('Getting value')
		return self._value

	# setting the values
	@value.setter
	def value(self, value):
		print('Setting value to ' + value)
		self._value = value

	# deleting the values
	@value.deleter
	def value(self):
		print('Deleting value')
		del self._value


# passing the value
x = Alphabet('Peter')
print(x.value)

x.value = 'Diesel'

del x.value
```

### 2.b Classmethod decorators

### 3.b Staticmethod decorators

----

## 3. Class decorators

Definition: A "class decorator" is a **function** that takes a class as input and returns a new class. It extend or modify the behavior of a class at the time of creation without making changes to the original class.


Syntax: 

``` python
def my_decorator(cls):
    # Modify or extend the class
    cls.new_attribute = "Added by decorator"

    def new_function(self):
        return "Added functionality"

    return cls

@my_decorator
class MyClass:
    pass

obj = MyClass()

print(obj.new_attribute)
print(obj.new_function())

```
