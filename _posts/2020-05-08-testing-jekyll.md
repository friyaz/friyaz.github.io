---
title: Testing Jekyll
tags: [Test]
style: fill
color: success

description: A quick test of jekyll tools
---

## This is a first test of post using jekyll

Here is a lot of stuff



{% include elements/github-edit-footer.html %}
{% highlight python %}
   
class ParametricRegion()    :
    """
    A class to represent a parametric region in space. This class can 
    represent a curve, surface or volume.
    """
    def __init__(self, par, definition, bounds):
        """
        par : A tuple of length less than 2. The elements of the tuple represent the
        parameter in terms of which the general point on the region
        will be represented.
        definition : A tuple of length 3 expressing base scalars of the
        coord system in terms of parameter par.
        bounds : A tuple of length less than 2. The inner tuple elementsact as upper and lower bound of
        the respective parameter par.  
        """
        if len(par) > 2:
            raise ValueError("Number of parameters should not be more than 2")

        if len(definition) > 2:
            raise ValueError("Each base scalar must be represented in terms of parameters")
            
        if len(par) == 1:
            self.U = par[0]
        if len(par) == 2:
            self.U = par[0]
            self.V = par[1]
            
        self._definition = definition 
        self._bounds = bounds                               
        
    def u():
        return self.U
        
    def v():
        return self.V
        
    def getdefinition()
        return self._defintion
        
    def getbounds():
        return self._bounds
                                          
        
class Line(ParametricRegion):
    """
    A class to represent a line in space
    """
    def __init__(self, firstpoint, secondpoint):
        """
        firstpoint : Position vector of any endpoint of the line segment
        secondpoint : Position vector of any endpoint of the line segment
        """
        diff = secondpoint - firstpoint;
        t = Symbol('t')
        definition = (firstpoint.dot(i) + t* diff.dot(i),  
            firstpoint.dot(j) + t* diff.dot(j), firstpoint.dot(j) + t* diff.dot(j))
            
        param = (t)
        
        super(Line, self).__init__(param, definition, bounds)    

class Circle(ParametricRegion):
    """
    A class to represent a circle in space. The circle should lie in
    x-y plane, y-z plane or x-z plane completely.
    """
    def __init__(self, center, radius, axis):
        """
        center : Position vector of the center of circle
        radius : A number to represent radius of circle
        axis : A string. Should be equal to xy, yz or xz to 
            determine the orientation of circle.  
        """

        theta = Symbol('theta')
        param = (theta)
        
        if axis == "xy":
            definition = (radius * cos(theta), radius * sin(theta), 0)
        if axis == "yz"
            defintion = (0, radius * cos(theta), radius * sin(theta))
        if axis == "xz"
            defintion = (radius * cos(theta), 0, radius * sin(theta))
            
        bounds = ((0, 2 * pi))
        
        super(Circle, self).__init__(param, definition, bounds)   

class Arc(ParametricRegion):
    """
    A class to represent a arc in space. The arc should lie in
    x-y plane, y-z plane or x-z plane completely.
    """
    def __init__(self, paramobject, start, end):
        """
        paramobject : A paramregion object which should be Circle or Ellipse.
        start : Starting angle of sector in terms of radian
        end : Ending angle of sector in terms of radian
        """ 
        theta = Symbol("theta")
        r = Symbol("radius")
        param = (theta, r)
        
        if axis == "xy":
            definition = (r * cos(theta), r * sin(theta), 0)
        if axis == "yz"
            defintion = (0, r * cos(theta), r * sin(theta))
        if axis == "xz"
            defintion = (r * cos(theta), 0, r * sin(theta))
            
        bounds = ((start, end))
        
        super(Arc, self).__init__(bounds, definition, bounds)

                        
class Sector(ParametricRegion):
    """
    A class to represent a sector in space. The sector should lie in
    x-y plane, y-z plane or x-z plane completely.
    """
    def __init__(self, paramobject, start, end):
        """
        paramobject : A paramregion object which should be Circle or Ellipse.
        start : Starting angle of sector in terms of radian
        end : Ending angle of sector in terms of radian
        """ 
        theta = Symbol("theta")
        r = Symbol("radius")
        param = (theta, r)
        
        if axis == "xy":
            definition = (r * cos(theta), r * sin(theta), 0)
        if axis == "yz"
            defintion = (0, r * cos(theta), r * sin(theta))
        if axis == "xz"
            defintion = (r * cos(theta), 0, r * sin(theta))
            
        bounds = ((start, end), (0, radius) )
        
        super(Sector, self).__init__(bounds, definition, bounds)                       
    
class Rectangle(ParametricRegion):
    """
    A class to represent a rectangle in space.
    """
    def __init__(self, points):
        """
        points: A tuple of length 2 each tuple. Each internal tuple has 2 elements 
        which the postion vector of corner of rectangle.
        """
     
    
class Traingle(ParametricRegion):
    """
    A class to represent a triangle in space.
    """
    def __init__(self, points):
        """
        points: A tuple of length 3. Each element of tuple represent
        the postion vector of vertex of the triangle.
        """
                 
