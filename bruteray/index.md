# ![Phyics based ray tracing in golang (go)](mascot.png) Physics Based Ray Tracing in Go


## Introduction

In this series of blog posts I explain the inner workings of [BruteRay](http://github.com/barnex/bruteray), a physics-based ray tracer written in Go.

First and foremost, BruteRay focuses on **simplicity**. I chose the name because I initially assumed that this would make it rather slow and "brute force".

However, that simple design (combined with Go's excellent profiling support and generally good performance) eventually led to a surprisingly fast implementation. In fact, the speed seems to be in the same  ballpark as  well-established tracers like _PovRay_.

The image below, for instance, was rendered on a laptop in only a few minutes.

![Damaliscus Korrigum skull ray traced in golang](damaliscus.jpg) 
*Damaliscus Korrigum skull (3D model with 300,000 faces) from [artec3d.com](http://www.artec3d.com). Sand heightmap drawn in GIMP. Rendered with BruteRay.*

It did take several thousand lines of code before I was able to render that skull with photorealistic quality. But ray tracing is actually quite accessible. A simpler image like the one below can be achieved with just a few hundred lines of code.

![Spheres rendered with raytracing in golang go](by-the-campfire.jpg)
*Spheres like this can be rendered with just a few hundred lines of code.*

In what follows I'll try to start from the basics needed to render the above spheres, and continue all the way to the techniques needed to render the Damaliscus Korrigum skull I showed earlier.

## Basics


In ray tracing we follow the light backwards. A ray starts from a pixel in the camera, travels out of the lens, bounces around the scene, and eventually ends at a light source. 

Thus when we speak of a ray, think of it as a _line of sight_. Fortunately, the laws of optics remain the same if we reverse the light's direction. So we generally don't need to worry about this.

Our process for finding a pixel's color consists of 3 steps

**1** The Camera constructs a Ray starting from a certain pixel position (u,v), pointing into the scene. 

```go
type Camera interface{
	RayFrom(u, v float64) *Ray
}
```

**2** We test for intersection between the ray and all objects in our scene. An Object is any type that knows how to find the its intersection with a ray:

```go
type Object interface{
	Intersect(r *Ray)HitRecord
}
```
If the ray actually intersects the object, then `Intersect` returns a non-zero `HitRecord`. The HitRecord stores information about the intersection point: its postion `T` along the ray, the object's surface normal at the intersection point, and the object's material:

```go
type HitRecord struct{
	T      float64
	Normal Vec
	Material Material
}
```

The `HitRecord` contains all the information we need to eventually find the pixel's color. But we only do this for the frontmost `HitRecord` (the one with the smallest positive `T` value). The other intersections points are occluded, and we don't want to waste time evaluation their color if we're only going to throw it away.

**3**
