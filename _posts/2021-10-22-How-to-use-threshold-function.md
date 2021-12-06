---
layout: post
title: "How to use threshold for local meshing in Gmsh"
categories: Gmsh
tag: 
  - Gmsh
---

Mesh refinement is **an important tool for editing finite element meshes** in order to increase the accuracy of the solution. In regions where stress is concentrated or in the critical regions the elements have to be refined locally. In such cases we need to use this function. In this post I will consider the plate with a hole problem, which I had explained the modeling and meshing part in the previous post. 

Problem statement:

A rectangular section of size 2 X 1, with a hole at center (1, 0.5) of diameter 0.5.The element size along the boundary of hole is refined. 

Steps:

* Create points as per your geometry. For this go to Modules --- Geometry --- Elementary entities --- Add --- Point. You will see a dialogue box opened, just enter the coordinates of each point and click on add.

* After creating all point next step is to join all those point using line to form a complete geometry. For this Go to Modules --- Geometry --- Elementary entities --- Add --- Line. Follow the instructions shown on the screen, i.e you have to select the start and end point of the line. 

* Create the hole using the circle option. For this Go to Modules --- Geometry --- Elementary entities --- Add ---  Circle. Just enter the coordinates of center point and radius of circle.

* Next step is to create a Plane surface.  For this Go to Modules --- Geometry --- Elementary entities --- Add --- Plane Surface. Then select the surface boundary of the rectangle and then select the circle boundary and then press 'e' to end selection. 

* After this step open the script and add the threshold meshing script given below. Just change the DistMax, DistMin, LcMax and LcMin as per the requirement. 

  ```python
  #Threshold script
  Field[1] = Distance;
  Field[1].NNodesByEdge = 1000;
  Field[1].EdgesList = {5};
  Field[2] = Threshold;
  Field[2].DistMax = 1;
  Field[2].DistMin = 0.2;
  Field[2].IField = 1;
  Field[2].LcMax = 0.1;
  Field[2].LcMin = 0.1/10;
  
  Background Field = 2;
  ```

  

* For 2D geometries it is very important to define Physical group for the created surface. For this Go to Modules --- Geometry --- Physical groups --- Add --- Surface --- Give a proper name tag -- select the surface  and press 'e' to add. 

* Next step is for meshing. You can simply go to  Modules --- Mesh --- 1D --- 2D. 

* Last and final step is to save the mesh. 

The file generated here will be saved in .msh format, which you can further convert into xdmf with the help of "Meshio" and you are good to import this mesh file in FEniCS. 

Script :

```python
Point(1) = {0, 0, 0, 1.0};
Point(2) = {2, 0, 0, 1.0};
Point(3) = {2, 1, 0, 1.0};
Point(4) = {0, 1, 0, 1.0};

Line(1) = {1, 2};
Line(2) = {2, 3};
Line(3) = {3, 4};
Line(4) = {4, 1};

Circle(5) = {1, 0.5, 0, 0.25, 0, 2*Pi};

Curve Loop(1) = {3, 4, 1, 2};
Curve Loop(2) = {5};
Plane Surface(1) = {1, 2};

#Threshold script
Field[1] = Distance;
Field[1].NNodesByEdge = 1000;
Field[1].EdgesList = {5};
Field[2] = Threshold;
Field[2].DistMax = 1;
Field[2].DistMin = 0.2;
Field[2].IField = 1;
Field[2].LcMax = 0.1;
Field[2].LcMin = 0.1/10;

Background Field = 2;

Physical Surface("domain", 6) = {1};
```

