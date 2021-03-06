---
layout: post
title:  "Object-oriented Programming"
date:   2014-08-16 22:00:00
analytics: true
comments: true
---

Oracle defines object-oriented programming as a method of programming based on a hierarchy of classes, and well-defined and cooperating objects. A class is a structure that models the data and the methods that can be called on that model. Relationships between objects can be created and objects can inherit characteristics from other objects. A principal advantage of object-oriented programming is that this design enables developers to create modules and classes that do not need to be changed when a new type of object is added. A new object that inherits many of features of an existing object can simply be created. This makes the programme easier to modify without breaking and or having to rebuild it in its entirety. 

I found this concept fairly hard to get my head around at first. So I thought it would be best to have a look at an example of object-oriented programming in the wild. 

The first step that we are going to take is writing out a description of the software programme. This will help us to identify what classes our model is going to contain. One of the first OOP projects we worked on was building a Battleships programme, so I'll use this as a starting point. 

###Our description of the game:

"Battleships is a two **player** **game**. Each player deploys 5 **ships** on a 10 x 10 **grid**. Each **cell** has a unique grid reference. Each player takes *turns* to call out a grid reference and the other players confirms whether it is a *‘hit’* or *‘miss’* if a ship is at that grid reference or not. The attacking players marks the ‘hit’ or ‘miss’ on their tracking grid. The defending player marks ‘hit’ or ‘miss’ on their primary grid. Players alternate turns. When every cell that comprises one ship has been ‘hit’, the defending player declares it *sunk*. When a player sinks all their opponent’s ships they *win* and the game ends.""

The first job is to highlight the nouns and verbs in the descriptions. The nouns will form the basis of the classes in our model, whilst the verbs describe the responsibility that each class has. In extreme-programming class-responsibility-collaboration cards are used as a brainstorming tool. Each class is written on an index card. Then for each class, the responsibilities of that class along with the collaborators are recorded. As you can see from the description of our battleships game, we highlighted our player as a noun, meaning that we should make it into a class. We then should think about what responsibilities our player has. For example, our player can be responsibile for deploying ships to the grid. It can also be responsible for possessing a grid. In these scenarios, the collaborators involved would be the ship and the grid respectively.

When working on this project in a team of four, we soon discovered that there are any number of ways to model the data and to divvy up the various responsibilities! Whilst we made many mistakes, we learnt several key lessons. Firstly, having the discussion about how to model the programme is an extremely useful process, but this does not mean that the design should be set in stone from the outset. We encountered places where other models would have worked better, and we adapted our original description to fit those requirements. Secondly, the more classes and object-oriented the programme is, the easier it is to model. In our original discussion we had decided that 'hit' and 'miss' were attributes that belonged to our cell class. However, as we were writing the programme, it became clear that having individual 'hit cell' and 'miss cell' classes made our game easier to play and gave way to a better design. 

There are five guiding principles, known as the SOLID principles, that help developers to model their software in a well designed object-oriented manner that allows for maximum flexibility of the code base whilst minimising bugs. 

These are:

1. Single responsibility principle
2. Open/closed principle
3. Liskov substitution principle
4. Interface segregation principle
5. Dependency inversion principle

But these deserve a blog post of their own. 

To summarise:

1. Object-oriented programming helps to prevent rigid, immobile and inflexible designs. 

2. Object-oriented programming and design involves using classes as models of real-world objects. Objects have both states(data) and behaviour (methods).

3. Object-oriented programming is about managing the interactivity and dependencies between various objects. The objects interact by sending and receiving messages to and from each other.  

Hannah 