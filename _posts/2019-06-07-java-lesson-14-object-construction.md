---
bg: "tools2.jpg"
layout: post
title:  "Java Lesson 14 - Object Construction"
crawlertitle: "Java Lesson 14"
summary: "Object Construction"
date:   2019-06-06 12:00:00 +0000
categories: posts
tags: ['java']
author: Eddie Summers
---

Usually, we create objects using their constructors. However there is an alternative mechanism - the **static factory method**. Consider the following:

{% highlight java %}
class Dog {
    String name;

    private Dog(String name) {
        this.name = name;
    }

    create(String name) {
        return new Dog(name);
    }
}

class Main {
    public static void main(String[] args) {
        Dog dog = Dog.create("Fido");
    }
}
{% endhighlight %}

This kind of approach has a couple of advantages. It allows us to abstract creation away from the object's actual constructor. If we wanted to control the existing instances of an object, this would let us either construct a new object or return one of the existing ones, without the client needing to know.

Also, this same benefit means that if we wanted to delegate to an appropriate implementation, we could. In Java 9, there were static factory methods added to the Collections library, meaning you can say something like `List<String> strings = List.of( ... );`, with '...' being the items you want to initialize the list with. We don't know whether this creates an ArrayList, a LinkedList or any other kind of list - but the client doesn't care, because whatever it is will still honour the List contract. We can do the same by implementing an `of()` static factory method in the abstract parent class of whatever our objects are.

Additionally, it can allow us more flexibility when creating child objects. Remember that the call to the superconstructor must be the first line in a child class's constructor. What if we want to do some kind of operation before doing that? This way, we can do that in the factory method, and _then_ call the child class's constructor.

A further benefit is that you could create conversion methods taking similar objects. Let's say that you were building a mock social network, and had some heavyweight `User` object that contained a bunch of data. If all you needed for some list view page was their name and picture, you might make a `PersonPreview` object that had a `from(User user)` factory method. Then you could easily produce your new lighter-weight objects with `PersonPreview preview = PersonPreview.from(user);`. This kind of thing can also make your code easier to read.

## Non-Instantiable Classes

Sometimes you might want to have a class that only contains static methods, and which should not be instantiated. Some would recommend to make the class abstract, but this indicates that it is designed to be extended. Our class would only have static methods, which cannot be overridden, so this would be confusing. The cleanest solution is to just declare a private constructor.