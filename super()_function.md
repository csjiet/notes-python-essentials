Resources:
- [Inheritance in Python](https://www.geeksforgeeks.org/inheritance-in-python/)

Definition:
Inheritance is a mechanism to share a set of properties (variables, functions) from a class (base/ parent class)  with another class (child class). 

Types of inheritance:
1. Single inheritance (child class inherits from only one parent class)
2. Multiple inheritance (child class inherits from multiple parent classes)

## Two steps to establish inheritance in Python:
- **Step 1**. Denote inheritance in code
- **Step 2**. Instantiate parent class

### Single inheritance
Problem:
> Below uses only a Single inheritance for simplicity. 
``` python
class A:
	def __init__(self, n='Rahul'):
		self.name = n

class B(A): # Step 1: Denote inheritance 
	def __init__(self, roll):
		# Step 2: : Initialize parent 
		# (Is not done here hence the error)
		self.roll = roll

object = B(23)
print(object.name)

'''
Output: 
AttributeError: 'B' object has no attribute 'name'
'''
```
> Above is a valid access of an attribute from its parent class. However, the error is thrown because the ***parent class was instantiated***, hence python's interpreter does not know that its parent exists. Hence: "Parent class of a child class should always be initialized first".

Solution: `super()`
> `super()` is an in-built function that returns the objects that represent the parent class.
``` python
# parent class
class Person():
def __init__(self, name, age):
	self.name = name
	self.age = age

def display(self):
	print(self.name, self.age)

# child class
class Student(Person):
def __init__(self, name, age):
	self.sName = name
	self.sAge = age
	# !!!! inheriting the properties of parent class !!!
	super().__init__("Rahul", age)

def displayInfo(self):
	print(self.sName, self.sAge)

obj = Student("Mayank", 23)
obj.display() # Now function inherited from base/ parent class can be used
obj.displayInfo()
```

Limitations `super()`:
- `super()` is used to access the immediate parent's class members.

### Multi-class inheritance
### Exploiting the MRO (Method Resolution Order) for multi-class inheritance
Overridden child functions
`super(ImmediateClassName, currentObject)` arguments:
- `ImmediateClassName`: The name of the class that is just inherited before the class that we want to access using the super() function.
- `currentObject`: The current object of the class.

Problem:
``` python
class Parent:
    def __init__(self):
        print("This is the parent class")
        
class Parent1:
    def __init__(self):
        print("This is the parent1 class")
        
class Child(Parent1, Parent):
    def __init__(self):
        ##Calling constructor of the Parnet 1 class
       super().__init__()
    
ob = Child()

'''
Output:
This is the parent1 class
'''
```
> But how do we access Parent class constructor?

Solution:
``` python
class Parent:
    def __init__(self):
        print("This is the parent class")
        
class Parent1:
    def __init__(self):
        print("This is the parent1 class")
        
class Child(Parent1, Parent):
    def __init__(self):
        ##Calling constructor of the Parent 1 class
       super(Parent1, self).__init__()

ob = Child()
'''
Output:
This is the parent class
'''
```
> The above works because of the Method Resolution Order (MRO) - which defines the order of the inherited methods in the child class.
> In the case above: the super() **by default** will search the constructor according to the order of the inherited class, ***it will search first in the Parent1 class*** than in the Parent class.

MRO example:
```python
class Parent:
    def __init__(self):
        print("This is the parent class")
        
class Parent1:
    def __init__(self):
        print("This is the parent1 class")
        
class Child(Parent1, Parent):
    def __init__(self):
        ##Calling constructor of the Parnet 1 class
       super().__init__()

print(Child.mro())

'''
Output:
[<class '__main__.Child'>, <class '__main__.Parent1'>, <class '__main__.Parent'>, <class 'object'>]
'''
```
> Notice: the Child class first extends the Parent1 class then extend the Parent class. The `object` class is the super class of all the classes in the python language that's why at last the Child class also extends the object class by default.

Hence when we introduce arguments into the `super()` function, we will specify the `Immediateclassname` - which denotes the class name in the MRO where the definition of its parent to the right of the MRO sequence will be used.
```python
class Parent:
    def __init__(self):
        print("This is the parent class")
        
class Parent1:
    def __init__(self):
        print("This is the parent1 class")
        
class Child(Parent1, Parent):
    def __init__(self):
	   # Hence
       super().__init__()
       # Is the same as 
       super(Child, self).__init__()

print(Child.mro())
'''
Output:
[<class '__main__.Child'>, <class '__main__.Parent1'>, <class '__main__.Parent'>, <class 'object'>]
'''
ob = Child() # Next to Child to the right is Parent1, hence its constructor will be called.
'''
Output:
This is the parent1 class 
This is the parent1 class
'''
```

AND We can utilize this arguments in super() to have finer-grain control:
``` python
class Parent:
    def __init__(self):
        print("This is the parent class")
        
class Parent1:
    def __init__(self):
        print("This is the parent1 class")
        
class Child(Parent1, Parent):
    def __init__(self):
       super(Parent1, self).__init__() # next in sequence of mro to Parent1 is Parent.
       print('###########################')
       super(Child, self).__init__() # next in sequence of mro to Child is Parent1.

print(Child.mro())
'''
Output:
[<class '__main__.Child'>, <class '__main__.Parent1'>, <class '__main__.Parent'>, <class 'object'>]
'''
print(Parent1.mro())
'''
Output:
[<class '__main__.Parent1'>, <class 'object'>]
'''
print(Parent.mro())
'''
Output:
[<class '__main__.Parent'>, <class 'object'>]
'''

ob = Child()
'''
Output:
This is the parent class 
########################### 
This is the parent1 class
'''
```

