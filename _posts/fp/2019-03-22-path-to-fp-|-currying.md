---
layout: post
title: Path to FP - Currying
---

Currying is the process of decomposing a function of multiple arguments
into a chained sequence of functions of one argument each.

This simple device for replacing structured arguments by a sequence of simple ones
is known as 'currying', after the American logician H. B. Curry.For currying to work
properly in a consistent manner, we require that the operation of functional application
associates to the left.

That is, `f x y` means `(f x)y` and not `f(x y)`.

{% gist dcb1e67c1245776c136482d3c9d49c7e one.scala %}

We can create curried function as follow too:

{% gist dcb1e67c1245776c136482d3c9d49c7e two.scala %}