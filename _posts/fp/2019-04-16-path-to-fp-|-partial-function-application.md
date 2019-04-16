---
layout: post
title: Path to FP - Partial function application.
---

Partial function application is creating functions from other function setting “default”
parameters to our base function.

What this means is that, when applying the function, you do not pass in arguments for
all of the parameters defined by the function, but only for some of them, leaving the remaining ones blank.

{% gist 267713ef0145acb1c248aab9a9dc29bd one.scala %}

Then we partially apply `add` to get a brand new function:

{% gist 267713ef0145acb1c248aab9a9dc29bd two.scala %}

Also, we can do as follow:

{% gist 267713ef0145acb1c248aab9a9dc29bd three.scala %}

But if we know that our brand new function will be partially applied we can define multiple argument lists!

{% gist 267713ef0145acb1c248aab9a9dc29bd four.scala %}

What if there's a function that's already defined but we want to partially apply it?
Well, first we get our function, then we curry it and finally we can partially apply it!
Let's see:

{% gist 267713ef0145acb1c248aab9a9dc29bd five.scala %}

Finally, understanding this concept is really important because one application of it is: dependency injection.