---
title: GSoC Final Report
tags: [Sympy, GSoC]
style: fill
color: success

description: Final report of GSoC with SymPy
---

This report summarizes the work done in my GSoC 2020 project, **Implementation of Vector Integration** with SymPy.  Blog posts with step by step development of the project are available at [friyaz.github.io](https://friyaz.github.io).

## About Me
I am Faisal Riyaz and I have completed my third year of B.Tech in Computer Engineering student from Aligarh Muslim University.

## Overview
The goal of the project is to add functions and class structure to support the integration of scalar and vector fields over curves, surfaces, and volumes. My mentors were [Francesco Bonazzi](https://github.com/Upabjojr) (Primary) and [Divyanshu Thakur](https://github.com/divyanshu132).

## Work Completed
Here is a list of PRs which were opened during the span of GSoC:
* (Merged) [#19472](https://github.com/sympy/sympy/pull/19472): Adds `ParametricRegion` class to represent parametrically defined regions.

* (Merged) [#19539](https://github.com/sympy/sympy/pull/19539): Adds `ParametricIntegral` class to represent integral of scalar or vector field over a parametrically defined region. 

* (Merged) [#19580](https://github.com/sympy/sympy/pull/19580): Modified API of `ParametricRegion`.

* (Merged) [#19650](https://github.com/sympy/sympy/pull/19650): Added support to integrate over objects of geometry module.

* (Merged) [#19681](https://github.com/sympy/sympy/pull/19681): Added `ImplicitRegion` class to represent implicitly defined regions.

* (Megred) [#19807](https://github.com/sympy/sympy/pull/19807): Implemented the algorithm for rational parametrization of conics.

* (Merged) [#20000](https://github.com/sympy/sympy/pull/20000): Added API of newly added classes to sympy's documentation.

* (Open) [#19883](https://github.com/sympy/sympy/pull/19883): Allow `vector_integrate` to handle `ImplicitRegion` objects.

* (Open) [#20021](https://github.com/sympy/sympy/pull/20021): Add usage examples.

We had an important discussion regarding our initial approach and possible problems on issue [#19320](https://github.com/sympy/sympy/issues/19320) 
### Defining Regions with their parametric equations
The `ParametricRegion` class is used to represent a parametric region in space. 
```python
>>> from sympy.vector import CoordSys3D, ParametricRegion, vector_integrate
>>> from sympy.abc import r, theta, phi, t, x, y, z
>>> from sympy import pi, sin, cos, Eq

>>> C = CoordSys3D('C')

>>> circle = ParametricRegion((4*cos(theta), 4*sin(theta)), (theta, 0, 2*pi))
>>> disc = ParametricRegion((r*cos(theta), r*sin(theta)), (r, 0, 4), (theta, 0, 2*pi))
>>> box = ParametricRegion((x, y, z), (x, 0, 1), (y, -1, 1), (z, 0, 2))
>>> cone = ParametricRegion((r*cos(theta), r*sin(theta), r), (theta, 0, 2*pi), (r, 0, 3))

>>> vector_integrate(1, circle)
8*pi
>>> vector_integrate(C.x*C.x - 8*C.y*C.x, disc)
64*pi
>>> vector_integrate(C.i + C.j, box)
(Integral(1, (x, 0, 1), (y, -1, 1), (z, 0, 2)))*C.i + (Integral(1, (x, 0, 1), (y, -1, 1), (z, 0, 2)))*C.j
>>> _.doit()
4*C.i + 4*C.j
>>> vector_integrate(C.x*C.i - C.z*C.j, cone)
-9*pi
```
### Integration over objects of `geometry` module
Many regions like circle are commonly encountered in problems of vector calculus. the geometry module of SymPy already had classes for some of these regions. The function`parametric_region_list` was added to determine the parametric representation of such classes. `vector_integrate` can directly integrate objects of Point, Curve, Ellipse, Segment and Polygon class of `geometry` module. 
```python 
>>> from sympy.geometry import Point, Segment, Polygon, Segment
>>> s = Segment(Point(4, -1, 9), Point(1, 5, 7))
>>> triangle = Polygon((0, 0), (1, 0), (1, 1))
>>> circle2 = Circle(Point(-2, 3), 6)
>>> vector_integrate(-6, s)
-42
>>> vector_integrate(C.x*C.y, circle2)
-72*pi
>>> vector_integrate(C.y*C.z*C.i + C.x*C.x*C.k, triangle)
-C.z/2
```
### Implictly defined Regions
In many cases, it is difficult to determine the parametric representation of a region. Instead, the region is defined using its implicit equation. To represent implicitly defined regions, we implemented the `ImplicitRegion` class.

But to integrate over a region, we need to determine its parametric representation. the `rationl_parametrization`  method was added to `ImplicitRegion`. 
```python
>>> from sympy.vector import ImplicitRegion
>>> circle3 = ImplicitRegion((x, y), (x-4)**2 + (y+3)**2 - 16)
>>> parabola = ImplicitRegion((x, y), (y - 1)**2 - 4*(x + 6))
>>> ellipse = ImplicitRegion((x, y), (x**2/4 + y**2/16 - 1))
>>> rect_hyperbola = ImplicitRegion((x, y), x*y - 1)
>>> sphere = ImplicitRegion((x, y, z), Eq(x**2 + y**2 + z**2, 2*x))

>>> circle3.rational_parametrization()
(8*t/(t**2 + 1) + 4, 8*t**2/(t**2 + 1) - 7)
>>> parabola.rational_parametrization()
(-6 + 4/t**2, 1 + 4/t)
>>> rect_hyperbola.rational_parametrization(t)
(-1 + (t + 1)/t, t)
>>> ellipse.rational_parametrization()
(t/(2*(t**2/16 + 1/4)), t**2/(2*(t**2/16 + 1/4)) - 4)
>>> sphere.rational_parametrization()
(2/(s**2 + t**2 + 1), 2*s/(s**2 + t**2 + 1), 2*t/(s**2 + t**2 + 1))
```

After PR [#19883](https://github.com/sympy/sympy/pull/19883) gets merged, `vector_integrate` can directly work upon `ImplicitRegion` objects.

## Future Work
* In vector calculus, many regions cannot be defined using a single implicit equation. Instead, inequality or a combination of the implicit equation and conditional equations is required. For Example, a disc can only be represented using an inequality `ImplicitRegion(x**2 + y**2 < 9)` and a semicircle can be represented as `ImplicitRegion(x**2 + y**2 -4) & (y < 0))`. Support for such implicit regions needs to be added.

* The parametrization obtained using the `rational_parametrization` method in most cases is a large expression. SymPy's `Integral` is unable to work over such expressions. It takes too long and often does not returns a result. We need to either simplify the parametric equations obtained or fix Integral to handle them.

* Adding the support to plot objects of `ParamRegion` and `ImplicitRegion`

## Conclusion
This summer has been a great learning experience. Writing a functionality, testing, debugging it has given me good experience in test-driven development. I think I realized many of the goals that I described in my proposal, though there were some major differences in the plan and actual implementation. Personally, I hoped I could have done better. I could not work much on the project during the last phase due to the start of the academic year.

I would like to thank [Francesco](https://github.com/Upabjojr) for his valuable suggestions and being readily available for discussions. He was always very friendly and helpful. I would love to work more with him. [S.Y Lee](https://github.com/sylee957) also provided useful suggestions.

Special thanks to [Johann Mitteramskogler](https://risc.jku.at/m/johann-mitteramskogler/), Professor [Sonia Perez Diaz](https://scholar.google.at/citations?user=IAz1bNgAAAAJ&hl=es), and Professor [Sonia L.Rueda](https://dblp.org/pid/87/7718.html). They personally helped me in finding the algorithm for determining the rational parametrization of conics.

SymPy is an amazing project with a great community. I would mostly stick around after the GSoC period as well and continue contributing to SymPy, hopefully, exploring the other modules as well.

{% include comments.html %}
