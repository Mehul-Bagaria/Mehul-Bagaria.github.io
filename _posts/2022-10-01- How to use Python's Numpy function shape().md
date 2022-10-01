---
layout: post
title: "How to use Python's Numpy function shape()?"
categories: coding
tag: 
  - coding
---

When using array in Python, there can be instances when you need to find the dimension of the array. In that case you can use shape function.

## Shape and Dimension of an array

Array is the arrangement of data in a defined form. It is characterized by it's **dimension** and number of elements in those dimensions.

 The dimension defines the number of subscripts or indices required to specify an element of that array.

The shape of any array tells the number of elements in each dimensions. 

**Example:** let's consider an array $[A]_{4 \times 3}$. This array is having dimension $2$ that means each of its element will require two numbers to specify its location in array. And each of its dimension is having $4 \text{ and } 3$ elements, respectively.

## shape() function

The `shape()` function returns the tuple, the elements of the whcih, defines the number of elements in each dimension.

There are two approaches to use the `shape()` function:

* **Finding the shape of array:** When you need to find the shape of the array. This returns the output in `tuple`.

* **Finding the number of elements in particular dimension of array:** When you need to find number of elements in particular dimension. This returns the output in `int`.

**Syntax:** `np.shape(array_name)`

**Example:**

```python
import numpy as np

A = np.array([[4,1,3,5],[5,2,5,7]])
np.shape(A)
```

**Output:**

![](\assets\images\np_shape_example1.png)

This returns the shape of array, i.e. $2 \times 3$. But, when you need to elements in particular dimension then, you use the following approach.

**Syntax:** `array_name.shape(dimension)`

**Example:**

```python
import numpy as np

A = np.array([[4,1,3,5],[5,2,5,7]])
A.shape[1]
```

**Output:**

![](\assets\images\np_shape_example2.png)

`A.shape(1)` returns the number of elements in the 1st dimension of the array.

## References

* [NumPy Array Shape - GeeksforGeeks](https://www.geeksforgeeks.org/numpy-array-shape/)
