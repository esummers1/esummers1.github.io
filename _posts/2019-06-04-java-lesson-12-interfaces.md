---
bg: "wires.jpg"
layout: post
title:  "Java Lesson 12 - Interfaces"
crawlertitle: "Java Lesson 12"
summary: "Interfaces"
date:   2019-06-04 18:00:00 +0000
categories: posts
tags: ['java']
author: Eddie Summers
---

An **interface** in Java is a special kind of type. It is declared similarly to a class, but while a class specifies the data and behaviour of an object, an interface in the abstract represents a contract that an object that **implements** it will honour. For example:

{% highlight java %}
interface Pet {

    // Declares method signature alone, without the {body}
    void play();
}

class Dog implements Pet {

    void play() {
        System.out.println("Dog is fetching a stick");
    }
}
{% endhighlight %}

At first, it may just seem like the interface is hindering us unnecessarily. Since `Dog` **implements** `Pet`, it has agreed to take on the responsibilities that being a Pet entails. But Dog has to do the actual implementing of the behaviour!

## Advantages

Interfaces have two very powerful features. The first is that an object implementing the interface can through polymorphism be the value of any variable of that interface's type. This means that any time we declare a Pet, we can use a Dog e.g. `Pet fido = new Dog();`. Fido can then be passed around through methods that specify a parameter of type Pet - this is also true of any other class that implements Pet.

The second is that while a class can only extend/inherit from one class, it can implement any number of interfaces (e.g. `class Dog implements Pet, Barker {...`). This allows you to **compose** objects that fulfil various behavioural contracts. For example, in lesson 4 we saw that the `List` interface is implemented by a few different classes, including `ArrayList` and `LinkedList`. As it happens, LinkedList also implements the `Queue` interface, so any time you need to use the agreed behaviours of a Queue, a LinkedList will do. This is the true meaning of polymorphism, i.e. the taking on of many forms.

## Composition Over Inheritance

It is advantageous to compose your objects' behaviours using interfaces rather than inheritance, because while hierarchies of classes based on inheritance are easy to create, they are brittle - remember you can only extend one class, so if you want to change the hierarchy it may be very difficult. If you have the behaviours that different pets have e.g. `Playable`, `Barkable`, `Sittable`, `Scratchable` you can mix and match these for your objects as appropriate. Then any time you just need something that can Sit, you can declare its type `Sittable`. Normally this is described as a "has-a" relationship, in that a Dog _has_ the ability to sit, rather than _being_ an Animal, which it could also be. This is much more flexible because you can implement additional interfaces without redesigning your class hierarchy.

The -able suffix I've been using is often used to distinguish interfaces from superclasses, but you might prefer `Player`, `Barker`, `Sitter`, `Scratcher` etc. so that you might say `Barker fido = new Dog();`.

Note that if a class extends a class which implements an interface, your child class will implicitly implement that interface. The parent class's method implementations can be overridden as normal, including the ones that are specified by that interface. If a class declares that it implements an interface but does not provide implementations for all of its methods, your program will not compile.

It can be hard to visualize how this should work in practice when speaking abstractly. You'll naturally find uses for interfaces in your programs - just keep in mind it is usually preferable to use them over abstract classes, which we'll discuss next.