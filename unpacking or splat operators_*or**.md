Resources:
- [YT, Real Python: Unpacking with asterisk operators in python](https://www.youtube.com/watch?v=K5XHaoROxI4)

## Introduction
`* or **`: Operators that "unpack" elements within iterable objects/ iterable variables in Python.

#### Use cases: 
***Passing unpacked elements as individual arguments to a function.***

# `*` 
Strips away the "iterable housing" revealing each individual elements separately within the iterable.
- Python *Iterables*: (list, tuples, sets, dictionaries, strings)
## Syntax: 
``` python
*var_iter1
```
## Examples:

#### Example 1: What is being unpacked? 
> Elements at axis 0 of the iterable is unpacked.

> Rules: 
> - Assigned variable must be a list or tuple
``` python
# Unpacking a list
l1 = [1,2,3]
print(l1) # Output: [1,2,3]
print(*l1) # Output: 1 2 3 
```

```python
# Unpacking a matrix 
l1 = [[1,2,3],[4,5,6]]
print(*l1) # Output: [1,2,3] [4,5,6]
```

```python
# Unpacking a string 
var = [*"Hello"]

print(var) # Output: ['H', 'e', 'l', 'l', 'o']
```


#### Example 2: Functions that take in an exact number of arguments
```python
# Unpacking a list as arguments to a function

def my_sum(a, b, c):
	print(a+b+c)

l1 = [1,2,3]
my_sum(*l1) # Output: 6

l2 = [1,2,3,4]
my_sum(*l2) # Output: TypeError: my_sum() takes 3 positional arguments but 4 were given 

```

#### Example 3: Functions that can take in a variable (n) number of arguments
``` python
# Unpacking a list as arguments to a function

def my_sum(*args):
    print('*********************')
    print(args)
    print(*args)
    print(type(args))
    result = 0
    for x in args:
        result += x
    return result
    
list1 = [1,2,3]
list2 = [4,5]
list3 = [6,7,8,9]
print(my_sum(*list1, *list2, *list3))

'''
*********************
(1, 2, 3, 4, 5, 6, 7, 8, 9)
1 2 3 4 5 6 7 8 9
<class 'tuple'>
45
'''
```
> Above: 3 lists are unpacked and passed into my_sum() as argument - `1 2 3 4 5 6 7 8 9`, where ***Python combines the unpacked elements into a single tuple and passes that tuple as the `args` parameter*** to the function - `(1,2,3,4,5,6,7,8,9)`. 
> When it encounters `*args` in `my_sum()`'s function definition, it it unpacks elements in the tuple to reveal `1 2 3 4 5 6 7 8 9` as separate elements.
> Why does Python combine unpacked elements into a single tuple **by default**?
> - To maintain consistency and behavior of code - since `*var` always reveals the unpacked elements of an iterable, `var` should always represent an iterable. Hence, it packs it in a tuple by default before passing it into function parameter `*args*`.

``` python
# zip() also takes a variable number of arguments
lst = [[1,2,3,4,5],
	  ['a','b','c','d','e']]

for a,b in zip(*lst):
	print(a,b)
'''
Output:
1 a
2 b
3 c
4 d
5 e 
'''
```

#### Example 4: Store an iterable into multiple individual variables 
``` python
lst1 = [1,2,3,4,5,6]
a, *b, c = lst1

print(a) # Output: 1
print(b) # Output: [2,3,4,5]
print(a) # Output: 6
```
> Note: The **first** and **last** variables above are called ***mandatory variables***, as they must be assigned concrete values. The **middle** variable, due to using the * or unpacking operator, can have any number of values, including zero. If there are not enough values to unpack for the mandatory variables, we will get a ValueError.

``` python
# Caveat: This style of mergining lists is INEFFICIENT as it creates a new list to store the merged list.
# Solution: .extend()
lst1 = [1,2,3]
lst2 = [4,5,6]

merged_lst = [*lst1, *lst2]

print(merged_lst) # Output: [1,2,3,4,5,6]
```

#### Example 5: Store unpacked values into one individual variable
``` python
*names, = ‘Michael’, ‘John’, ‘Nancy’
print(names) # Output: ['Michael', 'John', 'Nancy']
```

#### Example 6: Unpack an assigned iterable and store it in an iterable?
> Left hand side of the assignment must be a tuple or list. And the trailing comma after `*names`  makes it a list.
``` python
'''
This syntax is allowed, as the resulting variable is a list/ tuple. In this case, a tuple.
BUT NOT ENCOURAGED - due to bad readability.
'''

*a, = "Hello"
print(a) # Output: ['H', 'e', 'l', 'l', 'o']

*f, = [1,2,3,4,5]
print(f) # Output: [1, 2, 3, 4, 5]
```

# `**` 
- Can be applied to dictionaries only
## Examples:
#### Example 1: What is being unpacked?
``` python
num_dict = {‘a’: 1, ‘b’: 2, ‘c’: 3}
print(*num_dict) # Output: a b c
```
> One `*` only unpacks the keys in a dictionary.

#### Example 4: Collecting and storing iterable objects 
```python
dictionary1 = {"A": 1, "B": 2}
dictionary2 = {"C": 3, "D": 4}

merged_dictionary = {**dictionary1, **dictionary2}
print(merged_dictionary)

'''
Output:
{'A': 1, 'B': 2, 'C': 3, 'D':4 }
'''
```
