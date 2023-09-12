Resources:
- [Dunder functions in python](https://mathspp.com/blog/pydonts/dunder-methods)

Dunder functions are built in python functions that give meaning to python's built-in functions (e.g., `len()`) and operators (e.g., `+`) when it is  applied to any user-defined class or any class instance (e.g., `obj + ...` , `obj - ...` , `obj != ...` , `... in obj`, `abs(obj)`, `int(obj)`, `math.floor(obj)`, `len(obj)`) 
- `obj` here can be instance of any type of python class (e.g.,  `ABCDE_Class() + 3` , where we can define a meaning for this expression of an instance, which seems to make no sense at first glance).

## Table with exhaustive list of dunder methods in and its usage [here](https://mathspp.com/blog/pydonts/dunder-methods)


|Dunder method|Usage / Needed for|Learn more|
|---|---|---|
|`__init__`|Initialise object|[docs](https://docs.python.org/3/reference/datamodel.html#object.__init__)|
|`__new__`|Create object|[docs](https://docs.python.org/3/reference/datamodel.html#object.__new__)|
|`__del__`|Destroy object|[docs](https://docs.python.org/3/reference/datamodel.html#object.__del__)|
|`__repr__`|Compute “official” string representation / `repr(obj)`|[blog](https://mathspp.com/blog/pydonts/str-and-repr); [docs](https://docs.python.org/3/reference/datamodel.html#object.__repr__)|
|`__str__`|Pretty print object / `str(obj)` / `print(obj)`|[blog](https://mathspp.com/blog/pydonts/str-and-repr); [docs](https://docs.python.org/3/reference/datamodel.html#object.__str__)|
|`__bytes__`|`bytes(obj)`|[docs](https://docs.python.org/3/reference/datamodel.html#object.__bytes__)|
|`__format__`|Custom string formatting|[blog](https://mathspp.com/blog/pydonts/string-formatting-comparison#custom-formatting); [docs](https://docs.python.org/3/reference/datamodel.html#object.__format__)|
|`__lt__`|`obj < ...`|[docs](https://docs.python.org/3/reference/datamodel.html#object.__lt__)|
|`__le__`|`obj <= ...`|[docs](https://docs.python.org/3/reference/datamodel.html#object.__le__)|
|`__eq__`|`obj == ...`|[docs](https://docs.python.org/3/reference/datamodel.html#object.__eq__)|
|`__ne__`|`obj != ...`|[docs](https://docs.python.org/3/reference/datamodel.html#object.__ne__)|
|`__gt__`|`obj > ...`|[docs](https://docs.python.org/3/reference/datamodel.html#object.__gt__)|
|`__ge__`|`obj >= ...`|[docs](https://docs.python.org/3/reference/datamodel.html#object.__ge__)|
|`__hash__`|`hash(obj)` / object as dictionary key|[docs](https://docs.python.org/3/reference/datamodel.html#object.__hash__)|
|`__bool__`|`bool(obj)` / define Truthy/Falsy value of object|[blog](https://mathspp.com/blog/pydonts/truthy-falsy-and-bool); [docs](https://docs.python.org/3/reference/datamodel.html#object.__bool__)|
|`__getattr__`|Fallback for attribute access|[docs](https://docs.python.org/3/reference/datamodel.html#object.__getattr__)|
|`__getattribute__`|Implement attribute access: `obj.name`|[docs](https://docs.python.org/3/reference/datamodel.html#object.__getattribute__)|
|`__setattr__`|Set attribute values: `obj.name = value`|[docs](https://docs.python.org/3/reference/datamodel.html#object.__setattr__)|
|`__delattr__`|Delete attribute: `del obj.name`|[docs](https://docs.python.org/3/reference/datamodel.html#object.__delattr__)|
|`__dir__`|`dir(obj)`|[docs](https://docs.python.org/3/reference/datamodel.html#object.__dir__)|
|`__get__`|Attribute access in descriptor|[docs](https://docs.python.org/3/reference/datamodel.html#object.__get__)|
|`__set__`|Set attribute in descriptor|[docs](https://docs.python.org/3/reference/datamodel.html#object.__set__)|
|`__delete__`|Attribute deletion in descriptor|[docs](https://docs.python.org/3/reference/datamodel.html#object.__delete__)|
|`__init_subclass__`|Initialise subclass|[docs](https://docs.python.org/3/reference/datamodel.html#object.__init_subclass__)|
|`__set_name__`|Owner class assignment callback|[docs](https://docs.python.org/3/reference/datamodel.html#object.__set_name__)|
|`__instancecheck__`|`isinstance(obj, ...)`|[docs](https://docs.python.org/3/reference/datamodel.html#class.__instancecheck__)|
|`__subclasscheck__`|`issubclass(obj, ...)`|[docs](https://docs.python.org/3/reference/datamodel.html#class.__subclasscheck__)|
|`__class_getitem__`|Emulate generic types|[docs](https://docs.python.org/3/reference/datamodel.html#object.__class_getitem__)|
|`__call__`|Emulate callables / `obj(*args, **kwargs)`|[docs](https://docs.python.org/3/reference/datamodel.html#object.__call__)|
|`__len__`|`len(obj)`|[docs](https://docs.python.org/3/reference/datamodel.html#object.__len__)|
|`__length_hint__`|Estimate length for optimisation purposes|[docs](https://docs.python.org/3/reference/datamodel.html#object.__length_hint__)|
|`__getitem__`|Access `obj[key]`|[blog](https://mathspp.com/blog/pydonts/inner-workings-of-sequence-slicing#getting-items-from-sequences); [docs](https://docs.python.org/3/reference/datamodel.html#object.__getitem__)|
|`__setitem__`|`obj[key] = ...` or `obj[]`|[blog](https://mathspp.com/blog/pydonts/inner-workings-of-sequence-slicing#setting-items-deleting-items-and-container-emulation); [docs](https://docs.python.org/3/reference/datamodel.html#object.__setitem__)|
|`__delitem__`|`del obj[key]`|[blog](https://mathspp.com/blog/pydonts/inner-workings-of-sequence-slicing#setting-items-deleting-items-and-container-emulation); [docs](https://docs.python.org/3/reference/datamodel.html#object.__delitem__)|
|`__missing__`|Handle missing keys in `dict` subclasses|[docs](https://docs.python.org/3/reference/datamodel.html#object.__missing__)|
|`__iter__`|`iter(obj)` generates an iterator object where each subsequent element can be accessed using the `next()` function, defined in `__next_()`  / `for ... in obj` (iterating over)|[docs](https://docs.python.org/3/reference/datamodel.html#object.__iter__) [example](https://www.geeksforgeeks.org/python-__iter__-__next__-converting-object-iterator/)|
|`__reversed__`|`reverse(obj)`|[docs](https://docs.python.org/3/reference/datamodel.html#object.__reversed__)|
|`__contains__`|`... in obj` (membership test)|[docs](https://docs.python.org/3/reference/datamodel.html#object.__contains__)|
|`__add__`|`obj + ...`|[blog](https://mathspp.com/blog/pydonts/overloading-arithmetic-operators-with-dunder-methods#the-dunder-methods-for-binary-arithmetic-operations); [docs](https://docs.python.org/3/reference/datamodel.html#object.__add__)|
|`__radd__`|`... + obj`|[blog](https://mathspp.com/blog/pydonts/overloading-arithmetic-operators-with-dunder-methods#reflected-dunder-methods); [docs](https://docs.python.org/3/reference/datamodel.html#object.__radd__)|
|`__iadd__`|`obj += ...`|[blog](https://mathspp.com/blog/pydonts/overloading-arithmetic-operators-with-dunder-methods#augmented-arithmetic-assignment); [docs](https://docs.python.org/3/reference/datamodel.html#object.__iadd__)|
|`__sub__` [2](https://mathspp.com/blog/pydonts/dunder-methods#fn:2) [3](https://mathspp.com/blog/pydonts/dunder-methods#fn:3)|`obj - ...`|[blog](https://mathspp.com/blog/pydonts/overloading-arithmetic-operators-with-dunder-methods#the-dunder-methods-for-binary-arithmetic-operations); [docs](https://docs.python.org/3/reference/datamodel.html#object.__sub__)|
|`__mul__` [2](https://mathspp.com/blog/pydonts/dunder-methods#fn:2) [3](https://mathspp.com/blog/pydonts/dunder-methods#fn:3)|`obj * ...`|[blog](https://mathspp.com/blog/pydonts/overloading-arithmetic-operators-with-dunder-methods#the-dunder-methods-for-binary-arithmetic-operations); [docs](https://docs.python.org/3/reference/datamodel.html#object.__mul__)|
|`__matmul__` [2](https://mathspp.com/blog/pydonts/dunder-methods#fn:2) [3](https://mathspp.com/blog/pydonts/dunder-methods#fn:3)|`obj @ ...`|[blog](https://mathspp.com/blog/pydonts/overloading-arithmetic-operators-with-dunder-methods#the-dunder-methods-for-binary-arithmetic-operations); [docs](https://docs.python.org/3/reference/datamodel.html#object.__matmul__)|
|`__truediv__` [2](https://mathspp.com/blog/pydonts/dunder-methods#fn:2) [3](https://mathspp.com/blog/pydonts/dunder-methods#fn:3)|`obj / ...`|[blog](https://mathspp.com/blog/pydonts/overloading-arithmetic-operators-with-dunder-methods#the-dunder-methods-for-binary-arithmetic-operations); [docs](https://docs.python.org/3/reference/datamodel.html#object.__div__)|
|`__floordiv__` [2](https://mathspp.com/blog/pydonts/dunder-methods#fn:2) [3](https://mathspp.com/blog/pydonts/dunder-methods#fn:3)|`obj // ...`|[blog](https://mathspp.com/blog/pydonts/overloading-arithmetic-operators-with-dunder-methods#the-dunder-methods-for-binary-arithmetic-operations); [docs](https://docs.python.org/3/reference/datamodel.html#object.__floordiv__)|
|`__mod__` [2](https://mathspp.com/blog/pydonts/dunder-methods#fn:2) [3](https://mathspp.com/blog/pydonts/dunder-methods#fn:3)|`obj % ...`|[blog](https://mathspp.com/blog/pydonts/overloading-arithmetic-operators-with-dunder-methods#the-dunder-methods-for-binary-arithmetic-operations); [docs](https://docs.python.org/3/reference/datamodel.html#object.__mod__)|
|`__divmod__` [2](https://mathspp.com/blog/pydonts/dunder-methods#fn:2)|`divmod(obj, ...)`|[blog](https://mathspp.com/blog/pydonts/overloading-arithmetic-operators-with-dunder-methods#the-dunder-methods-for-binary-arithmetic-operations); [docs](https://docs.python.org/3/reference/datamodel.html#object.__divmod__)|
|`__pow__` [2](https://mathspp.com/blog/pydonts/dunder-methods#fn:2) [3](https://mathspp.com/blog/pydonts/dunder-methods#fn:3)|`obj ** ...`|[blog](https://mathspp.com/blog/pydonts/overloading-arithmetic-operators-with-dunder-methods#the-dunder-methods-for-binary-arithmetic-operations); [docs](https://docs.python.org/3/reference/datamodel.html#object.__pow__)|
|`__lshift__` [2](https://mathspp.com/blog/pydonts/dunder-methods#fn:2) [3](https://mathspp.com/blog/pydonts/dunder-methods#fn:3)|`obj << ...`|[blog](https://mathspp.com/blog/pydonts/overloading-arithmetic-operators-with-dunder-methods#the-dunder-methods-for-binary-arithmetic-operations); [docs](https://docs.python.org/3/reference/datamodel.html#object.__lshift__)|
|`__rshift__` [2](https://mathspp.com/blog/pydonts/dunder-methods#fn:2) [3](https://mathspp.com/blog/pydonts/dunder-methods#fn:3)|`obj >> ...`|[blog](https://mathspp.com/blog/pydonts/overloading-arithmetic-operators-with-dunder-methods#the-dunder-methods-for-binary-arithmetic-operations); [docs](https://docs.python.org/3/reference/datamodel.html#object.__rshift__)|
|`__and__` [2](https://mathspp.com/blog/pydonts/dunder-methods#fn:2) [3](https://mathspp.com/blog/pydonts/dunder-methods#fn:3)|`obj & ...`|[blog](https://mathspp.com/blog/pydonts/overloading-arithmetic-operators-with-dunder-methods#the-dunder-methods-for-binary-arithmetic-operations); [docs](https://docs.python.org/3/reference/datamodel.html#object.__and__)|
|`__xor__` [2](https://mathspp.com/blog/pydonts/dunder-methods#fn:2) [3](https://mathspp.com/blog/pydonts/dunder-methods#fn:3)|`obj ^ ...`|[blog](https://mathspp.com/blog/pydonts/overloading-arithmetic-operators-with-dunder-methods#the-dunder-methods-for-binary-arithmetic-operations); [docs](https://docs.python.org/3/reference/datamodel.html#object.__xor__)|
|`__or__` [2](https://mathspp.com/blog/pydonts/dunder-methods#fn:2) [3](https://mathspp.com/blog/pydonts/dunder-methods#fn:3)|`obj \| ...`|[blog](https://mathspp.com/blog/pydonts/overloading-arithmetic-operators-with-dunder-methods#the-dunder-methods-for-binary-arithmetic-operations); [docs](https://docs.python.org/3/reference/datamodel.html#object.__or__)|
|`__neg__`|`-obj` (unary)|[blog](https://mathspp.com/blog/pydonts/overloading-arithmetic-operators-with-dunder-methods#the-dunder-methods-for-the-unary-arithmetic-operations); [docs](https://docs.python.org/3/reference/datamodel.html#object.__neg__)|
|`__pos__`|`+obj` (unary)|[blog](https://mathspp.com/blog/pydonts/overloading-arithmetic-operators-with-dunder-methods#the-dunder-methods-for-the-unary-arithmetic-operations); [docs](https://docs.python.org/3/reference/datamodel.html#object.__pos__)|
|`__abs__`|`abs(obj)`|[blog](https://mathspp.com/blog/pydonts/overloading-arithmetic-operators-with-dunder-methods#the-dunder-methods-for-the-unary-arithmetic-operations); [docs](https://docs.python.org/3/reference/datamodel.html#object.__abs__)|
|`__invert__`|`~obj` (unary)|[blog](https://mathspp.com/blog/pydonts/overloading-arithmetic-operators-with-dunder-methods#the-dunder-methods-for-the-unary-arithmetic-operations); [docs](https://docs.python.org/3/reference/datamodel.html#object.__invert__)|
|`__complex__`|`complex(obj)`|[docs](https://docs.python.org/3/reference/datamodel.html#object.__complex__)|
|`__int__`|`int(obj)`|[docs](https://docs.python.org/3/reference/datamodel.html#object.__int__)|
|`__float__`|`float(obj)`|[docs](https://docs.python.org/3/reference/datamodel.html#object.__float__)|
|`__index__`|Losslessly convert to integer|[docs](https://docs.python.org/3/reference/datamodel.html#object.__index__)|
|`__round__`|`round(obj)`|[docs](https://docs.python.org/3/reference/datamodel.html#object.__round__)|
|`__trunc__`|`math.trunc(obj)`|[docs](https://docs.python.org/3/reference/datamodel.html#object.__trunc__)|
|`__floor__`|`math.floor(obj)`|[docs](https://docs.python.org/3/reference/datamodel.html#object.__floor__)|
|`__ceil__`|`math.ceil(obj)`|[docs](https://docs.python.org/3/reference/datamodel.html#object.__ceil__)|
|`__enter__`|`with obj` (enter context manager)|[docs](https://docs.python.org/3/reference/datamodel.html#object.__enter__)|
|`__exit__`|`with obj` (exit context manager)|[docs](https://docs.python.org/3/reference/datamodel.html#object.__exit__)|
|`__await__`|Implement awaitable objects|[docs](https://docs.python.org/3/reference/datamodel.html#object.__await__)|
|`__aiter__`|`aiter(obj)`|[docs](https://docs.python.org/3/reference/datamodel.html#object.__aiter__)|
|`__anext__`|`anext(obj)`|[docs](https://docs.python.org/3/reference/datamodel.html#object.__anext__)|
|`__aenter__`|`async with obj` (enter async context manager)|[docs](https://docs.python.org/3/reference/datamodel.html#object.__aenter__)|
|`__aexit__`|`async with obj` (exit async context manager)|[docs](https://docs.python.org/3/reference/datamodel.html#object.__aexit__)|
|`__dict__`|`obj.__dict__` (holds the namespace of a class or an object/ a dict of class-level attribute and methods and its value); (`obj.__dict__['new_attribute'] = "value"` is not recommended as it can bypass any custom behavior or logic defined by the class at runtime, instead use `setattr()` to dynamically set attributes for an object) ||
