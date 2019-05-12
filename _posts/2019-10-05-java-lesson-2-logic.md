---
bg: "library.jpg"
layout: post
title:  "Java Lesson 2 - Operators and Branching Logic"
crawlertitle: "Java Lesson 2"
summary: "Operators and Branching Logic"
date:   2019-10-05 21:00:00 +0000
categories: posts
tags: ['java']
author: Eddie
---

Java, like all good programming languages, has the usual set of mathematical and logical operators. We can use logical operators to determine which branch of a program is executed.

Below are the mathematical operators:

{% highlight java %}
int i = 2 + 3;          // addition
int j = 5 - 4;          // subtraction
int k = 4 * 9;          // multiplication
int l = 8 / 2;          // division
int m = 9 % 2;          // modulo (remainder after division)
{% endhighlight %}

Boolean values can be passed or assigned as literals or as the result of expressions - e.g. `return 3 > 2;` is equivalent to `return true;`, although rather less clear. Expressions can be combined using the logical operators:

{% highlight java %}
boolean one = 2 < 3;                      // less than - expression is true
boolean two = 2 <= 3;                     // less than or equal to - expression is true
boolean three = 3 > 2;                    // greater than - expression is true
boolean four = 3 >= 2;                    // greater than or equal to - expression is true

boolean five = 7 == 8;                    // is equal to - expression is false
boolean six = 7 != 8;                     // is not equal to - expression is true

boolean seven = true && false;            // AND operator - expression is false
boolean eight = true || false;            // OR operator - expression is true
boolean nine = true && (false || true);   // OR is in brackets and evaluated first

boolean ten = true && !false;             // NOT operator (!) - expression is true
{% endhighlight %}

Expressions can be composed of arbitrarily many layers of these operators. In Java, AND will evaluate before OR if both are on the same level, but it's usually best to nest things properly in brackets to avoid confusion. Objects should be compared with the `Object.equals(object)` method rather than the `==` operator, but this is a topic we'll cover more later on.

To do something on the condition that some expression is true, we use `if` statements:

{% highlight java %}
int a = 5;
int b = 6;

if (a != b) {
    // do something
} else {
    // do something else
}
{% endhighlight %}

An `if` block can have as many `else if` blocks as you like - these specify a condition that must be true for the block they contain to be executed, just like `if`. If you do not provide an `else` block, and none of the `if` or `else if` conditions are true, all of the blocks will be skipped entirely. If one of your `else if` conditions is true _in addition_ to an earlier `if` or `else if` condition being true, it will be skipped - once one block is executed, **none of the others is checked**. So, for example:

{% highlight java %}
if (1 < 2) {
    // true, so this block will be entered
} else if (2 < 3) {
    // also true, but this block will never be entered
}
{% endhighlight %}

A common idiom is to evaluate a boolean value directly, i.e. `if (booleanVariable == true)` is equivalent to `if (booleanVariable)`. Also, rather than asking if something `== false`, it's simpler to say something like `if (!booleanVariable)`. So, for instance:

{% highlight java %}
boolean isRed = true;
boolean isBlue = false;
boolean isBlack = false;

// We want to do something if our colour is red, but only if it's not also black
if (isRed && !isBlack) {
    // do the thing
}
{% endhighlight %}