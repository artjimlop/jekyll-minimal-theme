---
layout: post
title: "What the hell is Elixir?"
---

This is a question that usually comes around whenever I'm talking about Elixir at the office so, In order to help myself and others to answer this question, I have decided to create  a post about that!

First of all, because Elixir is built on top of Erlang and depends heavily on it, let's make a brief introduction to the language:

Erlang is a development platform for building scalable and reliable systems that constantly provide service with little or no downtime conceived in the mid-1980s by Ericsson. It powers various large systems and has been doing so for more than two decades, such as the WhatsApp messaging application or the Heroku cloud and, in order to make systems work 24/7 without any downtime, it has to tackle some technical challenges: Reliability, responsiveness, scalability, and constant availability.

### These challanges sound so good... how are they achieved?

Concurrency is at the heart and soul of Elixir systems. The basic concurrency primitive is called an Erlang process (not to be confused with OS processes or threads), and typical systems run thousands or even millions of such processes. This processes are managed by the BEAM (Erlang virtual machine). It uses its own schedulers to distribute the execution of processes over the available CPU cores, thus parallelizing execution as much as possible. Processes are completely isolated from each other and communicate via asynchronous messages. They share no memory, and a crash of one process doesn’t cause a crash of other processes. Moreover, you are provided with means to detect a process crash and do something about it: typically, you start a new process in place of the crashed one. Communication between processes works the same way regardless of whether these processes reside in the same BEAM instance or on two different instances on two separate, remote computers. In case you already haven’t guessed it, all these features are inherited prom Erlang!

### Can we talk about Elixir now?

Elixir is an alternative language for the Erlang virtual machine that allows you to write cleaner, more compact, code that does a better job of revealing your intentions. You write programs in Elixir and run them normally in BEAM. Both Erlang and Elixir are functional languages. They rely on immutable data and functions that transform data. One of the supposed benefits of this approach is that code is divided into many small, reusable, composable functions.

You can use Erlang libraries from Elixir and vice versa. There is nothing you can do in Erlang that can’t be done in Elixir, and usually the Elixir code is as performant as its Erlang counterpart. One of the most important benefits of Elixir is the ability to radically reduce boilerplate and eliminate noise from code, which results in simpler code that is easier to write and maintain. Let's see an example. The following snippet applies the XML to the in-memory model, process the resulting changes and, finally, persist the model.

Erlang approach:

~~~
process_xml(Model, Xml) ->
  Model1 = update(Model, Xml),
  Model2 = process_changes(Model1),
  persist(Model2).
~~~

Elixir approach:

~~~
def process_xml(model, xml) do
  model
  |> update(xml)
  |> process_changes
  |> persist
end
~~~

What you've just seen is called **the pipeline operator**. `|>` Takes the result of the previous expression and feeds it to the next one as the first argument. The resulting code is clean, contains no temporary variables, and reads like the prose, top to bottom, left to right. 

### Everything is fine? Have we found the silver bullet of software engineering?

There are no silver bullets in this world (except for the actual silver bullets that kill vampires). Usually, when I am learning about a methodology, language or paradigm I don't find the dark spots. This is my post and I wouldn't think it's fair to do the same way, so I decided to make a list of all downsides.

* Erlang is by no means the fastest platform out there. The goal of the platform isn’t to squeeze out as many requests per seconds as possible, but to keep performance predictable and within limits.

* The ecosystem built around Erlang isn’t small, but it definitely isn’t as big as that of some other languages.

* Elixir’s ecosystem currently isn’t as mature as Erlang’s, but you can use practically any Erlang library from Elixir.

### Summary

* Erlang is a technology for developing highly available systems that constantly provide service with little or no downtime. It has been battle tested in diverse large systems for more than two decades.

* Elixir is a modern language that makes development for the Erlang platform much more pleasant. It helps organize code more efficiently and abstracts away boilerplate, noise, and duplication.

~~~
title:   'What the hell is Elixir?'
url:     'https://artjimlop.github.io/napalmdrivendevelopment/what-is-elixir.html'
author:
  name:  '@artjimlop'
~~~

