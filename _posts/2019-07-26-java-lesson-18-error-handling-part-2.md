---
bg: "tools.jpg"
layout: post
title:  "Java Lesson 18 - Error Handling, Part 2"
crawlertitle: "Java Lesson 18"
summary: "Error Handling"
date:   2019-07-26 12:00:00 +0000
categories: posts
tags: ['java']
author: Eddie Summers
---

Last time, we looked at the basics of error handling in Java. But we've only just scratched the surface. There are three more features to examine: compile-time error validation, custom Exceptions, and try-with-resources.

## Compile-Time Error Validation

Java allows you to deliberately throw an Exception using the `throw` keyword. This gives you a very powerful way to send messages between different parts of your program. Importantly, this means that you can specify that your methods should be invoked within a `try` - allowing you to encapsulate potential error sources and shield the rest of the program from them.

If we throw a checked Exception manually, we need to catch it somewhere, or the program will not compile. We can either do this by wrapping the code that might throw the Exception in a `try-catch`, or delegate this responsibility to the method's caller by declaring in its signature that it `throws` the Exception of this kind. For example:

{% highlight java %}
try {
    divideBy(1, 0);
} catch (ArithmeticException e) {
    System.err.println("Stop doing garbage");
}

...

double divideBy(double num, double den) throws ArithmeticException {
    if (den == 0) {
        throw new ArithmeticException();
    } else {
        return num / den;
    }
}
{% endhighlight %}

## Custom Exceptions

You can define your own Exception types that extend Exception - think of the benefit of this as coming up with your own language for describing possible failure conditions in your program. If a method that tries to link out to a database throws a `DatabaseOfflineException` if the database doesn't respond, or a `NetworkConnectionOfflineException` if the request can't even be made, then the client that invokes the connection attempt can gracefully and specifically catch these errors, and the code will be inituitive.

{% highlight java %}
public class NetworkConnectionOfflineException extends Exception {
    public NetworkConnectionOfflineException() {
        super("Computer is not connected to the internet.");
    }
}
{% endhighlight %}

Something like the above is more than is required - the call to `super()` which provides a custom message is a bonus. Then, when catching an Exception of this type we can print `e.getMessage()` to get a human-readable description, to go with `e.getStackTrace()`, which gives us the exact moment of failure in the terminal. All Exceptions can provide us these details.

## Try-with-Resources

When you use a resource such as a Scanner object, you're meant to close it once you're done with it. Since Java 7, any resource of this kind which implements `AutoCloseable` can be handled using the clever `try-with-resources` construct:

{% highlight java %}
try (Scanner sc = new Scanner(System.in)) {
    // do something with the scanner
} catch (Exception e) {
    // handle error case
}
{% endhighlight %}

The Scanner created during the `try` declaration will be automatically closed when the whole block is finished. This replaces the more awkward `finally` approach:

{% highlight java %}
try {
    Scanner sc = new Scanner(System.in)
    // do something with the scanner
} catch (Exception e) {
    // handle error case
} finally {
    if (sc != null) {
        sc.close();
    }
}
{% endhighlight %}

This reduces the amount of boilerplate code we need, which in my opinion is almost always a good thing.