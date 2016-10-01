---
layout: post
title:  "Intro. to Object Oriented Princiles and Design Patterns"
date:   2016-10-01 
categories: quick-reference 
---

[OO Basics](#oo-basics)  
&nbsp;&nbsp;&nbsp;&nbsp;[Abstraction](#abstraction)  
&nbsp;&nbsp;&nbsp;&nbsp;[Encapsulation](#encapsulation)  
&nbsp;&nbsp;&nbsp;&nbsp;[Polymorphism](#polymorphism)  
&nbsp;&nbsp;&nbsp;&nbsp;[Inheritance](#inheritance)  
[OO Patterns](#oo-patterns)  
&nbsp;&nbsp;&nbsp;&nbsp;[The Strategy Pattern](#strategy-pattern)  
&nbsp;&nbsp;&nbsp;&nbsp;[The Observer Pattern](#observer-pattern)  
&nbsp;&nbsp;&nbsp;&nbsp;[The Factory Pattern](#factory-pattern)  
&nbsp;&nbsp;&nbsp;&nbsp;[The Command Pattern](#command-pattern)  
&nbsp;&nbsp;&nbsp;&nbsp;[The State Pattern](#state-pattern) 
<br/><br/>

## OO Basics

#### Main Principles

1. Encapsulate what varies from what stays the same.
2. Program to an interface instead of an implementation.
3. Favor composition over inheritance.

#### Abstraction

Abstraction involves only focusing on the details that are necessary when modelling an object in a system. When abstracting, we are not concerned about the nitty-gritty implementation details, but rather, we would like to describe to the client of the object, the operation and behaviors that the given object is capable of performing (i.e. how to use it). It allows developers to better manage complexity by breaking up complex systems and allows them to focus on what the object does instead of how it does it.

Related posts:  
http://codebetter.com/raymondlewallen/2005/07/19/4-major-principles-of-object-oriented-programming/

#### Encapsulation

Encapsulation is a mechanism by which information in a class can be hidden from the client. In Java, this can be accomplished through the use of access modifiers (private, protected, default and public).

These are the advantages of making attributes and methods as least accessible as possible:  
- Since we know that it is not outide of the class, developers can have more confidence in not breaking any other part of the application when making code updates  
- It makes it easier to troubleshoot and debug code (especially in multi-threaded applications) since the scope of use is more limited  
- We can prevent clients from setting the attributes of a class to an erroneous value  

Related posts:  
http://stackoverflow.com/questions/11071407/advantage-of-set-and-get-methods-vs-public-variable

#### Polymorphism

Polymorphism in code is the ability to replace the object of a supertype with an object of a subtype. That is to say, when we are declaring variables, defining the return type of a method, or specifiying the arguments of a method, we should always use the supertype (i.e. program to an interface) so that we have more flexibility whenever we want to change something. If we always program to a supertype, whenever there is a change in the implementation, it will be transparent to the client, and there will be no changes that are required on their part.

Advantages:  
- It allows your code to be unit tested by allowing you to mock the dependency and then inject it into the class  
- It doesn't require clients to update their code whenever the implementation changes. For example, suppose you are working on a mesaging application and you want to persist the message before sending it to the user. There are different mechanisms of persisting messages - you could store it in memory, save it to the filesystem, or store it on disk. If all of the storage implementations  are coded to a common storage interface, the client code can remain unchanged whenever you decide to add or change the storage mechanism. Furthermore it ensures that your code abides by the open-closed principle, which states that an object should be open for extension but closed for modification.  
- It allows the system to be developed independently from the clients that use it.  

Related posts:  
https://sourcemaking.com/refactoring/replace-conditional-with-polymorphism  
 
#### Inheritance

Inheritance is the ability to extend a class so that we can reuse the attributes and behavior of the parent class. It's main purpose is to promote code reuse and prevenpt duplication. It's an essential concept in OO programming, but it is not always beneficial to use inheritance. One reason why is because, inheritance violates encapsusulation since the subclass depends on the implementation details of its superclass, and due to this, if there is an implementation change in the superclass, there is a risk that the subclass may break. If possible, it's advisable to use composition in place of inheritance.

<br/>

## Design Patterns

### Strategy Pattern 

#### Definition: 
Defines a family of algorithms (behaviors), encapsulates each one, and makes them interchangeable. Strategy lets the algorithms (behaviors) vary independenttly from the clients that use them.

#### When to use it:
