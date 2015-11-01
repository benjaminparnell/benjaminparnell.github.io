---
layout: post
title: Functional first
---

I was having a conversation with one of my lecturers recently about functional
programming. They mentioned to me that if there was one thing they wish they
could change about the course that I am doing (BSc Computer Science) it would
be to introduce functional programming much earlier on in the course. I agreed.

But why is that?

In my opinion (and this post only reflects one side of a many sided argument),
functional programming is an easier to understand paradigm for programming.
Everything has one job and one job only. The way you think about problems is far
more descriptive than say the object orientated paradigm.

Let's look at an example.

A basic programming task that most programmers will have encountered when they
were learning to code is this: given an array of integers, add up all the
integers and return the result.

A Java solution:

```java
public int addUp(int[] numbers) {
  int result = 0;

  for (int index = 0; index < numbers.length; index++) {
    result += numbers[index];
  }

  return result;
}
```

And now a functional approach to the same problem (Clojure):

```clojure
(defn addUp
  [numbers]
  (reduce + numbers))
```

The idea behind this task is to learn how to *reduce* an array to a single
value, which means iterate over the array and call a function on each item,
which should return our accumulated value. So why not do just that?

In the Java example, we have to explain to the language *how* to perform a
reduce operation. In functional programming languages, the language itself
understands that this is a common operation, and caters for it with an inbuilt
reduce method.

This is a very simple problem, but once you take into account the tool set you
get with functional languages and start throwing things like map and filter into
the mix, you quickly have a very easy way to think about problems. There is far 
less "boilerplate code" and confusion about where methods should live and what they
should do.

I am by no means saying that functional programming is **the** way to program
and that it's the silver bullet sent by Richard Stallman himself to save us from
damnation - I am saying its a nice way to be introduced to programming. If you
want to get into the real functional vs object orientated debate,
read [this excellent
post](http://blog.cleancoder.com/uncle-bob/2014/11/24/FPvsOO.html) by Uncle Bob.

While I understand the argument that novice coders should learn *how* things
like reduce work by writing them, that isn't the reality of software
development. The likelihood of you having to write your own reduce function in
your day to day job is slim. I think understanding why things like reduce exist
is more important than understanding how to make it yourself.

And that was exactly the point my lecturer had. If a student has no experience
at all with coding, why not give them a helping hand and a tool that teaches them the classic unix
philosophy of "Do one thing well"? Having at least one class in functional
programming in the first year of a computer science course starts to seem pretty
essential when you think about it that way.

Interested in trying out some functional programming? I would recommend giving
[Clojure](http://clojure.org/) a go.
