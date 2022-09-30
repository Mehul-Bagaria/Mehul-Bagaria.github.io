---
layout: post
title: "Plot lines using coordinates in Python"
categories: coding
tag: 
  - coding
---

In Python, there are multiple ways to  plot a curve, you can plot by defining the function or you can give the coordinates of the curve.

If you know the coordinate of the straight line, then you can plot that directly use `matplotlib` module.

**Syntax:** `plt.plot(x_values, y_values, '-o', color = 'b', linestyle = '--' )`

`x_values` and `y_values` are the points abscissa and ordinates written in the form of `list` or `tuple`.

`color = 'b'` and `linestyle = '--'` are optional arguments.

**Example:**

```python
import matplotlib.pyplot as plt

point_1 = [0,0]
point_2 = [1,1]
point_3 = [2,4]
point_4 = [5,6]

plt.plot([point_1[0], point_2[0], point_3[0], point_4[0]],[point_1[1], point_2[1], point_3[1], point_4[1]],'-o', color = 'b',linestyle = '--' )
plt.show()
```

**Output:**

![](\assets\images\plot_coordinates.png)

## References

* [Kite](https://www.adamsmith.haus/python/answers/how-to-draw-a-line-between-two-points-in-matplotlib-in-python)

* [How do you create line segments between two points in Matplotlib?](https://www.tutorialspoint.com/how-do-you-create-line-segments-between-two-points-in-matplotlib)
