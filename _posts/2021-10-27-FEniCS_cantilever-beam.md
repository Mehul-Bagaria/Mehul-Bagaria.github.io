---
layout: post
title: "FEniCS implementation of a cantilever beam with point load"
categories: FEniCS
tag: 
  - FEniCS
---
In this post I have documented a simple cantilever beam with a point load, applied at the end of the beam. I have understood this implementation with the help of the excellent document "Numerical tours of continuum mechanics using FEniCS by Jeremy Bleyer".

I have considered a cantilever beam of size 25 X 5 cross section, with a point load of 5 N applied at the free end. 

Code :

Create the mesh using the inbuilt mesh "RectangleMesh"

```python
from dolfin import *
L = 25.
H = 5.
Nx = 250
Ny = 10
mesh = RectangleMesh(Point(0., 0.), Point(L, H), Nx, Ny, "crossed")
plot(mesh)
```

Define the constitutive relation

```python
def eps(v):
    return sym(grad(v))
  
E = Constant(1e5)
nu = Constant(0.3)
model = "plane_stress"
mu = E/2/(1+nu)
lmbda = E*nu/(1+nu)/(1-2*nu)
if model == "plane_stress":
    lmbda = 2*mu*lmbda/(lmbda+2*mu)
def sigma(v):
    return lmbda*tr(eps(v))*Identity(2) + 2.0*mu*eps(v)
 
rhog = 1
f = Constant((0, -rhog))
```

Define the boundary conditions.

```python
left = CompiledSubDomain("near(x[0], 0)  && on_boundary")
right = CompiledSubDomain("near(x[0], 24.5, 0.5) && near(x[1], 1)")

mf = MeshFunction("size_t", mesh, mesh.topology().dim() - 2)
mf.set_all(0)
right.mark(mf, 2)
ds = Measure("ds")(subdomain_data=mf)

V = VectorFunctionSpace(mesh, 'Lagrange', degree=2)
bc_left = DirichletBC(V, Constant((0.,0.)), left)
bc_right = DirichletBC(V, Constant((0.,-5)), right, method = "pointwise")

bc = [bc_left, bc_right]
```

Define the variational form 

```python
v = TrialFunction(V)
u = TestFunction(V)
a = inner(sigma(v), eps(u))*dx
l = inner(f, u)*dx
```

Solve 

```python
u_sol = Function(V, name="Displacement")
solve(a == l, u_sol, bc)
plot(u_sol)
print(u_sol.vector()[:])
print(u_sol.vector().max())
```

![u_disp](/Users/meenu/Codes/umeenukrishnan.github.io/assets/images/u_disp.png)

