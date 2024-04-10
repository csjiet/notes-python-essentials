
Functions that can be called to create or manipulate a dictionary

dict()

len(d)

d[key]

clear()

copy()

get()

items()

keys()

values()

pop()

popitem()

update()

from collections import defaultdict
d = defaultdict()

setdefault()

OrderedDict()

dictionary comprehensions

merging dictionaries {**dict1, **dict2}



### `defaultdict`
`defaultdict` (a subclass of `dict` provided by the `collections`)
- Use: Creates and assigns a new default value when a missing key is accessed from the dictionary.
Syntax
``` python
from collections import defaultdict
defaultdict(factory_function)
```

`factory_function`
- function: `func_def_value` from: `def func_def_value(): return 1`
- class: `int`, which calls its constructor `int()` with no arguments, which returns 0.

Example of missing key, key-default_value creation 
```python
from collections import defaultdict
# default factory function is `int`, which returns 0 
my_default_dict = defaultdict(int) 
# This will print 0 instead of raising KeyError
print(my_default_dict['nonexistent_key']) 
# Output: 0
```

- Factory_function: Setting assigned default value to missing/ new key
```python
# Function to return a default values for keys that is not present 
def def_value(): 
	return "Not Present" 
# Defining the dict 
d = defaultdict(def_value) 
d["a"] = 1 
d["b"] = 2 

print(d["a"]) # Output: 1
print(d["b"]) # Output: 2
print(d["c"]) # Output: "Not Present"
```

----
### `dict`
- Upon accessing a missing key, no fall back (default value creation) is done.
Example
```python
# This will raise KeyError
my_dict = {} print(my_dict['nonexistent_key']) 
# Output: KeyError XXX
```
