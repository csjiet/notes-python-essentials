Resources:
- [Real Python, Python classes](https://realpython.com/python-classes/)


----

### Parent class/ Base class/ Super class

Constructor
``` python
# Parent class
class {class_name}:
    # Constructor
    def __init__({instance_iden}, {args}): 

        # Instance attributes 
        self.{attribute_1} = {values} 

    # Super class instance function 
    def {function_identifier}({instance_iden}, {args}): 
        pass

    # Super class private instance function 
    def _{function_identifier}({instance_iden}, {args}): 
        pass
```
> - `{instance_iden}`: instance to access members (attribute, function) of the class; commonly denoted as "self" as a naming convention (convention $\neq$ keyword)


### Child class/ Subclass/ Derived class

``` python
# Subclass
class {class_name}({parent_class_name}):
    # Constructor
    def __init__({instance_iden}, {args}): 

        # Call parent class constructor
        super().__init__({super_class_args}) 

    # Child class instance function 
    def {function_identifier}({instance_iden}, {args}):
        pass
```

- `super()`: A built-in function that returns object of parent class. It can be used to access parent class' functions, e.g., `super().foo()`. However, once we call `super().__init__()`, we can conveniently access ANY members within the parent + child class using just the `instance_identifier`, commonly named "`self`". 


### Example
``` python
class ParentClass:
    def __init__(self, value):
        self.value = value

    def parent_method(self):
        print("This is a method from the ParentClass")

class ChildClass(ParentClass):
    def __init__(self, value, additional_value):
        super().__init__(value)  # Calling the constructor of the parent class
        self.additional_value = additional_value

    def child_method(self):
        print("This is a method from the ChildClass")

    def use_parent_method(self):
        self.parent_method()  # Accessing the method from the parent class

# Creating an instance of ChildClass
child_obj = ChildClass(10, 20)

# Accessing attributes and calling methods from both parent and child classes
print(child_obj.value)           # Accessing attribute from the parent class
child_obj.child_method()         # Calling method from the child class
child_obj.use_parent_method()     # Calling method from the parent class
```
> Inheritence will allow sharing of parent members --- 
> 1. Attribute, 
> 2. Private instance function (`def _privfoo():`) --- just a naming convention, which means "cannot be called outside the class". It is not reinforced by Python.
> 3. Public instance function 
> 
> which can be accessed using the instance identifier of the child class.


Source: [Using Inheritance and Building Class Hierarchies](https://realpython.com/python-classes/#using-inheritance-and-building-class-hierarchies)


READ MORE! For best python code conventions
