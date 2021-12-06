---
layout: post
title: "Structured and Unstructured Mesh"
categories: Gmsh
tag: 
  - Gmsh
---
---

In our work for finite element analysis, we use two types of mesh namely structured and unstructured mesh. We use Gmsh as a tool for  mesh generation. Gmsh is a open- source 3D finite element mesh generator with a built-in CAD engine and post-processor. It is very user friendly and has a very good visualisation capabilities.

## Structured Mesh 

Structured mesh are identified by regular connectivity.  This method is highly space efficient, since the neighbourhood relationships are uniform. In structured mesh the size of all the elements are uniform. This meshing type is normally used for regular geometries, and the computational efficiency can be increased.

## Unstructured Mesh

Unstructured mesh are mostly adopted where the geometry is complex and irregular. In this type of mesh the element size is not uniform and in complex structures where we require localised dense meshing in some particular locations.  It demands for higher memory requirement, thus effects the computational efficiency.        

## Example :

The mesh generation procedure is explained using a rectangular specimen.

1. Create the coordinates of point (rectangle with 4 points).

    

   ```
   Point(Id) = {x, y, z, mesh size}
   
   Point(1) = {1, 0, 0,0.5};
   
   Point(2) = {1, 1, 0, 0.5};
   
   Point(3) = {0, 1, 0, 0.5};
   
   Point(4) = {0, 0, 0, 0.005};
   ```

2. Then the coordinate points are joined using line .

   ```
   Line(Id) = {starting point id , end point id}
   Line(1) = {1, 2};
   Line(2) = {2, 3};
   Line(3) = {3, 4};
   Line(4) = {4, 1};
   ```

3. The lines are joined, making a close loop.

   ```
   Curve Loop(Id) = {Ids of line/ curve};
   Curve Loop(1) = {2, 3, 4, 1};
   ```

4. Create a plane surface

   ```
   Plane Surface(Id) = {Id of the curve loop};
   Plane Surface(1) = {1};
   ```

5. We use Transfinite Curve to make structured mesh, use the following two lines and get a structured mesh. 

   ```
   Transfinite Curve {Ids of the curve} = No. of divisions one line should be divided;
   Transfinite Surface {Id of the plane surface
   Transfinite Curve {1 :4} = 10;
   Transfinite Surface {1};
   ```

   ![image-20210125200430015](../assets/images/image-20210125200430015.png)

   ​																				Structured Mesh



![image-20210125212304692](../assets/images/image-20210125212304692-1805652.png)

​																					Unstructured Mesh