---
layout: post
title: "How to use XDMF file to save multiple solutions in the same mesh "
categories: FEniCS
tag: 
  - FEniCS
---



In our workflow ,  we use FEniCS  for solving differential equations. To visualise the results we save the output variables into a XDMF file. And the XDMF file is visualised in the Paraview. 

Use this command to create the xdmf file.

```python
xdmf = XDMFFile("output/" +  "output_" + ".xdmf")
```

When we have more than one variable to save in the same xdmf file, we need to share the mesh for multiple variables. 

```python
xdmf.parameters["flush_output"] = True
xdmf.parameters["functions_share_mesh"] = True
xdmf.parameters["rewrite_function_mesh"] = False
```

Then use the following command to write the data in the file:

```python
xdmf.write(pnew, disp_current)
xdmf.write(unew, disp_current)
```

