Resources:
- [NumPy: More "Array creation routines"](https://numpy.org/doc/stable/reference/routines.array-creation.html)

All list-array-tensors are contiguous memory block upon creation.

# Lists
-  heterogenous, ordered, mutable data structures.
	- mutable: updates are done in-place of existing data structure.
- PERKS: Heterogeneity
```
# Empty list
var = []

# Manual
# 1D list 
var = [3, 'text', True]

# Automated
# 1D list comprehension
var = [x for x in range(10)]

# list constructor
list({iterables_or_map_or_filter})
```

# Numpy arrays
> Pytorch tensors > numpy arrays - speed and functionality. Unfortunately, pytorch tensors require external installation that might not exist ubiquitously. 

- homogenous, ordered, mutable data structures.
- It can be heterogenous too!
	- Using `object` dtype allows you to store heterogeneous data, such as numbers, strings, or even other objects, in the same array.
- PERKS: 
	- Superior in both time and space complexity. 
	- More control over propagated elements in the array 
- There are no inherent "empty arrays". If you don't want an array, you just don't create them. Instead, you can create an array of defined size, propagated with arbitrary values - which actually saves time. This allows a contiguous memory block to be allocated without assigning/ overriding the residual values left from prior usage of the allocated memory block. 
- Numpy only allows specific data types to be stored as elements. (Data types that are stored within `<class 'numpy.ndarray'>` can be viewed using `var.dtype` field)
	- `i` - integer
	- `b` - boolean
	- `u` - unsigned integer
	- `f` - float
	- `c` - complex float
	- `m` - timedelta
	- `M` - datetime
	- `O` - object
	- `S` - string
	- `U` - unicode string
	- `V` - fixed chunk of memory for other type ( void )
``` python
import numpy as np

# Empty array 
# Create by shape
# An array of defined shape, propagated with prior residual memory value
x = np.empty({shape_defined_as_tuple})
x = np.empty(
	{shape_defined_as_tuple}, 
	dtype={'np.float64'/ 'np.int64'}, 
	order={'C'/ 'F'}
	)

# An array of defined shape, propagated with 0's
x = np.zeros({shape_defined_as_tuple})
x = np.zeros(
	{shape_defined_as_tuple}, 
	dtype={'np.float64'/ 'np.int64'}, 
	order={'C'/ 'F'}
	)

# An array of defined shape, propagated with 1's
x = np.ones({shape_defined_as_tuple})
x = np.ones(
	{shape_defined_as_tuple}, 
	dtype={'np.float64'/ 'np.int64'}, 
	order={'C'/ 'F'}
	)

# An array of defined shape, propagated using a defined value 
x = np.full({shape_defined_as_tuple})
x = np.full(
	{shape_defined_as_tuple}, 
	{fill_value}, 
	dtype={dtype}, 
	order={'C'/'F'}
	)
```

``` python
import numpy as np

# Create by object
var = np.array({object})
var = np.array(
   {object}, 
   dtype={data_type}, 
   order={'C'/'F'/'A'}
   )

'''
# Optional arguments
dtype=
- np.int8, np.int16, np.int32, np.int64, np.int || int (signed integers)
- np.uint8, np.uint16, np.uint32, np.uint64, np.uint (signed integers)
- np.float16, np.float32, np.float64, np.float || float (floating-point)
- np.complex64, np.complex128, np.complex (complex types)
- np.bool_ || bool (boolean) # THIS IS KINDA COOL! CAN BE USED AS TYPE CASTING
- np.str_, np.unicode_ || str (string)
- np.void (generic types)
- np.datetime64 (datetime types)
- np.timedelta64 (timedelta types)
- object (object types)

order= 
Given
[[1, 2, 3],
 [4, 5, 6],
 [7, 8, 9]]
- 'C': Row-major order (C-contiguous order) (row are stored next to each other in memory, and rows are stored consecutively.)
	- Stored order: 1 2 3 4 5 6 7 8 9
- 'F': Column-major order (Fortran stype order) (Columns are stored consecutively in memory)
	- Stored order: 1 4 7 2 5 8 3 6 9
- 'A': Auto order (allows NumPy to automatically choose the order based on the input data and the memory layout of the system)
'''
```
- If object is a scalar (e.g., single string, boolean, integer), it will return a 0-d array of that object.
```python
import numpy as np
# Special creation
x = np.arange({start}, {stop}, {step}, dtype={dtype})

# linear space: number spaces evenly w.r.t interval
x = np.linspace({start}, {stop}, {num_data}, dtype={dtype}, retstep={False/ True})

# logarithmic space: number spaces evenly w.r.t interval on a log scale.
x = np.logspace({start}, {stop}, {num_data}, dtype={dtype}, retstep={False/ True})

'''
retstep = True
- returns interval step size as second element in the tuple after outputing array.
'''

x = np.random.rand({d0_size}, {d1_size}, ...)
'''
>> np.random.rand(3,2)
array([[ 0.14022471,  0.96360618],  #random
       [ 0.37601032,  0.25528411],  #random
       [ 0.49313049,  0.94909878]]) #random
'''
x = np.random.random_sample(size={shape})

x = np.fromiter()

x = np.fromfunction()

x = np.fromstring()

x = np.frombuffer()

```

``` python
# 0-d array
var = np.array(32)

# List creation casted into numpy
# 1D array  (an array of 0D arrays)
var = np.array([1,2,3,4,5])

# 2D array (an array of 1D arrays)
var = np.array(
[[1,2,3], 
[4,5,6]]
)

# 3D array (an array of 2D arrays)
var = np.array(
[
[[1,2,3], 
[4,5,6]], 

[[1,2,3], 
[4,5,6]]
]
)

```

# Pytorch Tensors