---
bg: "notre-dame.jpg"
layout: post
title:  "Java Lesson 20 - Project Structure"
crawlertitle: "Java Lesson 20"
summary: "Project Structure"
date:   2019-07-26 14:00:00 +0000
categories: posts
tags: ['java']
author: Eddie Summers
---

Java projects consist of **packages**. A package is represented in your filesystem as a folder, but from the compiler's point of view represents a node on the classpath. This is the overall structure of the project, required for compilation.

Recall that in lesson 10 we discussed package-private scope - this means that any file in the same package can see this member.

It is a loosely-held convention that your source package for all production code is `src`, though this may vary if you are using a particular framework e.g. Spring. Here is an example from one of my early programming projects, [Orbit Simulator](https://github.com/esummers1/orbit-simulator)

```
src
    |-- entities
        |-- Body.java
        |-- Entity.java
        |-- EntityRenderer.java
        |-- EntityShooter.java
        |-- EntityShot.java
    |-- main
        |-- Camera.java
        |-- Display.java
        |-- InputProvider.java
        |-- MyPanel.java
        |-- Scenario.java
        |-- ScenarioRepository.java
        |-- Simulation.java
    |-- physics
        |-- BearingVector.java
        |-- Geometry.java
        |-- Physics.java
        |-- Position.java
        |-- XYVector.java
```

Note how related classes are grouped into packages. Also, the full "address" of, say, `Body.java` is `src.entities.Body`. Classes in these packages will include a `package` declaration at the top, e.g. `package entities` for `Body.java`. Since `src` is considered the sources root, addresses are only specified from the next level down.

Classes can import from elsewhere in the project, provided the class is accessible. For example, in `Camera.java`, we have at the top:

```
package main;

import physics.Position;

...
```

This is because the Position class is public and has public members that the Camera class depends on.

You will probably want a separate test sources root, e.g. `test`, which you can designate as such in your IDE/classpath.