# ![Phyics based ray tracing in golang (go)](mascot.png) Physics Based Ray Tracing in Go


## Introduction

In this series of blog posts I explain the inner workings of [BruteRay](http://github.com/barnex/bruteray), a physics-based ray tracer written in Go.

BruteRay focuses on simplicity. I chose the name because initially I assumed that its simplicity would mean it had to be "brute force" and slow. However, the simple design eventually led to a surprisingly fast result. In fact, the speed seems to be in the same  ballpark as  tracers like [PovRay](http://www.povray.org/). The image below, for instance, was rendered on a laptop in just a few minutes.

![Damaliscus Korrigum skull ray traced in golang](damaliscus.jpg) 
*Damaliscus Korrigum skull (3D model with 300,000 faces, from [artec3d.com](http://www.artec3d.com)). Sand heightmap drawn in GIMP. Ray traced in Go.*

It did take several thousand lines of code before I was able to render that skull with photorealistic quality. But ray tracing is actually quite accessible. In fact, a simpler image like the one below can be achieved with just a few hundred lines of straightforward code.

![Spheres rendered with raytracing in golang go](by-the-campfire.jpg)
*Spheres like this can be ray traced with just a few hundred lines of code, but it does get trickier from there.*

In what follows I'll start from the basics needed to render some reflective spheres, and continue all the way to the techniques needed to render the Damaliscus Korrigum skull I showed earlier. 

Although I borrowed some naming from _PovRay_ and [pbrt](http://www.pbr-book.org/), the design presented here does *not* attempt translate these C++ implementations to Go. On the contrary, the design is very typical for Go: we use very simple interfaces (often with just a single method) and compose these building blocks into a more powerful whole, rather than construct a hierarchy of classes.

---

## Part 0: Geometric primitives
**2019-11-24**

Before we can start tracing rays, we need some basic building blocks like a 3-component vector [`Vec`](https://godoc.org/github.com/barnex/bruteray/geom#Vec) with some basic linear algebra methods. I use a `Vec` to store either a point in 3D space, or a displacement (vector).

We also need a floating-point [`Color`](https://godoc.org/github.com/barnex/bruteray/color#Color) implementation. 

See to the godoc for packages [geom](https://godoc.org/github.com/barnex/bruteray/geom) and [color](https://godoc.org/github.com/barnex/bruteray/color) if you want to see how I implemented them.

One thing to note is that for these small types, I chose to operate on values rather pointers, so that I didn't need to worry about mutability (or small allocations, for that matter).

Of course, we also need a [`Ray`](https://godoc.org/github.com/barnex/bruteray/tracer#Ray). A `Ray` is an infinitely long half-line with origin `Start` and direction `Dir` (a unit vector). Positions along the ray are denoted by `t`, with `t=0` being the starting point.

![Ray](ray.png)
*A ray has a starting point and direction (unit vector). Distances along the Ray are denoted by `t`. Points with negative `t` are not considered to lie on the ray*

It is important to note that a ray is just a half-line, not necessarily a beam of light. In ray tracing we often follow the light backwards. A ray starts from a pixel in the camera, travels out of the lens, bounces around the scene, and eventually ends at a light source. Thus light does not neccesarily travel in the direction of a ray -- it often travels oppositely. Fortunately, the laws of optics remain the same if we reverse the light's direction. So we generally don't need to worry about this. 

---

## Part 1: Ray tracing basics
**2019-11-25**

If you're completely new to ray tracing, you might want to familiarize yourself with the concept [here](https://en.wikipedia.org/wiki/Ray_tracing_(graphics)).


In a rather unusual approach to the subject, I define the ray tracing algorithm as:

```
Image = Camera(LightField)
```

which reads: *To calculate an Image, apply a Camera to a Light Field*.

In what follows, I shall explain what that means, and break down abstract concepts like `LightField` into simpler, more concrete building blocks like `Object` and `Material`.  These shall be broken down further until the entire algorithm has been explained.

In the end, the algorithm will be extended and expanded into something like:

```
Image = Sample(Camera(Shade(Frontmost(Intersect(Scene)))))
```

Where every step is a simple, well-defined computation mostly orthogonal to the others. Each step will be explained separately, starting with the light field.

### The Light Field

The Light Field of a scene is a function that gives us the light's brightness, seen from any given viewpoint and direction. The viewpoint and direction are, of course, represented by a `Ray`:

```go
func LightField(Ray) Color
```

I.e., if our eye was positioned at a ray's start and we looked along the ray's direction, then we would see the color returned by the light field.

![lightfield](lightfield.png)
*The light field of a scene encodes the color seen by any given ray.*

When a camera records an image, it captures a portion of the scene's light field and projects it onto a two-dimensional image. E.g., a 1-megapixel camera looks along 1 million rays, one per pixel, and captures the brightness of each of them.

![camera](camera.png)
*A camera records an image by capturing the brightness of one ray for every pixel.*

This breaks down the ray tracing algorithm in two smaller steps:
  1. finding rays corresponding to pixels (see [Cameras])
  2. calculating the light field of a ray (see [Calculating the Light Field])

---

## Part 2: Cameras


---

## Part 3: Calculating the Light Field