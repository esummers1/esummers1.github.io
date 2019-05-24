---
bg: "notre-dame.jpg"
layout: post
title:  "Java Lesson 7 - Inheritance"
crawlertitle: "Java Lesson 7"
summary: "Inheritance"
date:   2019-05-24 11:00:00 +0000
categories: posts
tags: ['java']
author: Eddie Summers
---

Java is an Object-Oriented Programming language. One of the key notions of OO languages is **polymorphism**. This means that objects can take on many forms, or more specifically that an object of some type may be acceptable where other types are specified. One mechanism for this is inheritance.

{% highlight java %}
class Animal {
    String name;
}

class Dog extends Animal {
}
{% endhighlight %}

In the above snippet we have an Animal class that has one field. Then we have a Dog class that `extends` Animal. This keyword indicates that a Dog is **also** an Animal. All Dogs can now be considered Animals, though not all Animals can be considered Dogs. This creates an "is-a" relationship - a Dog **is** an Animal. This means two things:

1. Any time you need to provide or use an Animal, you can use a Dog instead
2. Anything an Animal can do or store, a Dog can also do or store

So a Dog object will have a `name` field, even though one is not provided on Dog.

This is a very powerful tool. Now if we have a bunch of objects that are similar in some fundamental way - share some properties and behaviour - we can extract what is the same, put this in a superclass (or parent class, the one that the others extend), and extend that superclass in the subclasses (or child classes, the ones that do the extending). If we want to modify that common behaviour, we need only do it in one place.

## Construction
To construct a child class we need the `super` keyword. `super` allows us to refer to the parent class from the child. We need to do this in the first line of our constructor, and we can just call `super()`, since that is equivalent to calling its constructor by name.

{% highlight java %}
class Animal {

    String name;
    String species;

    Animal(String name, String species) {
        this.name = name;
        this.species = species;
    }
}

class Dog extends Animal {

    Dog(String name) {
        super(name, "Canis Lupus");
    }
}
{% endhighlight %}

Above, the `super()` call in Dog calls the Animal constructor of that signature, allowing us to construct the Dog object.

## Method Overriding
Extending a class in essence means that your subclass agrees to honour the contract that the superclass has with the rest of your program; it promises to have methods available with the same signatures, and to have at least the same data. However it does not promise to have the same _implementation_ of those methods. Otherwise there wouldn't be much point!

{% highlight java %}
class Animal {
    void greet() {
        System.out.println("Roar!");
    }
}

class Dog extends Animal {
    @Override
    void greet() {
        System.out.println("Woof!");
    }
}
{% endhighlight %}

Note that we tag the Dog's `greet()` method with the @Override annotation. This is not strictly required for the program to work, but it will allow the IDE to check that you are actually overriding a method. If you've made a mistake with the signature it will warn you immediately, rather than you needing to debug a misbehaving program later on.

If we invoke the `greet()` method on a Dog instance, we'll now get "Woof!" printed to the terminal, instead of "Roar!".

## Chain of Inheritance
A class can extend a class that is itself a subclass. This is actually what happens when you use the `extends` keyword, as all classes in Java implicitly inherit from `Object`. This fact creates interesting possibilities in defining how our objects work within the language at large, which we'll explore later on.

While this is possible, you should be careful about multi-step inheritance. Classes can only extend one other class in Java, and inheritance relationships create a tight coupling between the superclass and subclass. Imagine you have a chain of inheritance four classes long, and someone changes something in a method of the superclass at the top - this change will also occur in any subclass in any of the layers below that have not overridden this method. You could imagine a whole tree of classes affected by this change; a class implicitly extends all ancestor classes. Perhaps a better metaphor would be a house of cards.