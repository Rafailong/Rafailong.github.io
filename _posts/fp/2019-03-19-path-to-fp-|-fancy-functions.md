---
layout: post
title: Path to FP - Fancy functions
---

We already know FP is about programming just with functions, pure and descriptive functions.

There are some really fancy kind of functions out there:

## HOF (High Order Function)

Yep, a HOF is one that can take in as parameter or spit out as its result a function, and guess what,
if for some weird reason you've been doing some JavaScript there's a super high probability that you already used HOF.

```javascript
function add1(x) { return x + 1; }
var number = [1, 2, 3, 4, 5].map(add1);
```

Where `map` is a HOF. Now let's see the same example in Scala:

```scala
val numbers = (0 to 10).toList

numbers.map(x => x * x)

println(numbers)
```

Let's get some diabetes by syntactic sugar 🤣

```scala
numbers.map(_ + 1)
```

When doing Scala code and working with HOF is super normal to pass around anonymous functions
(as we did in `number.map` example) rather than declaring a val or a `def`.

## Partial Functions

A partial function is a function that will only work for a given set of its domain.
A function that will not produce a value for every possible input value it can be given.
We can use this type of function whenever we have functions with a ton of guard code (a bunch if and else testing the inputs).
A simple example is when dividing by zero.

```scala
def divide(x: Int, y: Int) = x / y

// dividing(1, 0) will throw
// we can use partial function for testing valid y values

val devidePF: PartialFunction[(Int, Int), Int] = {
  case (x, y) if y > 0 => x / y
}
println("8/2 equals " + devidePF(8, 2))
// println("8/2 equals " + devidePF(2, 0)) this will throw, the value of y is not valid
```
