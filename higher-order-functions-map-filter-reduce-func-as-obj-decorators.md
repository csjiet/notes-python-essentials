### Higher order functions

**Definition**: A function that does one of the following: 
1. takes one or more functions as arguments (e.g., function composition (in math) --- $f(g(x))$)
2. returns a function as its result.


> Benefits: Promotes "functional programming"
> - **Functional programming**: A programming paradigm where programs are constructed by applying and **composing functions**. (Benefits: concise and non-redundant code, readable)
> 

> Types of "higher order functions" in python:
> 1. Function as objects
> 2. In-built higher-order functions
> 3. Decorators


### 1) Function as objects:
> ALL functions that are declared in python are higher-order functions --- capable of taking one or more "functions as objects" as arguments.
```python
def foo():
    return 1 
    
def bar(func):
    return func()

print(bar(foo)) # Output: 1
```


### 2) In-built higher-order functions:
- `map`
- `filter`
- `reduce`


### 3) Decorators:
READ `python-decorators.md`


