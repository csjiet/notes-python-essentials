
> Type hinting was introduced in Python3.5, that allows users to annotate the expected types of **parameters** and **return values** of a function. 


# Type definition syntax:
```python
def foo(name: str) -> str:
	return 'Hello ' + name
```
> States that: This function expects type `str` for argument `name`, and expects return type to be `str`.

It provide a way of hinting types to statically indicate the type of a value within your Python code. 
This may help static type checkers and linters accurately predict errors.

# `typing` module

All typing classes - [typing Type](https://docs.python.org/3/library/typing.html#aliases-to-built-in-types)

`List[]` 
``` python
from typing import List

VectoR = List[float]
print(VectoR) # Output: typing.List[float]

def foo(vec: VectoR): -> Vector
	return [2 * num for num in VectoR]
```
> The above assigns `VectoR` as a type alias: `List[float]`. Which means the function `foo()` only expects a list of floating point values - gives more specification as to which `list` the function expects.

`Dict[]`
```python
from typing import Dict

ContactDict = Dict[str, str]
def name(contact: ContactDict) -> str:	
	return str(contact.keys())
```
> The above assigns `ContactDict` as a type alias for `Dict[str, str]`, which means the function `name()` only expects  
> - keys are strings (`str`) and 
> - values are also strings (`str`). 
> Essentially, it's defining a dictionary with string keys and string values.

