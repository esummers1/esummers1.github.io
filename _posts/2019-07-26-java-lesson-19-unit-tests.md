---
bg: "tools2.jpg"
layout: post
title:  "Java Lesson 19 - Unit Tests"
crawlertitle: "Java Lesson 19"
summary: "Unit Tests"
date:   2019-07-26 12:00:00 +0000
categories: posts
tags: ['java']
author: Eddie Summers
---

Testing a program - i.e. checking that it both works correctly and has all the capabilities it should - is of utmost importance, especially in professional development. Tests range from the most broad level (manual testing) to the finest (unit testing of individual functions). We will discuss automated unit and integration tests.

Most languages have libraries you can use to run automated unit tests on your programs. Java has the JUnit framework, which provides the ability to run classes as test classes, and provides various tools for setting up your tests and performing assertions. An assertion is the basic unit of the unit test - you assert that some condition is true, and the test fails if it is not.

In theory, all behaviours of a program *should* be covered by unit tests. In practice, at least in Java, there is no good way to test private methods. This means that tests should test a class's ability to **honour its contract**, rather than testing all its methods individually. If you find yourself in a position where you want to test private methods, you may need to rethink your design.

## JUnit

To get JUnit up and running, you will need to add it to your project as a dependency. This can usually be done fairly easily - it will be best to just google how to do it in your IDE of choice. Here is a skeleton JUnit test class:

{% highlight java %}
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.Assertions.*;

class BasicTest {

    private Object someObject;

    @Before
    private static void setUp() {
        someObject = new Something();
    }

    @Test
    public void testSomething() {
        Assertions.assertNotEquals(null, someObject);
    }

    @Test
    public void testSomethingElse() {
        Assertions.assertEquals(1, 2 - 1);
    }
}
{% endhighlight %}

The `@Before` annotation tells JUnit to run this method before each `@Test` method. The `@Test` annotation tells it that the following method should be executed when this class is executed in test context. There are other time-hook annotations e.g. `@BeforeClass`, `@After`, and so on.

JUnit's Assertions class will give you many different kinds of assertions. The basic few are `assert` (for a boolean condition), `assertEquals` (two compare two conditions), and `assertNotEquals` (to negatively compare two conditions).

## Approach

It's a good idea to describe the scenario and expected result in the test method name. For example, if asserting that a calculator should give you some kind of error when you try to divide by zero, you could name the method `testThrowsErrorWhenDivideByZero` or something similar.

Your goal should be to try to exercise every possible behaviour of the object or component under test. Ideally this would include covering all logical paths within it, but this is not always practical.

Having good test coverage of your code means you can make changes with impunity - you can be confident things aren't broken if the tests are good and they still pass.

## Other Kinds of Tests

There are other kinds of automated tests besides unit tests - integration tests are automated tests running in the same codebase which check how different components of a large application work together. API tests (we'll come on to APIs later) assert that a service that exposes some endpoints for other programs to make requests to reacts to requests in an expected manner.

In web projects, there are often automated UI tests - based in a separate repo - which pretend to be a user performing various actions in the system.