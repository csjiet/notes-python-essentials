Pass by reference in Python: When you pass a variable as an argument to a function, the function receives a reference (pointer) to the variable (similar to C/C++)

Depending on the object's data type - `mutable` or `immutable`, a function call that passes the created object as an argument will invoke separate protocols.
- When object is a `mutable` object - `dict`, `list`, `set`, pass by reference:  
	- The reference of the object will be passed into the function, where modification to the object within the function will cause the original object outside the function to be updated as well.
	- Solution (if a local copy is meant to be retained): `dictionary1.copy()`/ `list_1.copy()`/ `set_1.copy()`
- When object is an `immutable` object - `int`, `string`, `tuples`, pass by copy: 
	- The value of the object is copied to a new local variable with a new reference, where modifications to the object within the function will NOT cause the original object outside the function to be changed. 
