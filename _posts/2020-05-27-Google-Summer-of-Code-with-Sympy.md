---
title: Google Summer of Code with SymPy
tags: [Sympy, GSoC]
style: fill
color: success

description: My selection in GSoC 2020 and the community bonding period.
---

My proposal to SymPy has been selected for GSoC. My [project](https://summerofcode.withgoogle.com/organizations/4831132022996992/#6273573989122048) is to add the support of vector integration over Curves, Lines, and Surfaces to SymPy. My mentors are [Francesco Bonazzi](https://github.com/Upabjojr) and [DivyanshuThakur](https://github.com/divyanshu132). I am very excited to learn from them and contribute to SymPy.

Google Summer of Code or GSoC is a three-month program to bring student developers into open source development. Students contribute to an open project for three months. Students apply by submitting proposals to organizations. Students can submit up to 3 proposals. I only submitted one as most students do. 

When I started contributing to SymPy, I was new to Open-source. I looked through many projects. SymPy was a great fit for my skills and interests. The [Introduction to contributing](https://github.com/sympy/sympy/wiki/Introduction-to-contributing) and [development workflow](https://github.com/sympy/sympy/wiki/Development-workflow) pages are great and helpful. SymPy is well documented and the codebase is well maintained. I received continuous feedback from the community on my Pull Requests. SymPy is a great project to get started with the open-source if you are familiar with Python and comfortable with mathematics.

# SymPy
[SymPy](https://www.sympy.org/en/index.html) is a python library for symbolic mathematics. Symbolic computations are useful when we want to represent any mathematical quantity exactly. 

SymPy is free software and is licensed under New BSD license. 

Perhaps, the best way to get started with SymPy is to go through the SymPy [tutorial](https://docs.sympy.org/latest/tutorial/index.html). We can compute complicated math expressions, solve equations, perform integration, and do many more things. 

```python
>>> from sympy import *
>>>
>>> eq = 9*x - 2*x*y + y**2
>>> eq = eq - x
>>> eq
-2*x*y + 8*x + y**2
>>>
>>> eqdash = eq/x
>>> eqdash.expand()
-2*y + 8 + y**2/x
>>> factor(eqdash)
-(2*x*y - 8*x - y**2)/x
>>>
>>> diff(eq,x)
-2*y + 8
>>> Integral(eq,y)
Integral(-2*x*y + 8*x + y**2, y)
>>> Integral(eq,y).doit()
-x*y**2 + 8*x*y + y**3/3
>>>
>>> solve(sin(x)*x, x)
[0, pi]
```
# My project
SymPy has a vector module. It provides tools for basic vector maths. 

To get started with vectors, we first have to define a coordinate system. The module supports Cartesian, spherical, and curvilinear coordinate systems. 

```python
>>> from sympy.vector import CoordSys3D, divergence, gradient
>>> C = CoordSys3D('C')
``` 

We can access the unit vectors of the Coordinate System using C.i, C.j an C.k. C.x, C.y and C.z represent . Any vector expression can be created by performing basic mathematical operations like *,-,+ or / on base scalars and base vectors. We can also calculate gradient, curl and divergence.
```python
>>> v = 3*C.i + 5*C.j - 2*C.k
>>> s = 3*C.x*C.y
>>> vdash = C.i - 8*C.j + 11*C.k 
>>> v + vdash
4*C.i + (-3)*C.j + 9*C.k
>>> v.cross(vdash)
39*C.i + (-35)*C.j + (-29)*C.k
>>> gradient(s)
3*C.y*C.i + 3*C.x*C.j
```
SymPy does not support integration of vector/scalar fields over curves, surfaces and volume elements. But Vector instances can be integrated with respect to a single variable using Integral class.
```python
>>> from sympy import Integral
>>> Integral(v, C.x)
(Integral(3, C.x))*C.i + (Integral(5, C.x))*C.j + (Integral(-2, C.x))*C.k
>>> Integral(v, C.x).doit()
3*C.x*C.i + 5*C.x*C.j + (-2*C.x)*C.k
```

Vector calculus has many applications in the field of physics and mathematics, especially in the description of electromagnetic fields, gravitational fields, and fluid flow. The integrals of these fields represent important physical quantities. Vector Calculus plays a significant role in the study of partial differential equations. 

Let's look at some problems of such integrals. 
1. Integrate a scalar field f(x,y,z) = x<sup>2</sup>*y*z over the circle centered at x = 2 and radius r = 3.
2. Calculate the flux of the vector field **v** across the surface x<sup>2</sup> + y<sup>2</sup> + z<sup>2</sup> = 4 and z > 0. 
3. Calculate the mass of the body of Volume V bounded by x<sup>2</sup> + y<sup>2</sup> + z<sup>2</sup> = 1 and z<sup>2</sup> = (x<sup>2</sup> + y<sup>2</sup>)/2. The desnity is given as rho = z. 

To solve such integrals using Sympy, one first has to represent these integrals into multiple integrals and then use Integral class to get the result. Other Computer Algebra Systems like Mathematica and Maple already provides the functionality to perform such Integrals. 

# Community Bonding Period
Community Bonding Period is the first phase of the program. Students try to get familiar with the community and the codebase. I have contributed to SymPy in the past so I was comfortable with the development workflow. 

I submitted my proposal just before the deadline. Therefore, I could not discuss the proposal with the community. I wanted to use this period to discuss the API with the community and find any possible problem which can arise. I also wanted to get familiar with the vector module. SymPy, require that all student-mentor interactions happen on a public channel like a mailing list or Gitter. The Gitter room for discussion related to vectors is [sympy/vector](https://gitter.im/sympy/vector). If you have any ideas or suggestions or just want to check out the progress, do lurk around there. 

## The API
In my proposal, I suggested a possible API. But there were some obvious problems with that API which Francesco highlighted. The API must be easy to use and intuitive for SymPy users. It has to be close to the mathematical representation in textbooks. This reduces the difficulty of learning a new API and allows the user to focus. I have started an [issue](https://github.com/sympy/sympy/issues/19320) for discussing the API with the rest of the community. I also looked at other CAS to get inspiration. Mathematica seems to do a good job of calculating vector integrals. 

I proposed separate classes for different types of integrals(Line, Surface, Volume). Francesco suggested that the classes should represent the way an integral is displayed, not what kind of integral it is. SymPy should distinguish what these integrals are. Integral equations will be represented using subclasses of Integral. Then, we can write algorithms to perform computation.

We discussed about the separate classes to represent special surfaces. Many problems involve integrating over geometric objects like Circle, Sphere, Rectangle, Disk, etc. It can be helpful to the users if SymPy provides classes to represent such geometric entities. This saves the user from defining these objects using their parametric or implicit equation. We have decided to leave this part for later.

Another problem is determining the orientation of a surface. A surface can have two normals. The surface integral of scalar fields does not depend on the orientation. A surface integral of a vector field(flux) depends on the orientation. The result differs in sign. We decided that SymPy should always return the magnitude of the integral and it should be left to the user to decide the sign using the dot product.
      
## Defining regions using implicit equations
Many curves and surfaces are easy to describe using their implicit equations. As an example, a problem involves calculating integral over S where S is the portion of y = 3s*x<sup>2</sup> + 3*z<sup>2</sup> that lies behind y=6. It will be tiresome for the user to first get the parametric representation of this surface and then use SymPy to solve the integral. I believe that a major part of the problem is finding the parametric representation. The rest of the calculation can be easily performed.

But handling such integrals is a difficult problem. To calculate the integral, we generally need the parametric representation of the curve/surface. We can then reduce the integral to multiple integrals and use SymPy integral class to get the result. 

One approach to handle implicit equations is to write an algorithm to get the parametric representation from the implicit equation. This approach requires significant effort. We have decided to handle implicit integrals after we have completed the work on parametric integrals. 

## Conclusion
We have decided to first handle integrals over parametric regions. I will implement a class which will represent a parametric region in space. Another class will be implemented to represent an integral over a parametric region.

```python
>>> circle = ParametricCurve(r*cos(theta), r*sin(theta), (theta, 0, 2*pi), (r, 0, 1))
>>> ParametricIntegral(f(x, y), (x, y), circle)
``` 
 
We will handle implicit regions later. I plan to complete this work in the first phase hopefully and get started with implicit integrals from the next phase.
 
I wanted to start coding early but due to midsemester exams, I could not. Most probably, the end-semester exams will not be conducted this summer. They will get conducted along with next semester's exams. So, I do not have any other major commitments for the next 3 months.

{% include comments.html %}

