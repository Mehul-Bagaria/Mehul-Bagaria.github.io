---
layout: post
title: "Basics of Mesh Adaptivity"
categories: FEniCS, Adaptivity
tag: 
  - FEniCS
---

Adaptive mesh refinement is an extraordinary methd of adaptively refining the mesh to enhance the accuracy of the solution within a certain sensitive regions in the domain.

In any adative mesh refinement scheme, there are five steps involved. They are :

* Solve - In the first step the system of euations are solved to get the unknown variables in the coarse mesh.

* Estimate - This steps deals with the estimation of error indicator as per the problem , so as to identify the sensitive regions in the mesh domain.

* Mark - In this step as per the estimated error the elements are marked for refinement based on the different marking scheme. There are different marking scheme available in the literature. Some of the very commonly used marking schemes are :
  * According to the first marker , all elements whose value of error indicator is greater than "multiplication factor \times max(error indicator)" are marked.
  * Next marker is based on the mean value of eror indicator. All elements whose value of error indicator is greater than the mean value are marked.
  * In this marking scheme some top percentage of elements with maximum error indicator are marked.
  * Next marking scheme is called as bulk criterion, where the first k elements are marked, where k is computed using the reation :

* Refine - Refine the marked elements using the selected refinement strategy.

* Check - The last step is to check for the convergence of adaptivity ,as per the given condition. The stopping criteria may vary as per the problem.

Consider a 1D problem to show the different steps of an adaptivity sheme with the help of a python code.

* Import the different packages

```python
from scipy.integrate import quad
from matplotlib.pyplot import plot
import matplotlib.pyplot as plt
%matplotlib inline
from math import atan, pi, sin, sqrt,exp
import time
```

* Different parameters required for the study .

```python
AREA,L2 = "area","l2"
estimator = L2
toll = 1e-3
toll = 1e-3
max_num_refinement = 15     # the maximum allowed number of refinement
```

* Define the element. For this study, initially we are selecting 1 element with 2 nodes.

```python
node_cord = [-pi,pi]
```

* Next is to define the function which will evaluate the exact solution.

```python
def u_exact(x):
    value = sin(x)
    return value
```

* Define the approximate solution 

```python
def u_approx(x):
    global u1,u2,x1,x2
    zi = (x-(x2+x1)/2)*(2/(x2-x1))
    N1 = (1-zi)/2
    N2 = (1+zi)/2
    return (N1*u1 + N2*u2)
```

* Estimate the error

```python
def err_function(x):
    global x2,x1
    return (u_approx(x) -u_exact(x))**2
def area (n1,n2):
    return (u_exact(n1)+u_exact(n2))/2 *(n2-n1)

def estimate_error(node_cord,ele_num):
    if estimator==AREA:
        exact_area = (quad(u_exact, node_cord[ele_num] , node_cord[ele_num+1])[0])
        approx_area = (area(node_cord[ele_num] , node_cord[ele_num+1]))
        err = exact_area - approx_area
    if estimator==L2:
        global u1,u2,x1,x2
        x1,x2 = node_cord[ele_num] , node_cord[ele_num+1]
        u1,u2 = u_exact(node_cord[ele_num]) , u_exact(node_cord[ele_num+1])
        err = sqrt(quad(err_function, x1 , x2)[0])
        #err = err/sqrt(quad(u_exact_l2, x1 , x2)[0]) # for normalising the error by dividing with exact value 
    return err
```

* Mark the elements

```python
def mark_ele_refine(err_list):
    ele_num=0
    marker = []
    for err in err_list:
        if abs(err) > toll:
            marker.append(ele_num)
        ele_num += 1
    return marker
```

* Refine the marked elements

```python
def refine_ele(node_cord,marker):
    for k in range(len(marker)):
        node_cord.append((node_cord[marker[k]] + node_cord[marker[k]+1])/2)
    node_cord.sort()
    print("new nodal coordinate ------",node_cord)
    return node_cord
```

* Mesh adaptivity loop

```python
for i in range(max_num_refinement):
    error_list =[]
    for j in range(len(node_cord)-1):
        error_list.append(estimate_error(node_cord,j))
    print("Refinement step ------", i)   
    print("error list      ------",error_list)
    marker = mark_ele_refine(error_list) 
    if len(marker)==0:
        break
    
    print("elements marked ------",marker)
    print("nodal coordinates ----",node_cord)
    node_cord = refine_ele(node_cord,marker)
			plot(node_cord,[u_exact(x) for x in node_cord], marker = "o")
```

* Results of the study for the first 5 steps:

![image-1234](../assets/images/image-1234.png)



From the above plots it is clear that extra node is inserted where there is a change in curvature, i., the error will be more in the curved regions. To get a smooth curve the nodes should be close to each other that is the reason the nodes are inserted in those regions. Similarly if you implement mesh adaptivity for any problem, the mesh will be adaptively refined where the value of error indicator is more or more sensitive regions.