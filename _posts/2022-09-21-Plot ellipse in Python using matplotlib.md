---
layout: post
title: "Plot ellipse in Python using matplotlib"
categories: coding
tag: 
  - coding
---

To plot ellipse in Python you can use the polar form of the ellipse which is

 $x = u + a cos(t) ; y = v + b sin(t)$

of the ellipse having center at (u,v):

 $\frac{(x-u)^2}{a^2} + \frac{(y-v)^2}{b^2} = 1$

First we define the x and y coordinates of the ellipse (curve), then, we plot all the points.

**Example:**

```python
import numpy as np
from matplotlib import pyplot as plt

u=0     #abcissa of center
v=0    #ordinate of center
a=2     # major axis 2a
b=1  # minor axis 2b

t = np.linspace(0, 2*np.pi, 100)
plt.plot( u+a*np.cos(t) , v+b*np.sin(t) )
plt.grid()
plt.show()
```

**Output:**

![](\assets\images\ellipse.png)

You can also rotate the ellipse in the anticlocwise direction by multiplying the array of coordinates with the rotation matrix.

**Example:**

```python
import numpy as np
from matplotlib import pyplot as plt

u=0    #abcissa of center
v=0    #ordinate of center
a=2    # major axis 2a
b=1    # minor axis 2b
t_rot=pi/4 #rotation angle

t = np.linspace(0, 2*np.pi, 100)

# Coordinates of the ellipse
Ell = np.array([a*np.cos(t) , b*np.sin(t)])  

# Rotation matrix
R_rot = np.array([[np.cos(t_rot), -np.sin(t_rot)], [np.sin(t_rot), np.cos(t_rot)]])  

Ell_rot = np.zeros((2,Ell.shape[1]))
for i in range(Ell.shape[1]):
    Ell_rot[:,i] = np.dot(R_rot,Ell[:,i])

plt.plot( u+Ell_rot[0,:] , v+Ell_rot[1,:])
plt.grid()
plt.show()
```

**Output:**

![](\assets\images\ellipse_rotated.png)

## References

* [Plot Ellipse with matplotlib.pyplot (Python) - Stack Overflow](https://stackoverflow.com/a/48409811)

* [How to Plot ellipse in python](https://www.engineerknow.com/2021/03/how-to-plot-ellipse-in-python.html)
