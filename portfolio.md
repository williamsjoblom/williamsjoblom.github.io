---
layout: page
title: portfolio
permalink: /portfolio/
---

### Digestive
[Digestive](https://github.com/williamsjoblom/compiler-experiment) is my own programming language. Even though the JIT-compiler is far from completed it has some of the base functionality already in place. Features such as functions, basic control flow and composite data types are in a working state. One of the compilers main features is its ability to hotswap code at runtime. This means that one can magically make changes to the source code of a running program without having to restart it for the changes to have effect!

_Here are a few code examples:_
{% highlight swift %}
func swap(t : (i32, i32)) -> (i32, i32) {
     return (t.1, t.0);
}
{% endhighlight %}

{% highlight swift %}
func fib(n : i32) -> i32 {
    if (n <= 1) return n;
    if (n == 2) return 1;
    return fib(n - 1) + fib(n - 2);
}

pln fib(10);
{% endhighlight %}

In its current state the compiler is pretty barebones and only contains pretty generic features present in many other imperative languages. I have quite a few cool language feature ideas that will will end up in a blog post at some point (and hopefully in the language itself).

In its current state the compiler is missing a proper test suite, has a few memory leaks and segfaults once in a while. Reliability and robustness are currently at highest priority for future development.

### Other projects
Hopefully something will show up here soon. In the meantime you can have a look at my [GitHub]({{ site.author.github }})!
