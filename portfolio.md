---
layout: page
title: portfolio
permalink: /portfolio/
---

### Digestive
[Digestive](https://github.com/williamsjoblom/compiler-experiment) is my own programming language. Even though the JIT-compiler is far from completed it has some of the base functionality already in place. Features such as functions, basic control flow and composite data types are in a working state. One of the compilers main features is its ability to hotswap code at runtime. This means that one can magically make changes to the source code of a running program without having to restart it for the changes to have effect!

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

### Homebrew computer
A 6502-based homebrew computer with a simple unix-inspired multitasking OS with a shell and BASIC interpreter. 

Featuring a massive 32Kb of RAM (split up into 32 1K pages where each page is assigned to a process since the 6502 has no internal support for virtual memory), serial and parallel interfaces, PS/2 keyboard support, and an extension audio board capable of producing tunes from an AY-3-8910 sound generator. The operating system and drivers are all implemented in 6502-assembly. 

![](../assets/images/20150525_210636.jpg "Main board")
_Main board with the memory monitor running._

### Other projects
Hopefully something will show up here soon. In the meantime you can have a look at my [GitHub]({{ site.author.github }})!
