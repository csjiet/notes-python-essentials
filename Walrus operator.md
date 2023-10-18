Walrus operator (`:=`) - Python 3.8
 - Use: Assign a value to a variable within an expression

Normal for loop
``` python
for i in range(len(nums)):
	cnums[i] *= c
	c *= nums[i]
```
List comprehension with walrus operator
``` python
cnums = [cnums[i] * (c := nums[i]) for i in range(len(nums))]
```
- the corresponding value of `c`, which is updated in-place using the assignment expression `:=`.

