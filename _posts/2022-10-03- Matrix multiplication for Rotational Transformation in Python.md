---
layout: post
title: "Matrix multiplication for Rotational Transformation in Python"
categories: coding
tag: 
  - coding
---

In Python, whenever you wish to rotate any plot, you can do that with the help of Rotational Transformation. In Rotational Tranformation, the input coordinate matrix is multiplied with a Transformation (Rotation) matrix. 

$ [A]_{Rotated} = [A][T]_{Rotation}$

where, $[A]_{Rotated}$ is the output transformed matrix that contains coorindates of plot, rotated by certain angle.

$[A]$ is the input matrix containing initial coordinates and $[T]_{Rotation}$ is the tranformation matrix that contains array of $sin(\theta) \text{ and } cos(\theta)$.

## References

* 
