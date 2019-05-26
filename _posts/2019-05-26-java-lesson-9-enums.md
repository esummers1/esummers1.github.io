---
bg: "wires.jpg"
layout: post
title:  "Java Lesson 9 - Enums"
crawlertitle: "Java Lesson 9"
summary: "Enums"
date:   2019-05-26 18:00:00 +0000
categories: posts
tags: ['java']
author: Eddie Summers
---

Enums - enumerations - are a way of declaring constants. They allow you to define a set of values that the enum type can have. They are declared in a similar way to classes:

{% highlight java %}
enum Weekday {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY;
}
{% endhighlight %}

Weekday is now a type; you could have a class with a field of type Weekday. The only values it can be assigned are the values of the Weekday enum provided above; otherwise it would be like trying to assign a boolean the value '2.7'.

Enums in Java are quite powerful and can contain methods of their own, but often the enumeration of values is enough. It's common to see enums as members of other classes, in the same way inner classes are used. Another use might be a Rating enum that contains POOR, AVERAGE, GOOD, or a Grade enum of F, E, D, C, B, A.