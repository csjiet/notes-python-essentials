# Functional programming functions

Functional programming:
- Definition: A programming paradigm based on breaking down a problem into a set of individual functions. Ideally, every function only takes a set of input arguments and produces an output. 

- Resources:
	- https://realpython.com/python-map-function/#:~:text=Since%20map()%20is%20written,list%20in%20your%20system's%20memory.
	- https://realpython.com/python-reduce-function/

-----------
-----------
## map()
`map(func_identifier, iter)`
- **Use**: Maps each item of the iterable in the first dimension of the iterable to the function using a function identifier which takes arguments.
> Note: Second argument MUST be an iterable

- **Example**:
```python 
# initializing the 2D array
array = [
   [1, 2, 3],
   [4, 5, 6],
   [7, 8, 9]
]
# passing the sum, array to function
result = list(map(sum, array))
# see the result values
# it contains sum of every sub array
print(result)
``` 

	 Output
	 [6, 15, 24]
 
 ----------
``` python
# Written in python interactive session
# We could also write it wtih ipython interactive session with enhanced features
>>> str_nums = ["4", "8", "6", "5", "3", "2", "8", "9", "2", "5"]

>>> int_nums = map(int, str_nums)
>>> int_nums
<map object at 0x7fb2c7e34c70>

>>> list(int_nums)
[4, 8, 6, 5, 3, 2, 8, 9, 2, 5]

>>> str_nums
["4", "8", "6", "5", "3", "2", "8", "9", "2", "5"]
```

- **Benefits**: 
	- Highly **optimized**: written using C
	- Low **memory consumption**: Loads one item in the iterable at a time instead of the whole iterable in the system's memory.
- Resources:
	- https://realpython.com/python-map-function/#:~:text=Since%20map()%20is%20written,list%20in%20your%20system's%20memory.

-----------

## map() with partial()

- Imports: `from functools import partial`
- `partial()`: Takes a function identifier and only listing the arguments to be a fixed, effectively generating a new function.

- Resources:
	- https://www.geeksforgeeks.org/partial-functions-python/ 


-----------
##  filter()
`filter(func_identifier, sequence)`

- **Use**: Filters a sequence, using a function that tests whether each element of a sequence true or not, and retains the item in the sequence if it is true.
- **Param**: 
	- func_identifier:
	- sequence: Any iterators (sets, lists, tuples, or containers)
 - **Return**: An iterator that is already filtered.
 - **Example**:
```python
# a list contains both even and odd numbers.` 
seq =[0,1,2,3,5,8,13]

# result contains odd numbers of the list`
result = filter(lambda x: x % 2 != 0, seq)`
print(list(result))
```

	Output:
	[1,3,5,13]

Using initializer (optional argument)
```python
# Written using python interactive session at the shell
>>> from functools import reduce

>>> numbers = [0, 1, 2, 3, 4]

>>> reduce(my_add, numbers, 100)
100 + 0 = 100
100 + 1 = 101
101 + 2 = 103
103 + 3 = 106
106 + 4 = 110
110
```
 
- Resources:
	- https://www.geeksforgeeks.org/filter-in-python/
 
-----------
-----------
## reduce()
`reduce(func_identifier, iterable, initializer=None)`
- Use: Implements a mathematical technique known as "folding"/ "reduction", where you reduce a list of items into ONLY ***a single cumulative value***, ***incrementally generating partial values from left to right in the iterable***. 
- Important properties/ Steps which are taken during "folding":
	1.  **Apply** a function (or callable) to the ***first two items in an iterable*** and ***generate a partial result***.
	2.  **Use** that partial result, together with the third item in the iterable, to ***generate another partial result***.
	3.  **Repeat** the process until the iterable is exhausted and then ***return a single cumulative value***.
- Example
```python
import functools
# Or
# from functools import reduce

# Initializing list
lis = [1,3,5,6,2]

# using reduce to compute sum of list
print(functools.reduce(lambda a, b: a+b, lis)) # Computes operation defined in the function incrementally, while storing partial values from left to right in an iterable.
```
	Output:
	17
	# Because (1+3) = 4 -> (4+5) = 9 -> (9+6) = 15 -> (15+2)=17 -> 17

- Resources:
	- https://realpython.com/python-reduce-function/


