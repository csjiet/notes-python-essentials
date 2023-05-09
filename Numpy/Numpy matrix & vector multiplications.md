We seek to demystify multiplication operations that numpy has to offer, and delineate and distinguish its exact method of operation.

**Table of content**:
- Describes the differences and similarities between these operations
	- `*`
	- `np.multiply(a,b)` 
	- `np.dot(a,b)`
	- `np.matmul(a,b)`
	- `@`

- TLDR: -  " `*` == `np.multiply` != `np.dot` != `np.matmul` == `@`"

# Operations:

## CANNOT compute the entire dot product operation in one line, using 1 function alone, requires the help of additional operations.
1. `*`
	- Computes the "product" of elements ONLY (BUT "SUM" is not conducted)
	- Hence, `*` is a partial operation to dot product/ matrix multiplication, where the sum part is not computed after the product of elements.
	- Can be used with `sum` operations to mimic matrix multiplication
	-  `sum(a * b)` $\neq$ dot product
		- ONLY works for vectors BUT NOT MATRICES, because this effectively 
		- ***Sums up ALL ELEMENTS in the matrix***, hence returning a scalar everytime, and not retaining its resultant shape.
	- `np.sum(a * b, axis=1)` $=$ dot product
		- ***Sums up row-wise elements in the matrix (axis = 1)***

2. `np.multiply(a,b)`
	- Computes the "product" of elements ONLY
	- **Same as `*` above**. (Numpy's version advantages: ~~speed~~ , can take more arguments for more complex operations.)
	- `np.sum(np.multiply(a, b), axis=1)` $=$ dot product

> Numpy almost always have their OWN version of arithmetric operation. BUT its advantages are mostly due to its richer features control, and versatility. 

## Computes dot product BY ITSELF
4. `np.dot(a,b)` - [[Dot product numpy]]
	- Operates as: `np.sum(np.multiply(a,b), axis=1)` 
	- CAN use for matrix multiplication, 
	- BUT it might 1) stem confusion, 2) Operation **DOES NOT WORK with higher dimensional matrices with dimension >2**.
## Computes matrix multiplication BY ITSELF
1. `np.matmul(a,b)`
	1. MATRIX MULTIPLICATION of any dimension (2D or higher matrix multiplication).
	2. CAN use for dot product for vectors. 
	3. BUT use `np.dot()` to avoid confusion.
2. `@`
	1. MATRIX MULTIPLICATION of any dimension (2D or higher matrix multiplication).
	2. **Same as `np.matmul(a,b)` above**

What are the differences between "`np.dot(a,b)`" and "`np.matmul(a,b) / a @ b`"?

> **Answer**: The difference stem from the definition of their implementation, which performs different operations. The difference is unnoticable at lower dimensional operations, where their behavior conviniently overlaps to solve dot product vs matrix multiplication for easier examples:

```python
# Example at higher dimensions - 3D
# define input arrays
a = np.random.rand(3,2,2)  # 2 rows, 2 columns, in 3 layers 
b = np.random.rand(3,2,2)  # 2 rows, 2 columns, in 3 layers 

# perform matrix multiplication
c = np.dot(a, b)
d = a @ b  # Python 3.5+

# Output:
>>> c.shape  # np.dot
(3, 2, 3, 2)

>>> d.shape  # @
(3, 2, 2)
```
 
**For `np.matmul/ @`**:
> - If either argument is N-D, N > 2, it is treated as a stack of matrices residing in the last two indexes and broadcast accordingly.

