---
layout: post
title: "How to model a simple geometry in Gmsh"
categories: Gmsh
tag: 
  - Gmsh
---

Meshing is the most important part of the finite element analysis. We use Gmsh as a tool for  mesh generation. Gmsh is a open- source 3D finite element mesh generator with a built-in CAD engine and post-processor. It is very user friendly and has a very good visualisation capabilities. 

In this post I will explain simple steps which you can adopt to model and mesh a simple geometry in Gmsh. 

Steps:

* Create the layout of the geometry with proper dimensioning and coordinates. In this I will be considering the a rectangular geometry with dimension L = 2 and B = 1. 

* Create points as per your geometry. For this go to Modules --- Geometry --- Elementary entities --- Add --- Point. You will see a dialogue box opened, just enter the coordinates of each point and click on add.
* After creating all point next step is to join all those point using line to form a complete geometry. For this Go to Modules --- Geometry --- Elementary entities --- Add --- Line. Follow the instructions shown on the screen, i.e you have to select the start and end point of the line. 
* Next step is to create a Plane surface.  For this Go to Modules --- Geometry --- Elementary entities --- Add --- Plane Surface. Then select the surface boundary and press 'e' to end selection. 
* For 2D geometries it is very important to define Physical group for the created surface. For this Go to Modules --- Geometry --- Physical groups --- Add --- Surface --- Give a proper name tag -- select the surface  and press 'e' to add. 
* Next step is for meshing. You can simply go to  Modules --- Mesh --- 1D --- 2D. 
* Last and final step is to save the mesh. 

The file generated here will be saved in .msh format, which you can further convert into xdmf with the help of "Meshio" and you are good to import this mesh file in FEniCS. 

Script is given below :

```python
Point(1) = {0, 0, 0, 1.0};
Point(2) = {2, 0, 0, 1.0};
Point(3) = {2, 1, 0, 1.0};
Point(4) = {0, 1, 0, 1.0};

Line(1) = {1, 2};
Line(2) = {2, 3};
Line(3) = {3, 4};
Line(4) = {4, 1};

Curve Loop(1) = {3, 4, 1, 2};
Plane Surface(1) = {1};

Physical Surface("domain", 5) = {1};

```