-----------
-----------
# Built-in functions in python that can be called using their function identifiers when calling functional functions 
[abs()](https://www.w3schools.com/python/ref_func_abs.asp) 
Returns the absolute value of a number

[all()](https://www.w3schools.com/python/ref_func_all.asp) 
Returns True if all items in an iterable object are true

[any()](https://www.w3schools.com/python/ref_func_any.asp) 
Returns True if any item in an iterable object is true

[ascii()](https://www.w3schools.com/python/ref_func_ascii.asp) 
Returns a readable version of an object. Replaces none-ascii characters with escape character

[bin()](https://www.w3schools.com/python/ref_func_bin.asp) 
Returns the binary version of a number

[bool()](https://www.w3schools.com/python/ref_func_bool.asp) 
Returns the boolean value of the specified object

[bytearray()](https://www.w3schools.com/python/ref_func_bytearray.asp) 
Returns an array of bytes

[bytes()](https://www.w3schools.com/python/ref_func_bytes.asp) 
Returns a bytes object

[callable()](https://www.w3schools.com/python/ref_func_callable.asp) 
Returns True if the specified object is callable, otherwise False

[chr()](https://www.w3schools.com/python/ref_func_chr.asp) 
Returns a character from the specified Unicode code.

classmethod() 
Converts a method into a class method

[compile()](https://www.w3schools.com/python/ref_func_compile.asp) 
Returns the specified source as an object, ready to be executed

[complex()](https://www.w3schools.com/python/ref_func_complex.asp) 
Returns a complex number

[delattr()](https://www.w3schools.com/python/ref_func_delattr.asp) 
Deletes the specified attribute (property or method) from the specified object

[dict()](https://www.w3schools.com/python/ref_func_dict.asp) 
Returns a dictionary (Array)

[dir()](https://www.w3schools.com/python/ref_func_dir.asp) 
Returns a list of the specified object's properties and methods

[divmod()](https://www.w3schools.com/python/ref_func_divmod.asp) 
Returns the quotient and the remainder when argument1 is divided by argument2

[enumerate()](https://www.w3schools.com/python/ref_func_enumerate.asp) 
Takes a collection (e.g. a tuple) and returns it as an enumerate object

[eval()](https://www.w3schools.com/python/ref_func_eval.asp) 
Evaluates and executes an expression

[exec()](https://www.w3schools.com/python/ref_func_exec.asp) 
Executes the specified code (or object)

[filter()](https://www.w3schools.com/python/ref_func_filter.asp) 
Use a filter function to exclude items in an iterable object

[float()](https://www.w3schools.com/python/ref_func_float.asp) 
Returns a floating point number

[format()](https://www.w3schools.com/python/ref_func_format.asp) 
Formats a specified value

[frozenset()](https://www.w3schools.com/python/ref_func_frozenset.asp) 
Returns a frozenset object

[getattr()](https://www.w3schools.com/python/ref_func_getattr.asp) 
Returns the value of the specified attribute (property or method)

[globals()](https://www.w3schools.com/python/ref_func_globals.asp) 
Returns the current global symbol table as a dictionary

[hasattr()](https://www.w3schools.com/python/ref_func_hasattr.asp) 
Returns True if the specified object has the specified attribute (property/method)

hash() 
Returns the hash value of a specified object

help() 
Executes the built-in help system

[hex()](https://www.w3schools.com/python/ref_func_hex.asp) 
Converts a number into a hexadecimal value

[id()](https://www.w3schools.com/python/ref_func_id.asp) 
Returns the id of an object

[input()](https://www.w3schools.com/python/ref_func_input.asp) 
Allowing user input

[int()](https://www.w3schools.com/python/ref_func_int.asp) 
Returns an integer number

[isinstance()](https://www.w3schools.com/python/ref_func_isinstance.asp) 
Returns True if a specified object is an instance of a specified object

[issubclass()](https://www.w3schools.com/python/ref_func_issubclass.asp) 
Returns True if a specified class is a subclass of a specified object

[iter()](https://www.w3schools.com/python/ref_func_iter.asp) 
Returns an iterator object

[len()](https://www.w3schools.com/python/ref_func_len.asp) 
Returns the length of an object

[list()](https://www.w3schools.com/python/ref_func_list.asp) 
Returns a list

[locals()](https://www.w3schools.com/python/ref_func_locals.asp) 
Returns an updated dictionary of the current local symbol table

[map()](https://www.w3schools.com/python/ref_func_map.asp) 
Returns the specified iterator with the specified function applied to each item

[max()](https://www.w3schools.com/python/ref_func_max.asp) 
Returns the largest item in an iterable

[memoryview()](https://www.w3schools.com/python/ref_func_memoryview.asp) 
Returns a memory view object

[min()](https://www.w3schools.com/python/ref_func_min.asp) 
Returns the smallest item in an iterable

[next()](https://www.w3schools.com/python/ref_func_next.asp) 
Returns the next item in an iterable

[object()](https://www.w3schools.com/python/ref_func_object.asp) 
Returns a new object

[oct()](https://www.w3schools.com/python/ref_func_oct.asp) 
Converts a number into an octal

[open()](https://www.w3schools.com/python/ref_func_open.asp) 
Opens a file and returns a file object

[ord()](https://www.w3schools.com/python/ref_func_ord.asp) 
Convert an integer representing the Unicode of the specified character

[pow()](https://www.w3schools.com/python/ref_func_pow.asp) 
Returns the value of x to the power of y

[print()](https://www.w3schools.com/python/ref_func_print.asp) 
Prints to the standard output device

property() 
Gets, sets, deletes a property

[range()](https://www.w3schools.com/python/ref_func_range.asp) 
Returns a sequence of numbers, starting from 0 and increments by 1 (by default)

repr() 
Returns a readable version of an object

[reversed()](https://www.w3schools.com/python/ref_func_reversed.asp) 
Returns a reversed iterator

[round()](https://www.w3schools.com/python/ref_func_round.asp) 
Rounds a numbers

[set()](https://www.w3schools.com/python/ref_func_set.asp) 
Returns a new set object

[setattr()](https://www.w3schools.com/python/ref_func_setattr.asp) 
Sets an attribute (property/method) of an object

[slice()](https://www.w3schools.com/python/ref_func_slice.asp) 
Returns a slice object

[sorted()](https://www.w3schools.com/python/ref_func_sorted.asp) 
Returns a sorted list

staticmethod() 
Converts a method into a static method

[str()](https://www.w3schools.com/python/ref_func_str.asp) 
Returns a string object

[sum()](https://www.w3schools.com/python/ref_func_sum.asp) 
Sums the items of an iterator

[super()](https://www.w3schools.com/python/ref_func_super.asp) 
Returns an object that represents the parent class

[tuple()](https://www.w3schools.com/python/ref_func_tuple.asp) 
Returns a tuple

[type()](https://www.w3schools.com/python/ref_func_type.asp) 
Returns the type of an object

[vars()](https://www.w3schools.com/python/ref_func_vars.asp) 
Returns the __dict__ property of an object

[zip()](https://www.w3schools.com/python/ref_func_zip.asp)
Returns an iterator, from two or more iterators