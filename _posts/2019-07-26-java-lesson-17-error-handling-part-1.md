---
bg: "road2.jpg"
layout: post
title:  "Java Lesson 17 - Error Handling, Part 1"
crawlertitle: "Java Lesson 17"
summary: "Error Handling"
date:   2019-07-26 11:00:00 +0000
categories: posts
tags: ['java']
author: Eddie Summers
---

Handling errors is an important part of any program. Wherever we interact with entities outside the program - databases, users, other systems, etc. - we will always need to handle errors. 

Java has a rich set of features for dealing with errors. When the program encounters a problem, it will throw an Exception `object` and terminate. If, as is usually the case, you'd rather the program handle the error gracefully and continue running, we will need to master handling these Exceptions.

The first weapon in your arsenal is the `try-catch` block. This consists of a thing you want to attempt (the try block) and something to do if there's a problem anywhere within the try block (the catch block).

{% highlight java %}
try {
    connectToDatabase();
} catch (Exception e) {
    System.err.println("Uh oh, something went wrong.");
}
{% endhighlight %}

There are a few things going on here. First we attempt to connect to a database (imagine this method is implemented somewhere nearby). This is an operation that can fail - maybe our network connection is offline, or the database itself is borked. In this situation, an Exception is thrown. We **catch** this Exception in the catch block, giving it a name (`Exception e`). We can refer to the Exception object inside this block using this name.

Also, I've used the `System.err` PrintStream instead of the usual `System.out`. This doesn't differ much - it just will probably come up in red in your IDE's terminal. If we have some other output stream we want to use, we could use that instead.

Now, notice that we specified we're looking for an `Exception`, specifically. This is a type - the superclass from which all more detailed Exceptions inherit. Since it is an object like any other, we can do all the things we'd normally do with objects, such as extend it with our own child classes.

There are many built-in Exception types. For example:

{% highlight java %}
try {
    int[] numbers = new int[]{1, 2, 3};
    int number = numbers[6];
} catch (ArrayIndexOutOfBoundsException e) {
    System.err.println("You did garbage");
}
{% endhighlight %}

Just as child classes can be referred to by their ancestor types, so specific Exceptions can be referred to by ancestor Exceptions. This means that catching `Exception e` will **always** catch any exception. Also, note that you can have multiple `catch` blocks. This leads us to an interesting situation:

{% highlight java %}
try {
    int[] numbers = new int[]{1, 2, 3};
    int number = numbers[6];
} catch (Exception e) {
    System.err.println("Uh oh, something went wrong.");
} catch (ArrayIndexOutOfBoundsException e) {
    System.err.println("You did garbage");
}
{% endhighlight %}

What do you think will be printed to the terminal?

If you guessed that it's both messages, that is incorrect. The correct answer is just the first one. Only one `catch` block in a `try-catch` can be entered - just like an `if-else` block. This means that if some Exception could be one of many of your caught types, you need to order them such that it will encounter the preferred one first. Alternatively, just put more general types later. The correct way round for the contrived example above is to catch `ArrayIndexOutOfBoundsException` first.

## Checked vs Unchecked Exceptions
Lastly, we need to distinguish between checked and unchecked Exceptions. This distinction will become even more important in the next lesson.

An **unchecked** Exception is one which represents a state the program should probably not be expected to recover from. They are those which are of type `Error`, `RuntimeException`, and their subclasses. `ArrayIndexOutOfBoundsException` is one of these, as is `NullPointerException`, possibly the most famous of all. These *will not* restrict compilation if uncaught.

A **checked** Exception is one which the program should reasonably be expected to recover from. They are all Exceptions which are not unchecked ones. These *must* be caught somewhere in order for the program to compile. They include things like `ClassNotFoundException` or `IOException`.