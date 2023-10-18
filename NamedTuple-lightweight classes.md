Resources:
- [GeeksForGeeks: Named tuple](https://www.geeksforgeeks.org/namedtuple-in-python/)

Definition: It provides a way to create simple, lightweight ==**immutable== data structures** similar to a class, but without the overhead of defining a full class.

> "NamedTuple"?:
> **Named**: It resembles named fields, where each element in the tuple is associated with a name or label, which is specified.
> **Tuple**: It is an ordered collection of elements (can be of different types) that is immutable. (Tuples in python are immutable; lists, dicts, sets, classes are mutable)

Import statements:
`from collections import namedtuple`

``` python
# Python code to demonstrate namedtuple()
from collections import namedtuple

# Declaring namedtuple()
Student = namedtuple('Student', ['name', 'age', 'DOB'])

# Adding values
s = Student('Nandini', '19', '2541997')

# Access using name
print("The Student name using keyname is : ", end="")
print(s.name)

# Access using index
print("The Student age using index is : ", end="")
print(s[1])

```

Benefits:
1. Fields: Allows you to create classes for storing data where the fields have names, which can be accessed using dot notation.
2. Immutable: Data remains constant, where values cannot be changed after creation.
3. Memory efficient: It inherits from Python's built-in `tuple` type and stores data in a compact, memory-efficient way.
4. Speed of creation: Small classes can be defined quickly without writing explicit class definitions. This is particularly useful when you need simple data containers

