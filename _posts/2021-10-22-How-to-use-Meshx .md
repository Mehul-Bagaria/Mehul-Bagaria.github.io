---
layout: post
title: "How to use Meshx to convert the .msh file to .xdmf file"
categories: Gmsh, Meshx
tag: 
  - Meshx
---

In FEniCS we have an option of importing the mesh geometry in .xdmf format. This makes our job much more easier and simpler. As it allows us to use different packages (Gmsh, Ansys, Abaqus etc) for complex geometry modeling and meshing. Check

[this post]: https://computationalmechanics.in/easy-way-to-import-mesh-file-of-complex-geometries-from-ansys-to-fenics/

to know how to use Nastran file (.bdf) from Ansys to FEniCS.  

In this post I will mainly focus on Gmsh because thats what I mostly prefer to use as it is an open source  GUI based package. 

## Meshx

A simple tool to convert mesh created from Gmsh to XDMF for use in FEniCS. You can get the complete installation instruction 

[here]: https://github.com/iitrabhi/meshx



### Step by step procedure : 

1. Create the mesh file in Gmsh. Mark all the different boundary and loading condition using the different Physical groups in Gmsh. 

   ​	Example : Consider a rectangle section with four boundary condition, and two materials.  As shown in figure :

   

![](D:\Codes\Meenu\umeenukrishnan.github.io\assets\images\meshx.png)

Script for this is :

```python
Point(1) = {0, 0, 0, 1};
Point(2) = {1, 0, 0, 1};
Point(3) = {1, 1, 0, 1};
Point(4) = {0, 1, 0, 1};
Point(5) = {1, 0.75, 0, 1};
Point(6) = {1, 0.5, 0, 1};
Point(7) = {0.5, 0.5, 0, 1};
Point(8) = {0.5, 0.75, 0, 1};

Line(1) = {1, 2};
Line(2) = {2, 6};
Line(3) = {6, 7};
Line(4) = {7, 8};
Line(5) = {8, 5};
Line(6) = {5, 6};
Line(7) = {5, 3};
Line(8) = {3, 4};
Line(9) = {4, 1};

Curve Loop(1) = {8, 9, 1, 2, 3, 4, 5, 7};
Plane Surface(1) = {1};
Curve Loop(2) = {5, 6, 3, 4};
Plane Surface(2) = {2};

Physical Curve("top", 10) = {8};
Physical Curve("left", 11) = {9};
Physical Curve("right", 12) = {7, 6, 2};
Physical Curve("bottom", 13) = {1};

Physical Surface("Domain", 14) = {1};
Physical Surface("Obstacle", 15) = {2};

```



2. After creating the .msh file from gmsh. Open the temrinal and go to the folder containing the .msh file and use the following command to convert .msh to .xdmf file .

   ```
   meshx plate.msh
   ```

   ![](D:\Codes\Meenu\umeenukrishnan.github.io\assets\images\meshx_terminal.png)

![](D:\Codes\Meenu\umeenukrishnan.github.io\assets\images\meshx_folder.png)

As a output you will be getting two folders namely - "mesh and sub_domains". All the files in mesh folder is used in the main script and the files in the sub_domains folder can be used to ensure if all the different sub domains are marked properly by visualizing the .xdmf file in Paraview. 

3. In FEniCS, we can make use of this by creating the mesh function corresponding to the mesh entities. 

   In this case we are marking the boundary condition in curve mesh entity and the material subdomain is marked in the surface mesh entity. So you have to create two mesh function corresponding to curve and surface mesh entity. 

   ```python
   # Define mesh
   mesh = Mesh()
   with XDMFFile("mesh/triangle.xdmf") as infile:
       infile.read(mesh)
   
   # mesh value collection.
   mvc_1 = MeshValueCollection("size_t", mesh, 1) #for curve with dim 1
   mvc_2 = MeshValueCollection("size_t", mesh, 2) #for surface with dim 2
   
   #import the json file so that tag names can be used
   f = open('mesh/tags.json') 
   tags = json.load(f)
   
   with XDMFFile("mesh/line.xdmf") as infile:
       print("Reading 1d line data into dolfin mvc")
       infile.read(mvc_1, "tag")
   
   print("Constructing MeshFunction from MeshValueCollection")
   boundaries = cpp.mesh.MeshFunctionSizet(mesh, mvc_1) # creating mesh function for curve 
   
   with XDMFFile("mesh/triangle.xdmf") as infile:
       print("Reading 2d surface data into dolfin mvc")
       infile.read(mvc_2, "tag")
   
   print("Constructing MeshFunction from MeshValueCollection")
   domains = cpp.mesh.MeshFunctionSizet(mesh, mvc_2) # creating mesh function for surface 
   
   #--------------------------------------------------------------------------------------------------------------------------------
   
   # Define Dirichlet boundary conditions at top and bottom boundaries
   bcs = [DirichletBC(V, 5.0, boundaries, tags['Top']),
          DirichletBC(V, 0.0, boundaries, tags['Bottom'])]
   
   #--------------------------------------------------------------------------------------------------------------------------------
   
   # Define new measures associated with the interior domains and
   # exterior boundaries
   dx = Measure("dx")(subdomain_data=domains)
   ds = Measure("ds")(subdomain_data=boundaries)
   
   #--------------------------------------------------------------------------------------------------------------------------------
   
   # Define variational form
   F = (inner(a0*grad(u), grad(v))*dx(tags['Domain']) + inner(a1*grad(u), grad(v))*dx(tags['Obstacle'])
        - g_L*v*ds(tags['Left']) - g_R*v*ds(tags['Right'])
        - f*v*dx(tags['Domain']) - f*v*dx(tags['Obstacle']))
   ```

   

So I hope you get an idea how to use Meshx, If you are working with FEniCS. 