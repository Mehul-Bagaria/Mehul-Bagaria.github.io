---
layout: post
title: "How to add interactive widgets in Jupyter Notebook?"
categories: coding
tag: 
  - coding
---

In Jupyter notebook, you can add interactive widgets to visualize and manipulate codes and data. 

[ipywidgets](https://github.com/jupyter-widgets/ipywidgets) module provides bundles of various widgets that can be used for taking input and displaying outputs. 

Various widgets that are available:

* Sliders 

* Check boxes

* Dropdowns

* Selection Range sliders

* Toggle buttons etc.
  
  

`interact` function in `ipywidgets` module generates user interface (UI) for interactive input and function manipulation. For example, the movement in slider can change the input value of the function and generates the corresponding output.

*Syntex:* `interact(f, x = a)`, where `f` is the function having argument `x`. The slider generated will have limit -a to 3a.

*Syntex:* `interact(f, x=(min, max, steps))`

```python
from ipywidgets import interact, interactive, fixed, interact_manual
import ipywidgets as widget

import matplotlib.pyplot as plt
import numpy as nps


# Define function with argument as polynomial order
def poly_f(m):
    x = np.linspace(-10,10,100)
    y = x**m
    plt.plot(x,y, '-b', label = 'y=x^'+ str(m))
    plt.grid()
    plt.legend()  


# Interact function with arguments - function (f) and f's argument x.
interact(poly_f, m =(-4,4))
```

The output will be a slider to manipulate the argument (order of polynomial) value. And it will alter the plot based on the argument value.

![](\assets\images\ipywidgets_slider.png)



## References

* [Example Github repo](https://github.com/Mehul-Bagaria/Python_lessons/blob/main/7_UI_controlled_input.ipynb)

* [Jupyter Widgets &mdash; Jupyter Widgets 8.0.2 documentation](https://ipywidgets.readthedocs.io/en/stable/index.html)

* [How to create buttons in Jupyter? - GeeksforGeeks](https://www.geeksforgeeks.org/how-to-create-buttons-in-jupyter/)
