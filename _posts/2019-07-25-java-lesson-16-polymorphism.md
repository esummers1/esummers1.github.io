---
bg: "castle.jpg"
layout: post
title:  "Java Lesson 16 - Polymorphism"
crawlertitle: "Java Lesson 16"
summary: "Polymorphism"
date:   2019-07-25 10:00:00 +0000
categories: posts
tags: ['java']
author: Eddie Summers
---

We've discussed ideas such as defining your own objects, inheritance and abstraction. All of these are tools for achieving the primary benefit of an object-oriented language like Java: polymorphism.

Polymorphism is easy to palm off as using superclasses and interfaces to introduce dynamic behaviours, but that's missing the essential point. Types are contracts - if an object is of a certain type, you can be guaranteed that it will honour the same contract that any other object of that type will honour. For example, a `List` implementation will let you add new items on the end, and retrieve elements from any index.

The behaviours of an object can be composed by honouring many contracts. For example, a Java `LinkedList` is a `List`, but it's also a `Queue`, and an `Iterable`. An object of concrete type `LinkedList` can be considered to be these types as well, for any time that you need something they promise to provide.

This is what's really happening when you create an `Animal` class that is extended by `Dog`, and then say `Animal a = new Dog();`. `Dog` honours the `Animal` contract. This should lead you to be as vague as possible when specifying the type you require for something. For example, let's say you have a function that traverses a collection and returns a new collection with some transformation applied, e.g. a filter. You could specify that the collection be a `List` - or even (if you were being really foolish) an `ArrayList` - but you could just ask for an `Iterable`, and use its iterator (or the `forEach()` method) to traverse the collection. This way you can receive any object that implements `Iterable`, which will give you the same functionality but allow more clients in the system to use it.

Obviously, if there were behaviours specific to `List` that you needed, you would then specify a `List` as your parameter instead. As an aside, the way you do this for a collection of items of any type is a subject for a future lesson.