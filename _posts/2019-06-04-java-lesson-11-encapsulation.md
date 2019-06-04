---
bg: "tools.jpg"
layout: post
title:  "Java Lesson 11 - Encapsulation"
crawlertitle: "Java Lesson 11"
summary: "Encapsulation"
date:   2019-06-04 17:00:00 +0000
categories: posts
tags: ['java']
author: Eddie Summers
---

This is a lesson on style and good practice rather than syntax. We saw in the last lesson how you can control access to the members of a class. You should try as much as possible to make use of this to encapsulate different parts of your program. This idea was also introduced last lesson - the ideal is a situation where the different moving parts of the application only communicate through agreed channels.

Consider a contrived example. Let's say we have a Diet class that stores someone's macronutrient targets for a day:

{% highlight java %}
public class Diet {

    private int carbs;
    private int fat;
    private int protein;

    public Diet(int carbs, int fat, int protein) {
        this.carbs = carbs;
        this.fat = fat;
        this.protein = protein;
    }
}
{% endhighlight %}

In this example, a Diet object is immutable. This is because its fields, once initialized, cannot be changed by a user of the object. Let's imagine we wanted to provide a way for such a client to get the number of calories the person should eat per day:

{% highlight java %}
...

    public getCalories() {
        return carbs * 4 + fat * 9 + protein * 4;
    }
{% endhighlight %}

Note that we don't actually need to store the number of calories anywhere in the object, but the client is **unaware** of this. In fact, to the client it doesn't matter whether that number is stored on a field or computed at the moment of the request. The Diet object just fulfils its behavioural contract.

## Field Access

A common Java idiom taught to beginners is to create a class, add some private fields, and then create getter and setter methods for each of the fields, e.g.:

{% highlight java %}
public class Animal {

    private String name;
    private int numberOfLegs;

    public Animal(String name, int numberOfLegs) {
        this.name = name;
        this.numberOfLegs = numberOfLegs;
    }

    public String getName() {
        return name;
    }

    public int getNumberOfLegs() {
        return numberOfLegs;
    }

    public void setName(String name) {
        this.name = name;
    }

    public void setNumberOfLegs(int numberOfLegs) {
        this.numberofLegs = numberOfLegs
    }
}
{% endhighlight %}

This provides us some additional degree of control - if we want to have some kind of custom logic on the access (get) and mutate (set) events, such as saving a record of the access, this lets us do that. Or we could later change the underlying implementation - it would be easy in our Diet object to have previously had a private `calories` field, and now remove it and calculate it from the macronutrients each time.

However this is distinct from the fact that we've hidden the class's internal implementation, and then just exposed it again in a more verbose manner. What is preferable is to think carefully about what we want to expose to clients, and add just the ones we need. We might decide that in fact, we don't want clients to have any direct access to the object's fields, and just permit them to use its behaviour.

## Immutable Objects

An object that's immutable is one whose state cannot be changed. Objects can be themselves mutable and have immutable fields. All this really means is that if you create a class with some private fields whose values can only be **set** when the object is created (or just once, and never again), that part of the object is immutable.

Where they are appropriate, using immutable objects is usually preferable to using mutable ones. It can make your program easier to maintain and debug, and reduces the chance of unwanted behaviour in multi-thread conditions (more on this later). However don't be afraid to make objects mutable if this is how they should behave.