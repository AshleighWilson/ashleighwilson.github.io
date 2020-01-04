---
layout: post
title:  "Welcome to my blog!"
date:   2020-01-01
categories: General
tags: [ ]
mathjax: true
---

This post is a starting point for my blog and serves as a demonstration of some of the functionality available.

## Code Snippets

An example of a C++ code snippet below.

```cpp
#include <iostream>

using namespace std;

int main() 
{
    cout << "Hello, World!";
    return 0;
}
```

## MathJax Integration

MathJax allows math equations to be added to the website. 


Inline equations are possible by using `$ ... $`, i.e. $$ax^2 + bx + c = 0$$. Equations on separate lines can be created using `$$ ... $$`.

$$x = {-b \pm \sqrt{b^2-4ac} \over 2a}$$

It is possible to omit the equation number if needed by using `\nonumber`.

$$ \int_0^\infty \frac{x^3}{e^x-1}\,dx = \frac{\pi^4}{15} \nonumber $$

We can also label equations with `\label{...}` and then reference them with `\eqref{...}`. For example, equation \eqref{Einstein}.

$$ E=mc^2 \label{Einstein} $$

And we can align multiple equations with `\begin{align} ... \end{align}`.

$$
    \begin{align}
        \sqrt{37} & = \sqrt{\frac{73^2-1}{12^2}} \nonumber \\[3ex]
        & = \sqrt{\frac{73^2}{12^2}\cdot\frac{73^2-1}{73^2}} \nonumber \\[3ex]
        & = \sqrt{\frac{73^2}{12^2}}\sqrt{\frac{73^2-1}{73^2}} \nonumber \\[3ex]
        & = \frac{73}{12}\sqrt{1 - \frac{1}{73^2}} \nonumber \\[3ex]
        & \approx \frac{73}{12}\left(1 - \frac{1}{2\cdot73^2}\right)
    \end{align}
$$

## References

1. [Creating and Hosting a Personal Site on GitHub](http://jmcglone.com/guides/github-pages/){:target="_blank"}
2. [MathJax Basic Tutorial and Quick Reference](https://math.meta.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference){:target="_blank"}