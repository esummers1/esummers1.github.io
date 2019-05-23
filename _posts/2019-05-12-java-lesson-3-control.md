---
bg: "wires.jpg"
layout: post
title:  "Java Lesson 3 - Functions and Flow Control"
crawlertitle: "Java Lesson 3"
summary: "Functions and Flow Control"
date:   2019-05-12 20:00:00 +0000
categories: posts
tags: ['java']
author: Eddie Summers
---

A **function** is some set of instructions that has a name, and hence can be called. It can return a value of some kind if you like, but this is optional. **Parameters** - variables which are received by the function and inform its behaviour - can be specified, but this is also optional. A value which is passed to a function - i.e. an instance of a parameter - is called an **argument**.

You may have heard the name function used interchangeably with **method** - a method is a function that belongs to a class or object. In Java, all functions belong to a class or object, so "function" and "method" can be used interchangeably.

A function has a **signature** and a **body**:

{% highlight java %}
int addOneToNumber(int number) {    // signature
    return number + 1;              // body
}
{% endhighlight %}

In the above snippet, the first `int` is the return type of the function - it returns an integer. The function will not compile unless you provide a `return` statement that returns a literal or variable of type `int`.

After the return type (this can be any type, or `void`, meaning it returns nothing), there is the name of the function, by which it's called; then the parameters, which in this case just consists of one `int`, `number`. When the function is called, whatever name the variable has that's passed as an argument, we refer to it as `number` in the function body.

You don't have to include a `return` statement in a void function, but doing so can give you a way to control what happens in the function - if you want it to terminate early for some reason under some condition you can say `return` to abort its execution.

### Aside - Pass-by-Value

In Java, variables are passed as arguments by value. Confusingly, however, in Java the "value" of an object is actually the value of the _pointer_ to the object. This means that if you pass a primitive to a function, you're passing a copy of it - i.e. the value of the variable. However if you pass an object, you're passing a reference to the same object. If the object is modified during the function's execution, the object that was originally passed as an argument _will also_ be modified. This is not true for primitives.

## Iteration

In addition to giving a repeatable block of code a name (by making it a function), we can use loops to **iterate** over a series of instructions according to some conditions. There are two kinds of loop we'll look at for now.

### While Loop

A `while` loop repeats its contents so long as the condition in its declaration evaluates to true. If the condition is false, the body is not executed again and the code execution resumes after the loop.

{% highlight java %}
// Will print the numbers 0 - 9
int counter = 0;

while (counter < 10) {
    System.out.println(counter);
    counter++;
}
{% endhighlight %}

### For Loop

A `for` loop repeats a given number of times, according to conditions set up in its declaration. The declaration consists of three parts - the declaration of the counter variable (this is optional - you can use a variable that exists outside the loop, if you want), the condition that must be true for the loop to run again, and what to do each pass through the loop. The classic case is something like this:

{% highlight java %}
// Will print the numbers 0 - 9
for (int i = 0; i < 10; i++) {
    System.out.println(i);
}
{% endhighlight %}

`i` will keep the "index" of this pass through the loop, so it will be the numbers 0 through 9 in order in this example.

### Loop Interruption

If you want to break out of a loop at some point, you can use the `break` statement. This will jump out of the loop and continue from the next line after it. If this is within a loop that is inside another loop, `break` will just leave the innermost loop.

If you want to stop executing the loop's body and skip straight to the start of the next iteration (provided the condition remains true), you can use the `continue` statement. This behaves the same way in relation to nested loops as the `break` statement.