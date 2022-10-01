---
layout: post
title: "What is Python's Numpy function zeros()?"
categories: coding
tag: 
  - coding
---

np.zeros() generate the array of given shape and type, with zeros being its elements.

Syntax: `numpy.zeros(shape, d_type = None, order = 'C')`

where, `shape` defines the dimension of array, it can be integer or sequence. $[2,3]$ for generating the $2 \times 3$ matrix.

`data_type` defines whether it is integer or float (default).

`order` defines whether to store in row-major (default) or coloumn major.

Example:

```python
import numpy as np

np.zeros([2,3], dtype='int')
```

Output:

![](C:\Users\User\AppData\Roaming\marktext\images\2022-10-01-12-11-45-image.png) 

Example:

```python
import numpy as np

np.zeros(2, dtype='int')
```

Output:

![](C:\Users\User\AppData\Roaming\marktext\images\2022-10-01-12-12-28-image.png)

## References

* [numpy.zeros() in Python - GeeksforGeeks](https://www.geeksforgeeks.org/numpy-zeros-python/)

* [numpy.zeros &#8212; NumPy v1.23 Manual](https://numpy.org/doc/stable/reference/generated/numpy.zeros.html)
