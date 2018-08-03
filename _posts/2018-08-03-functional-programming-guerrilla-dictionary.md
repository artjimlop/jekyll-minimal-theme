---
layout: post
title: "Functional Programming Guerrilla Dictionary"
description: "This Functional Programming Glossary of Terms is a support for my posts about Monads. It's useful as a quick reference guide of FP terms."
---

The main idea of this post is to support my next posts' explanations because I will be talking about Monads. I will be adding more terms if I find it necessary. The only purpose is being a quick terms guide for understanding next posts. Kotlin is the language used for the code snippets below. Please, notice *this is not an in-depth explanation of these concepts*.

### Glossary of Terms

**Currying:** is when you break down a function that takes multiple arguments into a series of functions that take part of the arguments.

~~~
val benchmark = fun(startInMilliseconds: Int): (Int) -> Int {
    return fun(endInMilliseconds: Int): Int {
        return endInMilliseconds - startInMilliseconds
    }
}

val timeLapse = benchmark(1000)
timeLapse(5000) // result: 4000
~~~

This is also an example of a [Closure](http://www.napalmdrivendevelopment.xyz/why-learn-functional-programming.html).

**Function Composition:** to combine simple functions to build more complicated ones.

~~~
fun main(args: Array<String>) {
    val oddLength = compose(::isOdd, ::length)
    val strings = listOf("a", "ab", "abc")
    println(strings.filter(oddLength))
}

fun isOdd(x: Int) = x % 2 != 0
fun length(s: String) = s.length

fun <A, B, C> compose(f: (B) -> C, g: (A) -> B): (A) -> C {
    return { x -> f(g(x)) }
}
~~~

Inside the compose function, you can find the concept of *mathematical composition*, because compose is *f(g(x))*.

**Functor:** is something that can be mapped over to obtain a set of new things. For that purpose, we use .map(f) method. An array is one popular functor.

~~~
arrayListOf(1,2,3).map { it*2 }
~~~

**Applicative Functor:** has more structure than a functor but less than a monad. This means, an applicative knows how to apply a function wrapped in a context to a value wrapped in a context.

For making easier to understand, let's define the *apply* function. This function knows how to deal with values wrapped in the same context.
~~~
infix fun <A, B> Option<(A) -> B>.apply(f: Option<A>): Option<B> =
        when (this) {
            is Option.None -> Option.None
            is Option.Some -> f.map(this.value)
        }
~~~

So now, we are able to do:

~~~
Some({ a: Int -> a + 3 }) apply Some(2)
// Result is Some(5)
~~~

**Monad:** is a design pattern that defines how functions, operations, inputs, and outputs can be used together to build generic types, with the following organization:

1. Define a data type, and how values of that data type are combined.

2. Create functions that use the data type, and compose them together into operations, following the rules defined in the first step.

Monads have the following properties:

* It has a context with a value.

* The value doesn’t have to exists.

* It provides a way to get the value (usually by callback)

* A bind function which able to pull the value out from the the monad (first argument) and put that value into another function f as argument. (f should be a function that return a monad). And the returned value of bind function should be the same type of the first argument.

* The bind function often also named flatMap

A list of all *sources* used for this post.

[What is a functor](https://medium.com/@dtinth/what-is-a-functor-dcf510b098b6)

[Applicative functor usage](https://wiki.haskell.org/Applicative_functor#Usage)

[Kotlin functor applicatives and applicatives](https://hackernoon.com/kotlin-functors-applicatives-and-monads-in-pictures-part-2-3-f99a09efd1ec)

[Composing functions in Kotlin](https://try.kotlinlang.org/#/Examples/Callable%20references/Composition%20of%20functions/Composition%20of%20functions.kt)

[What is a monad?](https://hackernoon.com/functional-computational-thinking-what-is-a-monad-2adea91154e)

~~~
title:   'Functional Programming Guerrilla Dictionary'
url:     'http://www.napalmdrivendevelopment.xyz/functional-programming-guerrilla-dictionary.html'
author:
  name:  '@artjimlop'
~~~
