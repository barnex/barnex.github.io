# Arne Vansteenkiste's github projects

This page contains a few picks from my repos at [github.com/barnex](https://github.com/barnex)


## mumax3

[mumax3](https://mumax.github.io) is a GPU-accelerated micromagnetic simulator with ~1000 active users worldwide. It is [cited](http://aip.scitation.org/doi/10.1063/1.4899186) in 400 scientific publications.

[Read more...](https://mumax.github.io) 

![fig](https://mumax.github.io/web1.png)



## bruteray

[bruteray](https://github.com/barnex/bruteray) is a hobby ray tracer employing physically accurate light transport to generate realistic images.

[Read more...](https://github.com/barnex/bruteray) 

![fig](https://raw.githubusercontent.com/barnex/bruteray/master/shots/063.jpg)



## coffee-cpu

After drinking too much coffee, [@MathiasHelsen](https://github.com/mathiashelsen) and I built a softcore CPU on FPGA. The coffee-cpu has a 14-bit memory space. It has an assembler and can solve a few challenges from projecteuler.net.

[Read more...](https://github.com/barnex/coffee-cpu)


```
// This test program cycles the hex display
// through all 16-bit values

#def display 0x3FFF
#def Rcount R1

#label _start
XOR   R0     R0       A R0     -cmp
STORE Rcount display  N R0     -cmp
ADD   Rcount 1        A Rcount -cmp
ADD   R0     _start   A PC     -cmp
```



## just-in-time-compiler

[This](https://github.com/barnex/just-in-time-compiler) is a just-in-time compiler for mathematical expressions like `x + sqrt(y - 1)`. It does constant-folding and registerization. The resulting x86 binary machine code can be immediately executed for, e.g., super-fast function plotting.

[Read more...](https://github.com/barnex/just-in-time-compiler)

![fig](https://raw.githubusercontent.com/barnex/just-in-time-compiler/master/plotter.png)


## ev3cam

[ev3cam](https://github.com/barnex/ev3cam) detects motion in a webcam stream (using gstreamer), so that a LEGO mindstorms knows where to aim.

[Read more...](https://github.com/barnex/ev3cam) 

![fig](https://raw.githubusercontent.com/barnex/ev3cam/master/motion.gif)



## Game of life


[This](https://github.com/barnex/life) is an insanely optimized implementation of Conway's Game of Life (a Turing-complete "board game"). With extreme bit-fiddling, it achieves a ~300x speed-up over a naive implementation.

[Read more...](https://github.com/barnex/life) 

![fig](https://raw.githubusercontent.com/barnex/life/master/img.png)


## SetupSoftware

Not-so-aptly-named software to control the Magneto-Optical Scanning Microscope at Dynamat lab, UGent.

[Read more...](https://github.com/barnex/SetupSoftware)

![fig](https://raw.githubusercontent.com/barnex/SetupSoftware/master/Moka/screenshot.png)


## Raspberry heat

Home temperature control with Raspberry Pi and a web interface.

[Read more...](https://github.com/barnex/raspberryheat)

![fig](https://raw.githubusercontent.com/barnex/raspberryheat/master/rh2.png)



## Bare-metal raspberry pi

Bare-metal kernel image for raspberry Pi. It writes PI on the display. Inspired by [baking pi](http://www.cl.cam.ac.uk/projects/raspberrypi/tutorials/os/) but written mostly in C.

[Read more...](https://github.com/barnex/bakingcpi)

![fig](https://raw.githubusercontent.com/barnex/bakingcpi/master/pi.JPG)


## Go bindings for CUDA

Go bindings for CUDA, my most starred project. 

[Read more...](https://github.com/barnex/cuda5)

![fig](https://raw.githubusercontent.com/barnex/cuda5/master/gophergpu.png)


## arnecompiler

[This](https://github.com/barnex/arnecompiler) is a hobby compiler I wrote a really long time ago (2010). It can solve the first few problems of projecteuler.net.

[Read more...](https://github.com/barnex/arnecompiler) 

Language example:

```
include(int)

variable(int answer, 0)

for(variable(int i, 0), _lessl(i, 995), _incl(i), block(
  variable(int product, 1)
  for(variable(int j, 0), _lessl(j, 5), _incl(j), block(
    product(_mull(product, get_array(_addl(i, j))))
  ))
  if(_greaterl(product, answer)
    answer(product)
  )
))

print_int(answer)
```

## amumag

[amumag](https://github.com/barnex/amumag) is the Finite-Element micromagnetic simulator I wrote for my PhD thesis.

[Read more...](https://github.com/barnex/amumag)

![fig](https://raw.githubusercontent.com/barnex/amumag/master/amuview.png)

## Chaos

This is a very old (2006) project I made for a course on dynamical systems.

[Read more...](https://github.com/barnex/Chaos)

![fig](https://raw.githubusercontent.com/barnex/Chaos/master/shots/julia3.png)

## Engine3D

This is is a very old (2005-ish) project where I wrote a 3D engine using Java 2D API.

[Read more...](https://github.com/barnex/Engine3D)

![fig](https://raw.githubusercontent.com/barnex/Engine3D/master/Screenshots/light1.png)
