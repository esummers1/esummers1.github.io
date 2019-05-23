---
bg: "bridge.jpg"
layout: post
title:  "Java Lesson 5 - Classes and Objects"
crawlertitle: "Java Lesson 5"
summary: "Classes and Objects"
date:   2019-05-23 10:00:00 +0000
categories: posts
tags: ['java']
author: Eddie Summers
---

As previously covered, we can create our own objects in Java. A **class** is in essence a blueprint for creating objects. Classes can define data their objects will store - **fields** - and provide behaviour - **methods**, in any combination. Each class should be in its own `.java` file, where the name of the file is the same as the name of the class, and have a capitalized name:

{% highlight java %}
class Application {
}
{% endhighlight %}

## Constructors

To define a constructor for this class, we declare a function whose name and return type are that of the class:

{% highlight java %}
class Dog {

    // Fields of a Dog object
    String name;
    float weight;

    // Dog constructor
    Dog(String name, float weight) {
        this.name = name;
        this.weight = weight;
    }
}

...

class Main {
    public static void main(String[] args) {

        // Constructor invocation
        Dog fido = new Dog("Fido", 10f);
    }
}
{% endhighlight %}

Note the use of the `this` keyword within the constructor. This clarifies that we mean the field of _this object_ - i.e. when we say `this.name` in the constructor, we mean that the `name` field of the Dog instance being created in the constructor will be assigned a value. This is to distinguish it from the `name` parameter in the constructor's signature, though these do not have to have the same name.

### Implicit Constructors

If you do not provide a constructor for a class, you can still create an instance of the class using an implicit no-argument constructor - this would be `new Dog();` in the example above. Note that in our `Main` above we couldn't actually invoke this constructor, as we had explicitly provided one with a different signature.

## Use of Classes

A class should represent some entity or piece of a system - you could imagine a car consisting of an `Engine` class, a `Steering` class and so on. Ideally it should only be responsible for one thing; if you find your class growing and doing lots of different stuff, it's time to split it into smaller classes. Don't worry if these things don't come naturally; it takes time to think this way.