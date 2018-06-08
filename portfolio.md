---
layout: page
title: Projects
subtitle: or a few of the things that I've built and feel extra proud of!
permalink: /projects/
---

### Mapping robot <span class="year">2017</span> <span class="sub">or our omni-wheeled autonomous baby!</span> {#mapping-robot}
This project was done together with five fellow students at Linköping University for a course in construction with microcomputers during the fall of 2017.

![](../assets/images/kartrobot.jpg "Mapping robot")
*Our omni-wheeled creation.*

The main assignment was build a robot to map a maze-like course as fast as possible. The usual approach achieving this is by following a wall until you have explored the entire map. But this is far too simple right? Instead we used the more general SLAM-based approach using a LIDAR sensor, some clever algorithms and a ton of control theory; ultimately leading to a blowout in the mapping competition at the end of the semester.

During the project I was mainly responsible for design and construction of electronics along with embedded programming.

The project is open source and available on [GitHub](https://github.com/williamsjoblom/kmm).

<div class="divider"></div>

### Sonic Boom <span class="year">2017</span> <span class="sub">or a musical sequencer implemented on an FPGA!</span>

This was a project made for a course in micro processor design at Linköping University. The project goal was to implement a CPU in VHDL on a Xilinx FPGA and then program it to do something useful.

Since I already had a lot of experience using the 6502 CPU and the AY-3-8910 sound generator from the [homebrew computer project](#homebrew) the goal ended up being to implement a source code compatible 6502 processor in VHDL and interface it with said sound generator. This resulted in a music sequencer with 640x480 VGA output programmable via a hexadecimal keypad.

![](../assets/images/sonicboom.jpg "Sound generation board")
*Extension board housing the sound generator and associated components.*

The fact that the CPU was source code compatible with the 6502 meant that portions of the source code used in my homebrew computer could be reused. Of all vintage CPUs the 6502 has one of the larger still active communities, meaning that there are lots of resources available regarding the software bit, which also justified the choice of going with the 6502 compatible CPU.

The project ended with a fully functional sequencer and me buying an FPGA development board to implement a multi-core CPU with pipelining, caches and all that fancy stuff (a project that will show up here at some point).

The source code for the CPU, firmware and assembler is available on Github: [CPU and firmware](https://github.com/williamsjoblom/datorkonstruktion-projekt), [assembler](https://github.com/williamsjoblom/chasm).

<div class="divider"></div>

### Digestive <span class="year">2015&ndash;present</span> <span class="sub">or a work in progress language specification and JIT compiler!</span> {#digestive}
[Digestive](https://github.com/williamsjoblom/digestive-lang) is my own programming language. Even though the JIT-compiler is far from completed it has some of the base functionality already in place. Features such as functions, basic control flow and composite data types are in a working state. One of the compilers main features is its ability to hotswap code at runtime. This means that one can magically make changes to the source code of a running program without having to restart it for the changes to have effect!

_Here are a few code examples:_
{% highlight swift %}
fun swap(t : (i32, i32)) -> (i32, i32) {
     return (t.1, t.0);
}
{% endhighlight %}

{% highlight swift %}
fun fib(n : i32) -> i32 {
    if (n <= 1) return n;
    if (n == 2) return 1;
    return fib(n - 1) + fib(n - 2);
}

pln fib(10);
{% endhighlight %}

In its current state the compiler is pretty barebones and only contains generic features present in many other imperative languages. I have quite a few cool language feature ideas that will end up in a blog post at some point (and hopefully in the language itself).

<div class="divider"></div>

### Homebrew computer <span class="year">2013&ndash;2014</span> <span class="sub">or a 6502-based perfboard computer system!</span> {#homebrew}
A 6502-based homebrew computer with a simple unix-inspired multitasking OS with a shell and BASIC interpreter.

The computer resides on two separate perfboards. The main board which houses the core components such as CPU, memory, and some of the I/O while the extension board contains timers, sound generators and some additional I/O.

Sadly this project started before I was properly introduced to version control. As a result of this schematics and source code are nowhere to be found and most likely reside somewhere in my big pile of unused hard drives. When found schematics and source code will be made available on my GitHub.

![](../assets/images/20150525_210636.jpg "Main board")
_Main board with the memory monitor running._

**Specifications:**
* 2MHz clock frequency
* 32Kb of RAM
* 32Kb of ROM
* Virtual memory and multitasking

   Since the 6502 does not support virtual memory the RAM had to be split up into 32x1k pages to allow multitasking. A bunch of discrete logic chips are used to bind reserved addresses (the ones for the page swapping demultiplexer and some interrupt vectors) to the page used by the kernel to add process memory isolation.

* Programmable timers

   The computer has three programmable timers which can either be polled by software or configured to trigger interrupts individually.
   
* Double 8 bit parallell interface
* Serial interface
   
   With support for uploading data and programs using the YMODEM protocol.
* Audio output

   Audio output provided by the AY-3-8910 sound generator. Hardware for stereo output using two of these sound generators is present but software support is not yet implemented.

* PS/2 keyboard interface



<div class="divider"></div>

### Other projects
Hopefully more projects will show up here soon. In the meantime you can have a look at my [GitHub]({{ site.author.github }})!
