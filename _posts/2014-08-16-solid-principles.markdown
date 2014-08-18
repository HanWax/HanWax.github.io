---
layout: post
title:  "SOLID Principles"
date:   2014-08-16 22:10:00
analytics: true
comments: true
---

The SOLID principles lie at the heart of object-oriented design and exist to help you to design software that is robust and limited in bugs. My favourite principle is the single responsibility principle because I find it the most intuitive. I am still getting to grips with the practical implications of some of the principles, in particular the dependency inversion principle, and trying to incorporate them into the design of the projects. If anyone has any useful examples I would really appreciate hearing your thoughts!

###Single responsibility principle

The single responsibility principle states that each object should have one responsibility only, and that responsibility should be entirely encapsulated by that class. This doesn't mean that each class contains only one method, but that all methods are connected to the primary function of the class. If we think about our Battleships game, we gave our cell class the single responsibility of knowing its status. This included knowing whether it had been previously attacked or not, and whether it was occupied or empty. The idea behind this is that when a class has more than one responsibility, the likelihood of change to that class occurring is relatively high. Every time a class is changed, the risk of introducing bugs increase. In our design we can encourage tight cohesion but loose coupling by sticking to the SRP. Tight cohesion relates to how strongly related and focused the responsibilities are. Coupling is the degree to which one class/module relies on an other. If there is tight coupling, changes to one part of the programme are more likely to affect the behaviour of other parts in unexpected ways and more bugs will be introduced. 

###Open/closed principle

The open/closed principle states that software entities should be open for extension but close for modificiation. The closed part of the principle refers to the fact that once a class is pushed to development, and has been tested, it should only be modified to deal with bugs. However, the open part refers to the fact that a class can be open for extension to introduce new functionality. This should only be done by adding new code to the existing code base. This reduces risk of new bugs being introduced by limiting changes made to existing code. 

###Liskov substitution principle

Liskov substitution principle states that subtypes must be substitutable for their base types. This principle goes to the heart of any class inheritance chain. If you write a class that uses a parameter or variable of some base class, then you should be able to pass an instance of some descendant class into the base class and the behaviour should remain exactly the same. This can be illustrated with a simple example. Let's say we have a base class of a bird, that has a method that allows it to fly. Then we create a descendant duck class. The duck class has a method fly that overrides that method pertaining to how birds fly. Then an ostrich sub-class is created. Although an ostrich instance is substitutable for a bird instance - its introduction causes breaking change to every instance where a bird is asked to fly. It breaks the Liskov substitution principle because it introduces new behaviour into existing code by writing a descendant of the base class. To solve this, one might suggest the rewriting of the base class, our bird class. However, if you were to do this you If you would be breaking the Open/Close principle.

###Interface segregation principle

This principle states that classes that implement interfaces, should not be forced to implement methods that they do not use. Often when you create a class with a large number of methods and properties, the class is used by other types that only require access to one or two such methods. The classes become more tightly coupled as the number of methods they incorporate grows. In accordance with the ISP, large should classes implement multiple smaller interfaces that group functions according to their usage. 

###Dependency inversion principle

This principle states that high-level modules should not depend upon low-level modules, both should depend upon abstractions. Unlike what many people would assume, this principle inverts the idea that higher-level components should be dependent upon lower-level modules. Instead, both of them should depend upon the same abstraction.  Abstractions should not depend on details, but details should depend upon abstractions. 

Hannah
