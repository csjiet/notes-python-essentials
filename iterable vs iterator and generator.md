## Iterable (an object) 
E.g., list, tuples, strings, sets. Only accessible by a `for` loop.

> `iter()`: Iterable $\mapsto$ Iterator
## Iterator (an object): 
- Definition: Implements the `__next__()` function, allowing its elements to be accessed explicitly using `next()` or implicitly using `for` loop. 
- `<class 'list_iterator'>`, `<class 'tuple_iterator'>`, `<class 'set_iterator'>` --- uniquely returned by the `__repr__` function implemented by the respective collection object in python.

### Two methods of creating an iterator: 
1) Dunder methods (implement: `__iter__()`, `__next__()`)
2) Generators (Just call: `yield`) --- generators $\subset$ iterator.

> Benefits of using an iterator (or its subset generator):
> - Memory efficiency: (Due to) "***Lazy evaluation***" --- It only loads a single element pointed to the memory, one at a time. 
> 	- This is opposed to loading all elements within the collection into the memory at once in an iterable.
> 	- E.g., Loading large datasets into memory would be impossible. 
> - Composability: Can be used with `map()`, `filter()`, `reduce()`. --- read more.
> - Dunder functions `__next__` is called implicitly during a for loop without extra syntax. 

> Common use cases of iterator: 
> -  Processing large datasets (that cannot fit into memory)
> - Fine-grained control of iteration process --- pause, resume, or stop the iteration process as needed.
> - Chain operations with `map`, `filter`, and `reduce`.
> - Some function requires an iterator object as arguments. 

```python
# Creation
class NumberIterator:
  # Custom iterator 
  def __init__(self, start, stop, step=1):
    """
    Initialize the iterator with a starting number, ending number (exclusive), and optional step size.
    """
    self.start = start
    self.stop = stop
    self.step = step
    # Initialize current one step before start
    self.current = self.start - self.step  

  def __iter__(self):
    # Return the iterator object itself (self).
    return self

  def __next__(self):
    # Return the next element in the sequence or raise StopIteration when there are no more elements.
    self.current += self.step
    if self.current < self.stop:
      return self.current
    else:
      raise StopIteration # Class!


# Example usage
my_iterator = NumberIterator(2, 10, 2)  # Iterates from 2 to 9 (exclusive) with a step of 2

for number in my_iterator:
  print(number)  # Output: 2, 4, 6, 8

# You can also use next() explicitly
next_number = next(my_iterator)  # Raises StopIteration as there are no more elements
```

``` python
arr = ['Geeks', 'For', 'Geeks'] # iterable object (particularly a list iterable object)

### Convertion
iter_list = iter(arr) # iterable -> iterator object

print(type(iter_list)) # <class 'list_iterator'>
```

```python
### Access
# next()
print(next(iter_list)) 
print(next(iter_list))
print(next(iter_list)) 

'''
Output:
Geeks
For
Geeks
'''
# for loop
for e in iter_list:
	print(e)

'''
Output:
Geeks
For
Geeks
'''
```

> But ... there is a faster way to create iterators.
> If you do not like to implement `__next__()`, due to several reasons:
> 1) State tracking: You need a class dataclass structure (using attributes) that tracks the iteration state internally to know where to resume from.
> 2) Manual cleanups:  It requires careful design to avoid keeping too much state in memory within `__next__`.

Solution Generators:
1) Automatic state tracking: Solved by `yield` keyword, which automatically handles pausing and resuming iteration between `yield` statements.
2) Automatic cleanups: Solved by implicitly handing memory.

**Generators** (an object) (a subset of a iterator) 
- `<class 'generator'>`
- A syntactic sugar to create iterators.  
```python
# Creation 
def gen_foo():
	yield 'Geeks'
	yield 'For'
	yield 'Geeks'
```

Access of items in a generator is mostly still the same as an iterator ...
```python
# Access
iterator = gen_foo(0, 10)

# next()
print(next(iterator)) # Geeks 
print(next(iterator)) # For 
print(next(iterator)) # Geeks 

# for loop
for x in iterator:
	print(iterator)

'''
Geeks 
For 
Geeks
'''
```


