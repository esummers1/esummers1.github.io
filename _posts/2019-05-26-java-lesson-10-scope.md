---
bg: "road2.jpg"
layout: post
title:  "Java Lesson 10 - Scope"
crawlertitle: "Java Lesson 10"
summary: "Scope"
date:   2019-05-26 19:00:00 +0000
categories: posts
tags: ['java']
author: Eddie Summers
---

Scope - and hence, access control - is a big and important topic. A good program that contains many moving parts should keep them as separate from each other as possible, and have them only communicate with each other using agreed channels.

Think of it like a physical connector, such as a USB cable. Because there is an agreed contract that a device that connects by USB must fulfill, anyone with a USB connector can connect to it. Because this contract is agreed, the internal workings of such a device can change completely without the client - the other machine connected to it - being any the wiser.

Similarly, if we want to swap out the kind of database our web service uses, and we have properly encapsulated the code that speaks to the database, we can change that implementation without affecting the rest of the program, provided we still fulfill the same contract as before.

## Public Scope
Our first and most important tool for this effort is scope. Scope defines what a client - i.e. code in some other part of the program's codebase - can access. Recall the main method signature:

{% highlight java %}
public static void main(String[] args) {}
{% endhighlight %}

The first keyword, `public`, defines how visible this method is to clients. Public means that this method can be accessed by _anyone_ - anywhere in any of the packages (more on this soon) in our project, and even in other programs entirely. When you use the methods of the ArrayList class, which is from the `java.util` library and hence entirely separate to your program, you are calling its public ones.

## Package-Private Scope
Up until now I have avoided using any access modifiers in our code examples. This has led constructors, for example, to look like this:

{% highlight java %}
Dog(String name, float weight) {
    ...
}
{% endhighlight %}

A method or field without an access modifier can be called or used by any client in the same Java package.

## Protected Scope
Methods or fields which are declared `protected` are accessible only by code within the same class, or code in any **subclass**. Usually a class which has children will want to have protected rather than private fields - unless it wants to maintain control of the state of those fields and not allow child classes to access them.

## Private Scope
Methods or fields which are declared `private` are accessible only within that class. As we will explore next lesson, when you add things to a class your instinct should probably be to make them private, unless they are specifically needed outside.

Note that this private scope extends all members of the class, including inner classes. This means that private fields and methods of the outer class instance are accessible to inner class objects, and private fields and methods of the outer class **itself** are accessible to static nested class objects.

For the former, the following, somewhat confusing syntax is used:

{% highlight java %}
String something = OuterClass.this.fieldName;
{% endhighlight %}

It seems like `fieldName` would be a member of the _inner_ class instance due to it coming after `this`, but it will in fact refer to the `fieldName` field of the outer class instance.

## Local Scope
Consider the following snippet:

{% highlight java %}
for (int i = 0; i < 10; i++) {
    System.out.println("Hello number " + i);
}

System.out.println(i);
{% endhighlight %}

This will fail to compile, as the variable `i` will be inaccessible outside the for-loop. It is considered local to that code block. In general, variables such as this are accessible from the moment of their creation until the closure of the block (with curly braces {}) in which their creation occurred. You can consider them implicitly private to that block.