class Disc(ParametricRegion):
    """
    A class to represent a disc in space. The disc should lie in
    x-y plane, y-z plane or x-z plane completely.
    """
    def __init__(self, center, radius, axis):
        """
        center : Position vector of the center of circle
        radius : A number to represent radius of circle
        axis : A string. Should be equal to xy, yz or xz to 
            determine the orientation of circle.  
        """
        theta = Symbol("theta")
        r = Symbol("radius")
        param = (theta, r)
        
        if axis == "xy":
            definition = (r * cos(theta), r * sin(theta), 0)
        if axis == "yz"
            defintion = (0, r * cos(theta), r * sin(theta))
        if axis == "xz"
            defintion = (r * cos(theta), 0, r * sin(theta))
            
        bounds = ((0, 2 * pi), (0, radius) )
        
        super(Disc, self).__init__(bounds, definition, bounds) 
        
            
class Ball(ParametricRegion):
    """
    A class to represent a solid sphere in space.
    """
    def __init__(self, center, radius):
        """
        center : Position vector of the center of circle
        radius : A number to represent radius of circle
        """

class Sphere(ParametricRegion):
    """
    A class to represent a sphere in space.
    """
    def __init__(self, center, radius):
        """
        center : Position vector of the center of circle
        radius : A number to represent radius of circle
        """
        
class Ellipse(ParametricRegion):
    """
    A class to represent a sphere in space.
    """
    def __init__(self, center, a, b):
        """
        center : Position vector of the center of circle
        a : A number to represent radius of circle
        b : A number to represent radius of circle        
        axis: A string. Should be equal to xy, yz or xz to 
            determine the orientation of circle.  
        """          
    
class Box(ParametricRegion):
    """
    A class to represent rectangular cuboid.
    """
    def __init__(self, sides):
        """
        A tuple consisting of 12 internal tuples.
        Each internal tuple is of length 2 represnting the sides
        of box.
        """                 

class Tetrahedron(ParametricRegion):
    """
    A class to represent a terahedron in space
    """
    def __init__(self, points):
        """
        points: A tuple of length 4. Each element of tuple represent
        the postion vector of a vertex of Polygon. 
        """      
class VectorIntegral(object):
    """
    A class which will act as Base class for LineIntegral, 
    SurfaceIntegral and Volume Integral Class
    """
    def __init__(self, field, region):
        self.field = field
        self.region = region
    
        
class LineIntegral(VectorIntegral):
    """
    A class to represent line integral of scalar or vector field
    over a curve.
    """
    def __init__(self, field, region):
         super(LineIntegral, self).__init__(field, region)
         
    def eval(self):
    ### Pseudo Code
        d = self.field.gedefinition()
        
        for i in range(2):
                ddiff[i] = diff(d[i], self.field.u())
       
        Form the rdiff vector using ddiff and base vectors of coordinate system         
        express field in terms of self.field.u() using definition d
        let exp be the result
        Perform the dot product if vector field or multiply if scalar field
        bounds = self.field.getbounds()
         
        result = integrate(exp, self.region.u(), bounds[0][0], bounds[0][1])
        
        return res
        

class SurfaceIntegral(VectorIntegral):
    """
    A class to represent Surface integral of scalar or vector field
    over a curve.
    """
    def __init__(self, field, region):
         super(LineIntegral, self).__init__(field, region)
         
    def eval(self):
    ### Pseudo Code
        d = self.field.gedefinition()
        
        for i in range(3):
                ddiff_u[i] = diff(d[i], self.field.u())

        for i in range(3):
                ddiff_v[i] = diff(d[i], self.field.v())                
       
        Form the vector rdash_u and rdash_v using ddiff_u and ddiff_v 
        by multiplying with base scalars 
        
        n = rdash_u.cross(rdash_v)
        express field in terms of self.field.u() and self.field.v() 
        using definition d
        let exp be the result
        
        Perform the dot product if vector field or multiply if scalar field
        let v be the result
        bounds = self.field.getbounds()
         
        Determine the order of integration
        
        result = integrate(v, (self.region.u(), (bounds[0][0], bounds[0][1]))
                              (self.region.v(), (bounds[1][0], bounds[1][1])))
        OR
        result = integrate(v, (self.region.v(), (bounds[1][0], bounds[1][1]))
                              (self.region.u(), (bounds[0][0], bounds[0][1])))                              
        
        return res 
        
class VectorIntegral(VectorIntegral):
    """
    A class which will act as Base class for LineIntegral,
    SurfaceIntegral and Volume Integral Class
    """
    def __init__(self, field, region):
         super(LineIntegral, self).__init__(field, region)
         
    def determine_order():
    """
    A function to determine the order of integration     
    ""      
    
    def eval(self):
    ### Pseudo Code
        d = self.field.gedefinition()
        
        for i in range(3):
                ddiff_u[i] = diff(d[i], self.field.u())

        for i in range(3):
                ddiff_v[i] = diff(d[i], self.field.v())                
       
        Form the vector rdash_u and rdash_v using ddiff_u and ddiff_v 
        by multiplying with base scalars 
        
        n = rdash_u.cross(rdash_v)
        express field in terms of self.field.u() and self.field.v() 
        using definition d
        let exp be the result
        
        Perform the dot product if vector field or multiply if scalar field
        let v be the result
        bounds = self.field.getbounds()
         
        Determine the order of integration
        
        result = integrate(v, (self.region.u(), (bounds[0][0], bounds[0][1]))
                              (self.region.v(), (bounds[1][0], bounds[1][1])))
        OR
        result = integrate(v, (self.region.v(), (bounds[1][0], bounds[1][1]))
                              (self.region.u(), (bounds[0][0], bounds[0][1])))                              
        
        return res                                          
}
{% endhighlight %}
    {% include comments.html %}

