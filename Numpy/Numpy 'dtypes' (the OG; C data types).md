# numpy.dtypes (short for data types): 
is a class in a numpy library which ***specifies some properties of a data (E.g., type, size, byte order, if subarray: shape)***. 

## Purpose: 
- It is a class that can be instantiated, and takes arguments in its constructor to ***define how a given block of memory should be interpreted/ translated to a data type***. Similar to how you can manually create a memory allocation (malloc()) which generates a (void*) pointer in C, which can be casted to any data type (e.g., Stiring/ int/ float/...) to be "translated" and still be read accordingly, from an array of bits - machine code and give meaning based on the casted data types. 
	- We can think of numpy.dtypes class as an interface to use C data types.
	- Usage: Declaration of a numpy.dtype object using the [numpy.dtype class constructor](https://numpy.org/doc/stable/reference/arrays.dtypes.html).
- ### ONE Argument: (Things we can specify to create C data types)
	- `import numpy as np` 
	- `dt = np.dtype('{dtype_object}')`
		1) **Dtype object**: [dtype_object which can be used](https://numpy.org/doc/stable/reference/arrays.dtypes.html#specifying-and-constructing-data-types);[Image of dtype object hierarchy](https://numpy.org/doc/stable/_images/dtype-hierarchy.png)
			- `None`
				- Defaults to a `float_` data type.
			- `Array-scalar types`  
				- called using (`np.{scalar type})
				- [24 built in array scalar type objects](https://numpy.org/doc/stable/reference/arrays.scalars.html#scalars)
					- e.g.,`np.int32`, `np.int64`, `np.intp`, `np.uint64`,`np.float128`,
			- `Generic types` 
			- `Built-in Python types` 
			- `One-character strings` 
			- `Array-protocol type strings` 
			- `String with comma-separated fields`
			- `Type strings`
   
- ### Attributes that can be accessed 
	- They are fields in a class that can be inherently accessed AFTER a dtype object is instantiated.
	- Attributes:
		-  (`dt.name`) **Type of data**
		- (`dt.itemsize`) **Size of data in bytes** 
		- (`dt.byteorder`)**Byte order of data** 
		- IF we want to declare: "**Structured data types**" - an aggregate of multiple different data types (E.g., Array with elements of the same type in C, Structs, Union, Class) (simple data types: integral: char, short, int, long, bool; enum; floating: float, double, long double) we need to specify more:
			- [Fields](https://numpy.org/doc/stable/reference/arrays.dtypes.html)
		- IF we want to declare: "**Sub-array**" - an array nested within a structured data type. (e.g., a 1D array within a tuple) we need to specify more:
			- shape
			- data type
		- [Other attributes/ fields in the numpy.dtype class](https://numpy.org/doc/stable/reference/arrays.dtypes.html#dtype): When retrieved, gives details of the block of memory
	- E.g, 
	- `dt = np.dtype(np.int32)      # 32-bit integer
	- `dt = np.dtype(np.complex128) # 128-bit complex floating-point number``
	- E.g.,  
	 ```python
		dt = np.dtype([('a', np.int32), ('b', np.float32, (3,))])
		np.zeros(3, dtype=dt)
		array([(0, [0., 0., 0.]), (0, [0., 0., 0.]), (0, [0., 0., 0.])],
      dtype=[('a', '<i4'), ('b', '<f4', (3,))])
``` 

