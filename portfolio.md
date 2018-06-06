---
layout: page
title: Projects
permalink: /projects/
---

### Mapping robot <span>2017</span>
This project was done together with five fellow students at Linköping University for a course in construction with microcomputers during the fall of 2017.

![](../assets/images/kartrobot.jpg "Mapping robot") 

The main assignment was build a robot to map a maze-like course as fast as possible. The usual approach achieving this is by following a wall until you have explored the entire map. But this is far too simple right? Instead we used the more general SLAM-based approach using a LIDAR sensor, some clever algorithms and a ton of control theory; ultimately leading to a blowout in the mapping competition at the end of the semster.

During the project I was mainly involved in design and construction of electronics along with micro controller programming.

The project is open source and available on [GitHub](https://github.com/williamsjoblom/kmm).

<div class="divider"></div>

### Digestive <span>2015-present</span>
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

### Homebrew computer <span>2013-2014</span>
A 6502-based homebrew computer with a simple unix-inspired multitasking OS with a shell and BASIC interpreter. 

**Specifications:**
* 2MHz clock frequency
* 32Kb of RAM
* Virtual memory and multitasking

   Since the 6502 does not support virtual memory the RAM had to be split up into 32x1k pages to allow multitasking. A bunch of discrete logic chips are used to bind reserved addresses (the ones for the page swapping demux and some interrupt vectors) to the page used by the kernel to add process memory isolation.

* Programmable timers

   The computer has three programmable timers. Of these the first one is reserved to provide interrupts for context switching while the other two are available for the user.
   
* Double 8 bit parallell interface
* Serial interface
   
   With support for uploading data and programs using the YMODEM protocol.
* Audio output

   Audio output provided by the AY-3-8910 sound generator. Hardware for stereo output using two of these sound generators is present but software support is not yet implemented.

![](../assets/images/20150525_210636.jpg "Main board")
_Main board with the memory monitor running._

<div class="divider"></div>

### Other projects
Hopefully more projects will show up here soon. In the meantime you can have a look at my [GitHub]({{ site.author.github }})!
