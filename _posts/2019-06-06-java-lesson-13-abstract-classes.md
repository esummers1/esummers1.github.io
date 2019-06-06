---
bg: "rails.jpg"
layout: post
title:  "Java Lesson 13 - Abstract Classes"
crawlertitle: "Java Lesson 13"
summary: "Abstract Classes"
date:   2019-06-06 11:00:00 +0000
categories: posts
tags: ['java']
author: Eddie Summers
---

In the previous lesson we looked at interfaces. Interfaces allow you to specify a contract that an object must honour to be considered of that interface's type. This lets us compose the behaviour of our objects in a polymorphic manner, but means we must implement this behaviour in every object that wants to honour the interface.

Imagine instead we wanted to have many objects inherit some common behaviour, but did not want someone to instantiate their parent class directly. We can do this by declaring the class **abstract**. This prevents the class being instantiated.

{% highlight java %}
abstract class Item {

    String description;

    Item(String description) {
        this.description = description;
    }
}

class Book extends Item {

    int numberOfPages;

    Book(String description, int numberOfPages) {
        super(description);
        this.numberOfPages = numberOfPages;
    }
}
{% endhighlight %}

We could define other classes that inherit from Item, while keeping Item abstract - a thing can't just be an "item" without being something more concrete.

The other benefit of abstract classes is that they can contain abstract methods. These look just like the method signatures we defined in interfaces last time, except they use the abstract keyword:

{% highlight java %}
abstract class Item {

    ...

    abstract String describe();
}
{% endhighlight %}

Now, any class that extends Item must provide an `@Override` implementation for `describe()`, just as with implementing an interface. Note that an abstract class can have methods with implementations - its children can override these, but don't have to.

## Abstract Class or Interface?

This is a tricky question. A good rule of thumb is that if you can get away with it, use an interface, as they make for a less rigid hierarchy. However if what you really need is to define a bunch of types that have some shared behaviour and data, it's better to make them inherit from an abstract class, rather than implementing an interface and duplicating their method implementations. Also note that abstract classes allow you to define common fields, which may be another deciding factor.

Remember though that you can always use both - you could use a class hierarchy (with an abstract class at the top) to define shared data, and interfaces to compose behaviours. Don't worry too much about this, as it will come naturally with practice.