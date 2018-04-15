---
layout: post
title: "Point out to Fluent Builder"
excerpt: "Whenever you have a domain object, data transfer object, parameter object or any other object that can’t be instantiated with constructor parameters only, you need to create a builder for its class."
date: 2018-02-03
tags: [csharp, design patterns, builder pattern]
categories: design patterns
share: true
comments: true
author: Żaba
image:
  path: /images/kevin-jarrett-561802-unsplash.jpg
  caption: "Photo by Kevin Jarrett on [Unsplash](https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)"
---

<figure class="align-center">
  <a href="#"><img src="{{ '//images/kevin-jarrett-561802-unsplash.jpg' | absolute_url }}" alt=""></a>
  <figcaption>Look at 580 x 300 <a href="#">getting some</a> love.</figcaption>
</figure>

# Point out to Fluent Builder

This week I had occasion participated in training organized by company which I provide my services.
The main goal of training was improve our knowledge about design patterns, and all other stuff that we can call a good practices.

Our exercises relied on analyzing fragments of code (that was not really pretty), next on trying to pick up suitable pattern and finally on refactoring those fragments with chosen pattern.

When we stopped at the exercise with builder pattern, one thing motivated me to make this post.
To be honest I had only two occasions to implement and use fluent builder pattern, and it's look something like that

<script src="https://gist.github.com/Zabaa/585577b4987a9feace8a08f451126e2b.js"></script>

Lets imagine that **RecruitmentApplication** is some kind of large contract exhibited by an external service belonging to some university. As we can see it could be really large flat structure contract that's include every information which is gonna be need during recruitment process to university. We can use fluent builder pattern here to simplify creating such an object.

But back to my training, in many posts about fluent builder I noticed that object returned from builder was initialized in Builder constructor like that:

```csharp
public ApplicationBuilder CreateApplication(string name, string sureName, DateTime birthDate)
{
    var application = new RecruitmentApplication();
    application.Name = name;
    application.SureName = sureName;
    application.BirthDate = birthDate;

    return this;
}
```

I also initialized object like that in my examples. I've thought it was good approach, create object in constructor, fill it witch fluent manner and return after calling **Build** method.
But during training my instructor after watching my example gave me valuable attention. What if I would like to run **Build** method several time ?

```csharp
var builder = new ApplicationBuilder();
var application = builder
    .CreateApplication("Zaba", "Zul", new DateTime(1990, 9, 2))
    .WithDormitoryAssignment("Filon", "Kilinskiego 11")
    .WithRepetition("Electronics", 10, 10, 550)
    .WithRepetition("Object Oriented Programming", 20, 15, 850)
    .Build();
var secondApplication = builder.Build();
var thirdApplication = builder.Build();
```

In above example each time builder returns reference to exactly the same object. And that's not correct. Builder should return new object every time we call **Build** method.
So how can it be implemented correctly ? I can move object initialized to **Build** method and create right amount of private fields for storing values from fluent methods.
I realize that's increase amount of code lines, but with this manner I'm sure that my builder gives me a brand new object. Nice!

<script src="https://gist.github.com/Zabaa/585577b4987a9feace8a08f451126e2b.js"></script>