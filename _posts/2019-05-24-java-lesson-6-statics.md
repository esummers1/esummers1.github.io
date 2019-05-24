---
bg: "castle.jpg"
layout: post
title:  "Java Lesson 6 - Static Fields and Methods"
crawlertitle: "Java Lesson 6"
summary: "Static Fields and Methods"
date:   2019-05-24 10:00:00 +0000
categories: posts
tags: ['java']
author: Eddie Summers
---

In the last lesson we saw how to define **instance** fields and methods for objects. Recall that fields are declared in the class outside of any method - by convention they are grouped at the top. A field such as we saw last time is a property of the specific object it belongs to. If a Car class has a `colour` String field, and we have two Car objects with different values for `colour`, these values belong to their respective Car objects. Similarly if we have some behaviour for a Car, e.g. `honk()`, this is invoked on the object itself.

## Static Keyword

The `static` keyword allows us to specify that something - a field, method or inner class (we'll come to these later) - belongs to the _class_ itself, not to an instance of that class. If you declare a field `static` and access it from outside the class, you use a reference to the class itself rather than an instance of it:

{% highlight java %}
class Gorilla {

    // An instance field
    String name;

    // A static field, which we have initialized here
    static boolean isEndangered = true;

    Gorilla(String name) {
        this.name = name;
    }
}

class Main {

    public static void main(String[] args) {

        Gorilla koko = new Gorilla("Koko");

        // Access static field by class reference
        // If we'd tried to access koko.isEndangered, it would not compile
        System.out.println(Gorilla.isEndangered);
    }
}
{% endhighlight %}

The same logic applies to methods. A static method is one that belongs to the class, not to an instance. This, as with static fields, means it can be used without instantiating the class. Notice that the `main` method declaration above is static.

While this is simple to understand, knowing when to use statics is not always easy. Note that a static method can't be overridden by a subclass (wait for the next lesson!). A method _can_ be static if it doesn't use any of the instance fields of the class that contains it, but if you find yourself writing a lot of these methods, it's worth considering whether that class is actually the right place for the method to go.

A common valid use of static methods is in utility classes, i.e. classes that just contain static methods - for example a UrlUtils class in a web service that provides helpers for parsing and constructing URLs, or a Geometry class in a 2D game that helps with calculating bearings between lines, distances between points and so on.

### Constants

Another use of `static` is to define constants. Imagine you have a Geometry class that has some methods that need a Pi constant. It would be silly to type Pi out as a literal in each case, so you could define a constant for the class:

{% highlight java %}
class Geometry {

    // For constants, we use UPPER_SNAKE_CASE by convention
    static final double PI = 3.1415927;

    static double calculateAreaOfCircle(double radius) {
        return PI * radius * radius;
    }
}
{% endhighlight %}

Above we use the `final` keyword - for a variable, this means that once it is assigned a value, it is **immutable** - it cannot be changed. Here we set this immediately; if a `final` field is not assigned a constant value like this, it can be set like any other field at runtime, but cannot then be changed. A field is only considered a constant if it is both `static` and `final`.