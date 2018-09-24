---
layout: post
title: "Point out to Fluent Builder"
excerpt: "Whenever you have a domain object, data transfer object, parameter object or any other object that can’t be instantiated with constructor parameters only, you need to create a builder for its class."
date: 2018-09-24
tags: 
    - csharp
    - design patterns
    - builder pattern
    - best practices
categories: 
    - design patterns
share: true
comments: true
author: Żaba
---

<figure class="align-center">
  <a href="#"><img src="{{ '/images/kevin-jarrett-561802-unsplash.jpg' | absolute_url }}" alt=""></a>
  <figcaption>Photo by Kevin Jarrett on <a href="https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a></figcaption>
</figure>

# Point out to Fluent Builder

Some time ago I had occasion participated in craftsmanship training.
The main goal of the training was to improve our knowledge about design patterns, and all other stuff that we can call a good practices (including SOLID rules of course).

Our exercises relied on analyzing fragments of code (that was not really pretty), next on trying to pick up suitable pattern and finally on refactoring those fragments with chosen pattern.

When we carried out the exercise using builder pattern, one thing motivated me to make this post.
I'm not going to describe here in details the builder pattern so just for a quick reminder I put here qoute from the gang of four book that describe the purpose of builder pattern.

> Separate the construction of a complex object from its representation so that the same construction process can create different representation.  
> <footer>Design Patterns: Elements of Reusable Object-Oriented Software</footer>

To be honest I had only two occasions to implement and use fluent builder pattern, below I present how it could looks like.

Lets imagine that **RecruitmentApplication** is some kind of large contract exposes by an external service belonging to university and it's used during recruitment process for studies

Going further lets picture that some day we could be forced to integrate with this service. As we can see below it could be a really large flat class that's include every information that might be need during recruitment process to university.


<script src="https://gist.github.com/Zabaa/585577b4987a9feace8a08f451126e2b.js?file=RecruitmentApplication.cs"></script>

 We can use fluent builder pattern here to simplify creation of objects like RecruitmentApplication.

<script src="https://gist.github.com/Zabaa/585577b4987a9feace8a08f451126e2b.js?file=FirstApplicationBuilder.cs"></script>


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

I was also used this approach in my implementations of Builder pattern. I've thought it was good approach, create object in construcor, fill it using fluent manner and return after calling **Build** method. But during exercise my instructor after reviewing my example gave me valuable tip. What if I would like to run **Build** method several time ?

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

So how can it be implemented correctly ? 

I can move object initialized to **Build** method and create right amount of private fields for storing values from fluent methods.
I realize that's increase amount of code, but with this manner I'm sure that my builder will always create for me a new object. Nice!
Of course below you can find how it could looks like after a small refactoring.

<script src="https://gist.github.com/Zabaa/585577b4987a9feace8a08f451126e2b.js?file=ApplicationBuilder.cs"></script>