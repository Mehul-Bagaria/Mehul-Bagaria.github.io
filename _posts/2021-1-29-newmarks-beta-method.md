---
layout: post
title: "Newmark's Beta Method"
categories: Mathematics
tag: 
  - Mathematics
---
---

In Newmark's Beta method there are two special cases:

1. Average acceleration method : 
   $$
   \alpha = 1/2 \\
   \beta  = 1/4
   $$
   

2. Linear acceleration method: 

$$
\alpha = 1/2 \\
\beta  = 1/6
$$

These parameters define the variation of acceleration over a time step and determine the stability and accuracy characteristics of the method. 

The general equation for SDOF problem  is written as :
$$
m \ddot{u}_{t+1}+c \dot{u}_{i+1}+k {u}_{i+1}=p_{i+1}
$$
We can calculate the (i+1) terms using the i^th^ terms.

## Steps involved in the calculation:

1. Initial calculations:
   $$
   \ddot{u}_{0}=\frac{p_{0}-c \dot{u_{0}}-k{u_{0}}}{m_{0}}
   $$
   

   ​			Select $\Delta$ t

$$
\begin{array}{l}
a=\frac{1}{\beta \Delta t} m+\frac{\nu}{\beta} c ; \ \\
b=\frac{1}{2 \beta} m+\Delta t\left(\frac{\nu}{2 \beta}-1\right) c .
\end{array}
$$

2. Calculate for each time step.
   $$
   \Delta \hat{\rho}_{i}=\Delta p_{i}+a \dot{u}_{i}+b \ddot{u}_{i}
   $$
   Determine for tangent stiffness k~i~
   $$
   \hat{k}_{i}=k_{i}+\frac{\nu}{\beta \Delta t} C+\frac{1}{\beta(\Delta t)^{2}} m
   \\
   \Delta \dot{u}_{i} =\frac{\gamma}{\beta \Delta t} \Delta u_{i}-\frac{\gamma}{\beta} \dot{u}_{i}+\Delta t\left(1-\frac{\gamma}{2 \beta}\right) \ddot{u}_{i}
   \\
   
   \Delta \ddot{u}_{i} =\frac{1}{\beta(\Delta t)^{2}} \Delta u_{i}-\frac{1}{\beta \cdot \Delta t} \dot{u}_{i}-\frac{1}{2 \beta} \ddot{u}_{i}
   $$
   

3. Repeat this cycle for the next steps. 

