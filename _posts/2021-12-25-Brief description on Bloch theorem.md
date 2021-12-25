---
layout: post
title: "Brief description on Bloch theorem"
categories: wave mechanics
tag: 
  - wave
---



### Bloch wave

Waves propagating in the periodic structure takes on the symmetry and periodicity of the medium or the host.

![Bloch wave propagation](/assets/images/bloch_1.png)



### Bloch theorem

The propagation of wave inside  periodic structure are analogous to plane wave, and the envelop function $$u(\mathbf{r})$$ takes in the effects of periodicity and symmetry within the structure.
$$
\psi(\mathbf{r})=\mathrm{e}^{\mathrm{i} \mathbf{k} \cdot \mathbf{r}} u(\mathbf{r})
$$
where, $$\psi(\mathbf{r})$$ is the overall field {combination of plane wave and periodic function}

​			$$u(\mathbf{r})$$ is the plane wave {Bloch wave vector}

​			$$\mathrm{e}^{\mathrm{i} \mathbf{k} \cdot \mathbf{r}}$$  is the envelop function {takes the periodicity and symmetry of the periodic structure}



#### Periodicity 

A structure is considered periodic, if it's material properties repeat after certain intervals. 
$$
\varepsilon( \mathbf{r} + \mathbf{t_{pqr}} ) = \varepsilon (\mathbf{r})
$$
where, $$\mathbf {t_{pqr}}$$ is the periodicity of the structure.

​			$$\mathbf{\varepsilon}$$ is the permittivity of the material.

Amplitude $$A$$ of the Bloch wave will have the same periodicity as the structure, where wave is propagating.
$$
A( \mathbf{r} + \mathbf{t_{pqr}} ) = A (\mathbf{r})
$$
**Example :** Diffraction grating (periodic in one direction)
$$
\varepsilon( \mathbf{x} + \mathbf{\Lambda_{pqr}} ) = \varepsilon (\mathbf{x})
$$
![Diffraction grating](/assets/images/bloch_2.png)

### Band diagram

Plot between the normalized frequencies (eigen values) and the Bloch wave vector $$\mathbf{\beta}$$ .

![EM solver](/assets/images/bloch_3.png)

Steps - 

* take small step around the IBZ
* compute the eigen values at each step
* plot eigen values as a function of $$\beta$$





*Moving horizontally in X-axis, the periodicity and the direction of the wave propagation changes.*

**Five properties that can be estimated from band diagram -** 

* Band gap -  abscence of any band within a range of  frequencies.
* Transmission / reflection spectra - bandgap leads to suppressed transmission and enhanced reflection.
* Phase velocity
* Group velocity
* Dispersion

*Full band diagram is 3D*

### Phase v/s Power flow - 

![Phase v/s power flow]0(/assets/images/bloch_5.png)

- Phase propagates in the direction of $$\mathbf k$$.
- Power propagates in the direction of the poynting vector $$\mathbf{\zeta}$$ , which is normal to the surface of the index ellipsoid. 

**Example - ** self collimation, where wave is forced to move straight (in the direction of the power $$\mathbf{\zeta}$$ )

​					negative refractive index 

![Negative refraction](/assets/images/bloch_6.png)

