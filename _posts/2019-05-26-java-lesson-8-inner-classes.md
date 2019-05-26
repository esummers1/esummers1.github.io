---
bg: "road.jpg"
layout: post
title:  "Java Lesson 8 - Inner Classes"
crawlertitle: "Java Lesson 8"
summary: "Inner Classes"
date:   2019-05-26 17:00:00 +0000
categories: posts
tags: ['java']
author: Eddie Summers
---

Sometimes we might have a use for an object that only makes sense as an "inner" object of another. This would be useful if there is a strong logical coupling between the two, i.e. they make sense together and one is not often used without the other.

Other reasons include having custom Exceptions (more on this soon), Enums that are tied to another object (again, more on this to come) or if you want to create a field on a class for which you don't have already have a type.

{% highlight java %}
class Dog {

    class Trick {

        String description;

        void do() {
            System.out.println("Doing " + description);
        }
    }

    List<Trick> tricks;

    void teachTrick(Trick trick) {
        tricks.add(trick);
    }

    void doAllTricks() {
        for (Trick trick : tricks) {
            trick.do();
        }
    }
}
{% endhighlight %}

Note how the inner class `Trick` is declared in the normal manner, but inside its containing Dog class. It is important to understand that while this might look like a parent/child relationship, there is no inheritance going on. Trick is distinct from Dog.

Since the Trick class is a **member** of Dog, you must instantiate a Dog before creating tricks. Also, these Tricks will retain a reference to that specific Dog. This doesn't make too much sense in this example, since we're passing Tricks in from outside Dog. If we want the inner class to be instantiable without creating an instance of the outer class, we can instead make it a static nested class.

## Static Nested Classes

Just as a static field belongs to the class, not to the instance, a static nested class (which is an inner class declared as static) belongs to the outer class itself, not an instance of it.

{% highlight java %}
// Creation of inner object when it is NOT static
Dog dog = new Dog();
Dog.Trick trick = dog.new Trick();

// Creation of inner object when it IS static
Dog.Trick trick = new Dog.Trick();
{% endhighlight %}

If the first example seems clumsy, that's because it is - usually you wouldn't want to create an inner class object from a different class entirely. Typically the reason for having an inner class is that the outer class alone needs it for something. If you are writing code in the outer class, you just create it like any other object:

{% highlight java %}
class Dog {

    ...

        Trick trick = new Trick();

    ...

}
{% endhighlight %}