---
layout: post
title: "FEniCS How to start"
categories: FEniCS
tag: 
  - FEniCS
---
FEniCS is a very popular open source computing platform. I have been using FEniCS for my research work. And it is very interesting that each day brings a new aspect of this incredible software. In this post I am writing some very important points in which I usually do mistakes, hoping that this may help some of you. 

There are three key commands which can help you to understand in depth about the different in built functions available in FEniCS, they are :

```python
1. dir()
2. help()
3. type()
```

 One can use this three commands to understand any function correctly in FEniCS, this will be a great help for the beginners to know the proper syntax. 

Let us take an example of  "Object : Expression"

#### Simple user defined JIT compiled expressions.

```python
f0 = Expression('sin(x[0]) + cos(x[1])')
f1 = Expression(('cos(x[0])', 'sin(x[1])'), element = V.ufl_element())
f2 = Expression((('exp(x[0])','sin(x[1])'),
                ('sin(x[0])','tan(x[1])')))
```

In the above code f0 is a scalar, f1 is a vector valued expression and f2 is a tensor valued expression. In this it is evident that first argument should be a tuple.  In general, a single string expression will be interpreted as a scalar, a tuple of strings as a tensor of rank 1 (a vector) and a tuple of tuples of strings as a tensor of rank 2 (a matrix).  The expressions may depend on x[0], x[1], and x[2] which carry information about the coordinates where the expression is evaluated. If you want to know more about the syntax of expression you can use 'help' command.

```python
help(Expression)
```

```python
Help on class Expression in module dolfin.function.expression:

class Expression(BaseExpression)
 |  JIT Expressions
 |  
 |  Method resolution order:
 |      Expression
 |      BaseExpression
 |      ufl.coefficient.Coefficient
 |      ufl.core.terminal.FormArgument
 |      ufl.core.terminal.Terminal
 |      ufl.core.expr.Expr
 |      builtins.object
 |  
 |  Methods defined here:
 |  
 |  __getattr__(self, name)
 |      Pass attributes through to (JIT compiled) Expression object
 |  
 |  __init__(self, cpp_code=None, *args, **kwargs)
 |      Initialize self.  See help(type(self)) for accurate signature.
 |  
 |  __setattr__(self, name, value)
 |      Implement setattr(self, name, value).
 |  
 |  ----------------------------------------------------------------------
......
```

To debug one should always read the error message properly and can take the help of the three commands given at the start of the post. 

