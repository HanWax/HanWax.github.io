---
layout: post
title:  "Object-oriented Programming"
date:   2014-08-15 23:00:00
---

Oracle defines object-oriented programming as a method of programming based on a hierarchy of classes, and well-defined and cooperating objects. A class is a structure that models the data and the methods that can be called on that model. Relationships between objects can be created and objects can inherit characteristics from other objects. A principal advantage of object-oriented programming is that this design enables developers to create modules and classes that do not need to be changed when a new type of object is added. A new object that inherits many of features of an existing object can simply be created. This makes the programme easier to modify without breaking and or having to rebuild it in its entirety. 

I found this concept fairly hard to get my head around until I started building projects using OOP principles. So let's have a look at an example in the wild. The first step in creating a well-designed OOP software project lies in writing out a description of the software programme that we want to create in order to identify what classes we are going to need. One of the first OOP projects we worked on was building a Battleships programme, so I'll use this as a starting point. 

Our description of the game:

"Battleships is a two **player** **game**. Each player deploys 5 **ships** on a 10 x 10 **grid**. Each **cell** has a unique grid reference. Each player takes *turns* to call out a grid reference and the other players confirms whether it is a *‘hit’* or *‘miss’* if a ship is at that grid reference or not. The attacking players marks the ‘hit’ or ‘miss’ on their tracking grid. The defending player marks ‘hit’ or ‘miss’ on their primary grid. Players alternate turns. When every cell that comprises one ship has been ‘hit’, the defending player declares it *sunk*. When a player sinks all their opponent’s ships they *win* and the game ends.""

The first job is to highlight the nouns and verbs in the descriptions. The nouns will form the basis of the classes in your model, whilst the verbs describe the responsibility that each class has. In extreme-programming class-responsibility-collaboration cards are used as a brainstorming tool. Each class is written on an index card. Then for each class, the responsibilities of that class along with the collaborators are recorded. Therefore, with regard to the battleships programme that we were building, we had highlighted our player as a noun, thus indicating that we wanted to make our player a class of its own. We gave the player two responsibilities. The first was that the player was responsibile for deploying ships to the grid. The second responsibility of the player class was to possess a grid. The collaborators involved were the ship and the grid respectively.

As we soon discovered in our team of four, there are any number of ways to model the data and to divvy up the various responsibilities! Whilst we made many mistakes, there were several key lessons learnt. Firstly, it is a useful process to discuss how you want to model the programme, but this does not mean that the design should be set in stone from the outset. We encountered places where other models would have worked better, and we adapted our original description to fit that. Secondly, the more classes and object-oriented the programme is, the easier it was to model. In our oirignal discussion we had decided that 'hit' and 'miss' were attributes that belonged to our cell class. However, as we were writing the programme, it became clear that having individual 'hit cell' and 'miss cell' classes made our game easier to play and gave way to a better design. 

Well designed object-oriented software follows the SOLID principles:

1. Single responsibility principle
2. Open/closed principle
3. Liskov substitution principle
4. Interface segregation principle
5. Dependency inversion principle

But these deserve a blog post of their own. 

Hannah :) 