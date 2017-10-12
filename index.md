# Arne Vansteenkiste's github projects

This page contains a few picks from my repos at [github.com/barnex](http://github.com/barnex)


## mumax3

[mumax3](http://mumax.github.io) is a GPU-accelerated micromagnetic simulator with ~1000 active users worldwide. It is [cited](http://aip.scitation.org/doi/10.1063/1.4899186) in 400 scientific publications.

![fig](http://mumax.github.io/web1.png)

[Read more...](http://mumax.github.io) 


## bruteray

[bruteray](http://github.com/barnex/bruteray) is a hobby ray tracer employing physically accurate light transport to generate realistic images.

![fig](https://raw.githubusercontent.com/barnex/bruteray/master/shots/039.jpg)

[Read more...](http://github.com/barnex/bruteray) 


## coffee-cpu

After drinking too much coffee, [@MathiasHelsen](https://github.com/mathiashelsen) and I built a softcore CPU on FPGA. The coffee-cpu has a 14-bit memory space. It has an assembler and can solve a few challenges from projecteuler.net.


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

[Read more...](http://github.com/barnex/coffee-cpu)


## just-in-time-compiler

[This](https://github.com/barnex/just-in-time-compiler) is a just-in-time compiler for mathematical expressions like `x + sqrt(y - 1)`. It does constant-folding and registerization. The resulting x86 binary machine code can be immediately executed for, e.g., super-fast function plotting.

![fig](https://raw.githubusercontent.com/barnex/just-in-time-compiler/master/plotter.png)

[Read more...](https://github.com/barnex/just-in-time-compiler) i

## ev3cam

[ev3cam](http://github.com/barnex/ev3cam) detects motion in a webcam stream (using gstreamer), so that a LEGO mindstorms knows where to aim.

![fig](https://raw.githubusercontent.com/barnex/ev3cam/master/motion.gif)

[Read more...](http://github.com/barnex/ev3cam) 


## Game of life


[This](https://github.com/barnex/life) is an insanely optimized implementation of Conway's Game of Life (a Turing-complete "board game"). With extreme bit-fiddling, it achieves a ~300x speed-up over a naive implementation.

![fig](https://raw.githubusercontent.com/barnex/life/master/img.png)

[Read more...](https://github.com/barnex/life) 

## SetupSoftware

Not-so-aptly-named software to control the Magneto-Optical Scanning Microscope at Dynamat lab, UGent.

![fig](https://raw.githubusercontent.com/barnex/SetupSoftware/master/Moka/screenshot.png)

[Read more...](https://github.com/barnex/SetupSoftware)


## Bare-metal raspberry pi

Bare-metal kernel image for raspberry Pi. It writes PI on the display. Inspired by [baking pi](http://www.cl.cam.ac.uk/projects/raspberrypi/tutorials/os/) but written mostly in C.

![fig](https://raw.githubusercontent.com/barnex/bakingcpi/master/pi.JPG)

[Read more...](http://github.com/barnex/bakingcpi): 


## arnecompiler

[This](https://github.com/barnex/arnecompiler) is a compiler I wrote a really long time ago. It can solve the first few problems of projecteuler.net.

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
[Read more...](https://github.com/barnex/arnecompiler) 