```python
a:
[[[6, 3],
  [7, 4],
  [6, 9]],
	
 [[2, 6],
  [7, 4],
  [3, 7]],

 [[7, 2],
  [5, 4],
  [1, 7]],
], shape(3,3,2)

b: 
[[[5, 1, 4, 0],
  [9, 5, 8, 0]],
	
 [[9, 2, 6, 3],
  [8, 2, 4, 2]],

 [[6, 4, 8, 6],
  [1, 3, 8, 1]],
], shape(3,2,4)

a @ b

[[[57, 21, 48, 0],
  [71, 27, 60, 0],
  [111, 51, 96, 0]],
	
 [[66, 16, 36, 18],
  [95, 22, 58, 29],
  [83, 20, 46, 23]],

 [[44, 34, 72, 44],
  [34, 32, 72, 34],
  [13, 25, 64, 13]],
], shape(3,3,4)

# (3x3x2) @ (3,2,4) = (3,3,4)

```
> - The first matrix is a stack of three 2D matrices each of shape (3,2), 
> - The second matrix is a stack of three 2D matrices, each of shape (2,4).
> - The matrix multiplication between these two will involve **three multiplications** between ***corresponding 2D matrices of A and B having shapes (3,2) and (2,4) respectively***. Specifically, the first multiplication will be between A[0] and B[0], the second multiplication will be between A[1] and B[1], and finally, the third multiplication will be between A[2] and B[2]. The result of each individual multiplication of 2D matrices will be of shape (3,4). Hence, the final product of the two 3D matrices will be a matrix of shape (3,3,4).
> - In a way, it is conducts matrix multiplication for each element in axis 0.

![[numpy_mat_mul_example.png]]


 **For `np.dot`**:
> - For 2-D arrays it is equivalent to matrix multiplication, and for 1-D arrays to inner product of vectors (without complex conjugation). For N dimensions it is a sum product over the last axis of a and the second-to-last of b
> - If a is an N-D array and b is an M-D array (where M>=2), it is a sum product over the last axis of a and the second-to-last axis of b:
> - dot(a,b)[i,j,k,m]=sum(a[i,j,:]∗b[k,:,m])

```python
a:
[[[6, 3],
  [7, 4],
  [6, 9]],
	
 [[2, 6],
  [7, 4],
  [3, 7]],

 [[7, 2],
  [5, 4],
  [1, 7]],
], shape(3,3,2)

b: 
[[[5, 1, 4, 0],
  [9, 5, 8, 0]],
	
 [[9, 2, 6, 3],
  [8, 2, 4, 2]],

 [[6, 4, 8, 6],
  [1, 3, 8, 1]],
], shape(3,2,4)

a.dot(b)

[[[[ 57  21  48   0]
   [ 78  18  48  24]
   [ 39  33  72  39]]

  [[ 71  27  60   0]
   [ 95  22  58  29]
   [ 46  40  88  46]]

  [[111  51  96   0]
   [126  30  72  36]
   [ 45  51 120  45]]]


 [[[ 64  32  56   0]
   [ 66  16  36  18]
   [ 18  26  64  18]]

  [[ 71  27  60   0]
   [ 95  22  58  29]
   [ 46  40  88  46]]

  [[ 78  38  68   0]
   [ 83  20  46  23]
   [ 25  33  80  25]]]


 [[[ 53  17  44   0]
   [ 79  18  50  25]
   [ 44  34  72  44]]

  [[ 61  25  52   0]
   [ 77  18  46  23]
   [ 34  32  72  34]]

  [[ 68  36  60   0]
   [ 65  16  34  17]
   [ 13  25  64  13]]]], shape(3,3,3,4)

# (3x3x2).dot( (3,2,4) ) = (3,3,3,4)

```

> - The multiplication between this two will involve 3x3 = 9 multiplications, between the each of the 3 elements in axis 1 of shape (1,2) with the matrix in axis 0 of shape (2,4), hence generating 3 (1x4) vectors for each item in axis 0. Repeat for all elements in axis 0.
> - In a way, it takes each element (axis 0) from `a`  and for each nested element in the element, compute matrix multiplication with elements in axis 1 from `b`.

![[numpy_dot_prod_example.png]]

Resources:
- ['\*' or 'np.multiply' or 'np.dot' or 'np.matmul' or '@'](https://mkang32.github.io/python/2020/08/30/numpy-matmul.html)
- [Numpy 3D matrix multiplication example GeekForGeeks](https://www.geeksforgeeks.org/numpy-3d-matrix-multiplication/)
- 

