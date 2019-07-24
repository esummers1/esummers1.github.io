---
bg: "library.jpg"
layout: post
title:  "Java Lesson 15 - Comments"
crawlertitle: "Java Lesson 15"
summary: "Comments"
date:   2019-07-24 12:00:00 +0000
categories: posts
tags: ['java']
author: Eddie Summers
---

Most people can learn to write a program which does something. The real challenge is to design it so that it's easy to add new features and behaviour. The first step in accomplishing this is making your code easier for other people to understand, and your most basic weapon here is the comment.

Java supports three kinds of comments:

{% highlight java %}
// Single line comments

/*
 * Multiple
 * line
 * comments
 */

/**
 * Javadocs
 */
{% endhighlight %}

The purpose of comments should be to convey your intent, not the details of the implementation. The latter should be obvious enough from the way you've written what follows - using clear steps and descriptive names for your functions and variables. Compare the following:

{% highlight java %}
// Imagine functions "c" and "print" both just print the argument.

/*
 * Given two numbers, print out the second one if the first one is divisible by
 * it.
 */
private void pFac(int a, int b) {
    if (a % b == 0) {
        c(b);
    }
}

...

private void printIfFactor(int number, int factor) {
    if (number % factor == 0) {
        print(factor);
    }
}
{% endhighlight %}

In this example, the latter function doesn't need describing, as its descriptive names for things makes it clear what's going on. Excessive comments can be worse than no comments at all, as they make the code harder to read. This is especially true of completely unnecessary comments, e.g.:

{% highlight java %}
// Print all numbers from 1 to 10
for (i = 1; i <= 10; i++) {
    System.out.println(i);
}

// Make a equal to b x 2
int a = b * 2;
{% endhighlight %}

The ideal time to use a single-line comment is above a one-line operation which is reasonably clear but whose significance may not be obvious. You can also use comments to group together a few statements which wouldn't make sense to extract to their own function.

Multiple-line comments should be used sparingly. One time might be when there is some reason you've had to do something a particular way which might not be obvious. Another might be to explain that due to some third-party dependency you're using, things need to be done here in a certain way.

Javadocs - with the extra asterisk on the opening line - play a special role in Java. Documentation generation tools and IDEs hook into this syntax: the former can create documents for all your classes and functions automatically, and the latter can show you a detailed documentation view if you use a shortcut (Ctrl+J in IntelliJ, for example) when pointing at a function. A Javadoc looks like this:

{% highlight java %}
/**
 * Generate a random integer between 0 and the provided maximum, inclusive. Uses
 * the provided long as a seed.
 *
 * @param max - the maximum size of the generated number
 * @param seed - the seed used for random number generation
 * @return the random number
 */
private static int generateNumber(int max, long seed)...
{% endhighlight %}

A full Javadoc has these @param and @return tags, which should be descriptions of these attributes, rather than just their names or types. For short functions this can make classes look quite verbose, so you will need to decide for yourself in your own projects whether it makes sense to (and where to) include full Javadocs. The tools which hook into them will still work if you merely provide the description and forego the @param and @return tags.

Comment sparingly, and descriptively. Describe *why* the program is doing what it's doing, rather than *what* it's doing.