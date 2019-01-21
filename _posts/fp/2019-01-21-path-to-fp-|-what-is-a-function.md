---
layout: post
title: Path to FP - What is a function?
---

- A function is a computation that takes in a `A` as argument and returns a `B` as result.
- From category theory, a function is represented as a morphism (arrow).

There are several ways to define functions in Scala.

```scala
/**
 * In Scala we can define functions using `def` keyword
 * We are defining a funciton to add 2 integer numbers.
 */
def add(a: Int, b: Int): Int = a + b
println("Adding 2 and 3 equals ${addPrime(2, 3)}")

 /**
  * Now we define a function that takes in a A (Int)
  * and returns a B (String)
  */
def toString(n: Int): String = s"$n"
println(toString(10))

// But also we can do
val addPrime: (Int, Int) => Int = (a, b) => a + b
println("Adding 5 and 8 equals ${addPrime(5, 8)}")
```

But in Scala we have types, right? So, We also can do as follow:

```scala
val addPrime2: Function2[Int, Int, Int] = new Function2[Int, Int, Int] {
    def apply(a: Int, b: Int): Int = a + b
}

// Check how many Function types we do have.
println("Adding 10 plus 5 equals " + addPrime2(10, 5))
```

 But, is the same thing a method and  a function? 🤔
 Well, you right! No, they are not the same. A method is part of a class and a function is a complete object with some super powers
 that we will check in the next post.

 Have fun!