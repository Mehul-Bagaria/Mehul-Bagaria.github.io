---
layout: post
title: "Implementing Floquet Periodicity in FEniCS or FEniCSx"
categories: wave mechanics
tag: 
  - wave
---

When analyzing **wave propagation** inside a **periodic structure**, one may consider the analysis over a single section or a unit cell instead of the complete domain, by considering the appropriate periodicity at the boundaries. This approach reduces the domain of analysis and simplifies the problem. 

By implementing the **Floquet-periodicity**, we can analyze wave propagation (mechanical waves or electromagnetic waves) within any material. This approach when coupled with **FEniCS**, will enable the analysis of any periodic structure under wave mechanics physics.



## Theory

Bloch theorem describes the behavior of the wave propagation inside a periodic structure are analogous to plane wave modulated by a periodic function, which can be described mathematically as

$$
\psi(\mathbf{r})=\mathrm{e}^{\mathrm{ik} \cdot \mathbf{r}} u(\mathbf{r})
$$

where, $$\psi(\mathbf{r})$$ is the overall field {combination of plane wave and periodic function}

$$\mathrm{e}^{\mathrm{ik} \cdot \mathbf{r}}$$ is the plane wave {Bloch wave vector}

$$u(\mathbf{r})$$ is the envelop function {takes the periodicity and symmetry of the periodic structure}.

**Bloch-floquet theory** or **periodicity** provides a methodology to analyze the wave propagation by just considering a single unit cell and applying the following boundary condition as 

$$
u(\mathbf{r}+\mathbf{R})=u(\mathbf{r}) e^{i \mathbf{k} \mathbf{r}}
$$

where, $$u()$$ is the field variable, $$\mathbf{r}$$ is the spatial coordinates of the boundaries, $$R$$ is the periodicity, and $$k$$ is the wavenumber.

Wavenumber can be defined as the number of waves per unit length and is written as 

$$
k = \frac{1}{\lambda}
$$

A structure is considered **periodic **if its material properties repeat after certain intervals. 

Consider a unit cell as shown in below having periodicity $$R$$ equal to $$1$$ and the boundary value at left and right be $$u_l$$ and $$u_r$$, respectively. Then above equation reduces to 

$$
u(\mathbf{r}+1)=u(\mathbf{r}) e^{i \mathbf{k} \mathbf{r}}
$$

![](/assets/images/floquet-periodicity-1.png)

Considering the value of $$r$$ to be 1 at the left most side, then above equation becomes 

$$
u_r=u_l e^{i \mathbf{k}}
$$

## References

[How to implement Bloch-Floquet Boundary condition? - FEniCS Project](https://fenicsproject.discourse.group/t/how-to-implement-bloch-floquet-boundary-condition/1504)

[Bloch Floquet Boundary condition / Perfect Matching Layer - FEniCS Project](https://fenicsproject.discourse.group/t/bloch-floquet-boundary-condition-perfect-matching-layer/497)


So, the question remains. **How to implement Floquet-Periodicity in FEniCS  or FEniCSx?**
