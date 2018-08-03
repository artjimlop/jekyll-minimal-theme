---
layout: post
title: "This is why you should learn a functional programming language"
description: 'Should you learn functional programming with Javascript, Kotlin, Swift or whatever your language of choice is? The answer is yes!'
---

Functional programming for Android, for iOS, in Kotlin, Swift or Javascript. Lambda expressions, monads, Erlang, Scala. Do these things ring a bell to you? You've probably listened or read them before. So, what's so cool about a paradigm born in the 1950's with the appearing of this language called *Lisp*?

### Functional Programming features

Before talking about the benefits of functional programming, I find necessary to mention some features these languages provide us. I would like to explain this features and also charge against the *"it's too complex and it has poor readability"* myth by writing examples both in Kotlin and [Elixir](http://www.napalmdrivendevelopment.xyz/what-is-elixir.html). I'm not going to say you're not going to struggle when learning this but, from my experience, the reason of that is simply because the change of paradigm, not because of any poor readability.

A **First-class function** is a function that can be stored in variables and data structures, passed as arguments to and returned from other higher-order functions

~~~
// Kotlin
val double = fun(x: Int): Int {
  return x * 2
}

# Elixir
double = fn(x) -> x * 2 end
~~~

A **Higher-Order function** is a function that takes functions as parameters, or returns a function.

~~~
// Kotlin
val benchmark = fun(startInMilliseconds: Int): (Int) -> Int {
    return fun(endInMilliseconds: Int): Int {
        return endInMilliseconds - startInMilliseconds
    }
}

val timeLapse = benchmark(1000)
timeLapse(5000) // result: 4000

# Elixir
benchmark = fn(start_milliseconds) ->
  fn(end_milliseconds) -> end_milliseconds - start_milliseconds
  end
end
~~~

A **Pure Function** should have the following qualities:

* It should depends only on the input to produce the result, not on any hidden information or external state.

* It shouldn’t cause any observable side effects, like modifying a parameter passed by reference or global variable/object.

~~~
// Kotlin
fun printValue(x: Int) {
  println(x)
}

# Elixir
def print_value(x), do: IO.inspect(x+1)
~~~

A **Closure** simply creates a scope that allows the function to access and manipulate the variables outside of its scope. Let's try to define it again: you can store some data inside a function that's only accessible to a specific returning function.

~~~
// Kotlin
val benchmark = fun(startInMilliseconds: Int): (Int) -> Int {
    return fun(endInMilliseconds: Int): Int {
        return endInMilliseconds - startInMilliseconds
    }
}

val timeLapse = benchmark(1000)
timeLapse(5000) // result: 4000

# Elixir
benchmark = fn(start_milliseconds) ->
  fn(end_milliseconds) -> end_milliseconds - start_milliseconds
  end
end
~~~

I will use the same example of High-Order Function again, the variable startInMilliseconds (or start_milliseconds) was enclosed and is only accessible to the returning function.

**Immutable State** means that you can't change any state at all.

~~~
// Kotlin
val person = Person("John Doe")
person.name = "Not John Doe" // Fails. Val cannot be reassigned.

# Elixir
map_set = MapSet.new
foo_set = MapSet.put(map_set, "foo")  

# map_set = MapSet<[]>
# foo_set = MapSet<["foo"]>
~~~

### Object-oriented Programming VS Functional Programming: fight!

High availability, concurrency, parallelism, predictability, distributed systems... have you ever listened this keywords ever? I'm pretty sure it's the case. Usually, when talking about **Functional Programming VS OOP** we have this tendency to just expose the dark side of Object-oriented Programming. So, let's try to keep more positive.

Previously, I've enounced a bunch of functional programming features. **Immutable state** may sound like a not particularly interesting feature, but plays a huge role in helping us developing our systems. Not relying on Object Oriented Programming's mutability concept helps give us **predictability**. Given some input, a function is going to return us the same output whether if it's running in one core or in a thousand cores. No process is messing around with no state. A lot of *complexity is drastically reduced* just because we don't have to worry about keeping threads correctly updated and synchronized.

Functional programming languages are typically *less efficient* in their use of CPU and memory than imperative languages. However, such slowdowns are not universal. Programs that perform intensive numerical computations written in a functional programming language *has been proven to be only slightly slower than C*. Also, **immutability** of data can in many cases lead to **execution efficiency** by allowing the compiler to make assumptions that are unsafe in an imperative language.

Learning a functional programming language mainly gives you *a new perspective*. Keep in mind that you can use these functional features explained before in other languages. This said, I would recommend to use a functional language on a future pet project or even apply these concepts to your production code if this is possible.

~~~
title:   'This is why you should learn a functional programming language'
url:     'http://www.napalmdrivendevelopment.xyz/why-learn-functional-programming.html'
author:
  name:  '@artjimlop'
~~~
