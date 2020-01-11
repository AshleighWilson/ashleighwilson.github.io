---
layout: post
title:  "Welcome to my blog!"
date:   2020-01-01
categories: General
tags: [ ]
mathjax: true
---

This post is a starting point for my blog and serves as a demonstration of some of the functionality available. Examples include adding code snippets and math equations into posts.

## Code Snippets

An example of a C++ code snippet below.

{% highlight cpp %}
#include <iostream>

using namespace std;

int main() 
{
    cout << "Hello, World!";
    return 0;
}
{% endhighlight %}

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

## Tikz Integration

To create diagrams for this website I decided to use Tikz, as I like the quality and simplicity of the diagrams produced. The Tikz diagrams are generated offline and then converted to SVG (Scalable Vector Graphics) format, which can be included into the document like any other image. As an example, take the following code:

{% highlight latex %}
\documentclass{minimal}
\usepackage[RPvoltages]{circuitikz}
\thispagestyle{empty}

\newcommand\bjtname[1]{($(#1.C)!0.5!(#1.E)$) node[anchor=west]{} }

\begin{document}
    \begin{circuitikz}[american, cute inductors]
        \node [op amp](A1){\texttt{OA1}};
        \draw (A1.-) to[short] ++(0,1) coordinate(tmp) to[R, l_=$R$] (tmp -| A1.out) to[short] (A1.out);
        \draw (tmp) to[short] ++(0,1) coordinate(tmp) to[C=$C$] (tmp -| A1.out) to[short] (A1.out);
        \draw (A1.+) to [battery2, invert] ++(0,-2.5) node[ground](GND){};
        \draw (A1.-) to [L=$L$] ++(-2,0) coordinate(tmp) to[sV, l=$v_s$, fill=yellow] (tmp |-GND) node[ground]{};
        \draw (A1.out) to[R=$R_s$] ++(2,0) coordinate(bb) to[I, l_=$I_B$, invert] ++(0,2) node[vcc](VCC){};
        \draw (bb) to[D, l=$D$, *-] ++(0,-2) coordinate(bb1) to[R=$R_m$] ++(0,-2) node[vee](VEE){};
        \draw (bb) --++(1,0) node[npn, anchor=B](Q1){} \bjtname{Q1};
        \draw (bb1) --++(1,0) node[pnp, anchor=B](Q2){} \bjtname{Q2};
        \draw (Q1.E) -- (Q2.E) ($(Q1.E)!0.5!(Q2.E)$) to [short, *-o, name=S] ++(2.5,0)
        node[right]{$v_{o_Q}$};
        \draw (S.s) to[european resistor, l=$Z_L$, *-] (S.s|-GND) node[ground]{};
    \end{circuitikz}
\end{document}
{% endhighlight %}

Compiling this Latex code produces a PDF document of the diagram. We can use Inkscape to convert this to SVG by invoking it with `inkscape -zlD file.pdf`.

![Tikz Example SVG](/tikz/tikz-example.svg)

## References

1. [Creating and Hosting a Personal Site on GitHub](http://jmcglone.com/guides/github-pages/){:target="_blank"}
2. [MathJax Basic Tutorial and Quick Reference](https://math.meta.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference){:target="_blank"}