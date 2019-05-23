---
bg: "laptop.jpg"
layout: post
title:  "Java Lesson 4 - Collections"
crawlertitle: "Java Lesson 4"
summary: "Collections"
date:   2019-05-17 20:00:00 +0000
categories: posts
tags: ['java']
author: Eddie Summers
---

So far we've seen two ways to store information in our programs - **primitives** and **objects**. If we want to store groups of these pieces of data, we need to use collections.

A collection is a data structure that allows storage, retrieval and manipulation of other items. There are a few important kinds of collections we need to cover. Each one is most useful for different things.

## Arrays

Arrays are collections of data that are contiguous in memory - this means that when we instantiate an array, we reserve a chunk of memory for it to occupy. This means that we can access any element extremely quickly (because its location can be easily calculated by the computer), but it means the array is of fixed size. Arrays can hold any type, but all elements must be of the same type.

{% highlight java %}
// Declare and instantiate in one line, including the array's length
int[] numbers = new int[10];

// Assignment
numbers[0] = 20;

// Assignment from variable
int i = 5;
numbers[1] = i;

// Retrieval
System.out.println("The first element is: " + numbers[0]);

// Overwrite
numbers[0] = 17;

// Inline declaration, instantiation and initialization
int[] moreNumbers = {10, 5, 7, 11, 22};
{% endhighlight %}

Traversing (iterating through) arrays is very fast, because accessing an element by its index is very fast. We can do this in a couple of ways:

{% highlight java %}
int[] numbers = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};

// Print every element in the array by index
// N.B. you access an array's length using its ".length" property
for (int i = 0; i < numbers.length; i++) {
    System.out.println(numbers[i]);
}

// Implicitly use an iterator to go through by element - "i" is in each pass
// through the loop a copy of the element at the current position.
for (int i : numbers) {
    System.out.println(i);
}
{% endhighlight %}

Note that arrays' indices begin at 0 - an array of length 10 ends at index 9.

## Lists

Lists can come in many forms, but the most common implementation is a linked list - this is where each item in memory stores a reference to the _next_ element. In order to access element 10 of a linked list, the computer must go to the first one (whose position is known), then follow through each of the links until it reaches the tenth element. This means that long lists are much slower to traverse than arrays, but their length is dynamic.

List is an interface, so to actually create a list you'll need to choose a concrete implementation (more on this later). The default choice is ArrayList.

{% highlight java %}
// Declaration and instantiation
List strings = new ArrayList();

// Initialization
strings.add("Hello");
strings.add(" world");

// Retrieval by index
String hello = strings.get(0);

// Traversal using for-each
for (String string : strings) {
    System.out.print(string);
}
{% endhighlight %}

You can access a list's size using its `.size()` method. This is also true for all the collections to follow.

There's a little more to do here, though - Lists store their objects without type information for backwards-compatibility reasons. This means that our `strings` list above does not actually guarantee its contents are Strings. In order to read its contents and use them _as Strings_, i.e. use behaviour that String has more than Object (the base class of all classes in Java - again, more on this later), we use generics.

We'll cover this later in more detail, but what this basically means is that we save ourselves from having to do an explicit `(String)` cast every time we retrieve a value from our Strings list (as Java takes care of it for us), and it also ensures that if we try to add some other object to the list, which would cause an error at runtime when we tried to cast it to String, we'll instead get a compilation error. We use the diamond brackets:

{% highlight java %}
// Declaration and instantiation, specifying the type in our List generic
List<String> strings = new ArrayList<>();

// Would not compile, as an Integer is not a String
strings.add(new Integer(5));
{% endhighlight %}

You'll find yourself using Lists a lot - they're useful for many things. The only thing to watch out for with them is to avoid doing direct for-loop traversals; if you access every index in a 100-item list directly, the computer will have to take 1 step the first time, 2 steps the second time, all the way up to 100. If you use the (much more convenient) for-each syntax, Java cleverly uses an Iterator behind the scenes to remember its position in the List between each pass through the loop.

## Sets

Arrays and Lists are ordered collections - you are guaranteed to get their contents back in the same order you added them if you access their indices in order.

Sometimes you might not care what order you get things back in, and you may also want to ensure that no two elements in a collection are the same. For example, a grouping of unique ID numbers. For this we use the Set. The default implementation of this interface is HashSet.

{% highlight java %}
Set<Integer> uniqueNumbers = new HashSet<Integer>();

uniqueNumbers.add(new Integer(8));
uniqueNumbers.add(new Integer(9));

// Won't work - the Integer object will not be added
uniqueNumbers.add(new Integer(8));

// Will print every element in the Set, in an unpredictable order
for (Integer num : uniqueNumbers) {
    System.out.println(num);
}
{% endhighlight %}

## Maps

Sets lead us nicely into Maps. A Map is a collection of key-value pairs. They are called dictionaries in other languages - imagine a dictionary where the definition of each word was indexed not by the word itself but by number! You'd need to check through thousands of words to find the definition you wanted.

The actual implementation of the default Java map choice - the HashMap - is that the key of each pair is "hashed" using a function that produces some value. We'll come back to hashing later. Just suffice it to say that the result of this hash function tells the computer where exactly to store the value object of the pair - this way, when some key is provided to retrieve a value from the table, it can be hashed and that address's contents returned.

A Map's keys are like a Set - they must be unique. If you add a pair of values using a duplicate key, your new value will overwrite the old one, and the old one will be lost.

{% highlight java %}
Map<String, String> phoneNumbersByName = new HashMap<String, String>();

phoneNumbersByName.put("Mr Plow", "KL5-3226");
phoneNumbersByName.put("Mr Burns", "(636) 555-0113");
phoneNumbersByName.put("Mr Simpson", "(939) 555-0113");

// Retrieval
System.out.println(phoneNumbersByName.get("Mr Plow"));

// Traversal by key
for (String name : phoneNumbersByName.keySet()) {
    // do something with phoneNumbersByName.get(name)
}

// Traversal by entry
for (Map.Entry entry : phoneNumbersByName) {
    // get key of this entry - need to cast as Map.Entry is unaware of the types
    String name = (String) entry.getKey();

    // get value of this entry - again, must cast
    String phoneNumber = (String) entry.getValue();
}
{% endhighlight %}

One of the big advantages of Maps is that retrieval using a key and hash table is almost as fast as accessing an array element by index. We also get something of the Set, with how duplicate keys are overwritten. And their length is not restricted upon instantiation, as is the case for arrays. Remember however that since a Map's keys behave like a Set, traversing all entries in a Map will not visit them in a predictable order.

We'll come back to more convenient ways to traverse and manipulate collections when we cover Lambda expressions and Streams.