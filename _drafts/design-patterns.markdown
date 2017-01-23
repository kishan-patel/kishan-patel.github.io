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



### Behavioral Patterns

<b>Name:</b> Strategy  

<b>Overview:</b>  

![Strategy UML Diagram](/assets/strategy.png){:.center-image}

- The strategy pattern allows you to encapsulate algorithms and makes them interchangeable.  
- It decouples the decision of which strategy to use from the code that executes it.  
- It helps ensure that the code abides by the open-closed principle, because we just need to change the strategy and not the individual methods whenever we need to use a different algorithm.

<b>Examples:</b>  

- Message storage in a chat application: When a message is received from a particular user, it may be processed in cache, in memory, on disk or in a database. Instead of having numerous if/else statments at various locations in the code, we can let the strategy handle the operations (storage, retrieval, update and deletion), thus alleviating the need to revisit that code whenever we need to change the algorithm.

<br/>

<b>Name:</b> Decorator

<b>Overview:</b>

![Strategy UML Diagram](/assets/decorator.png){:.center-image}

- Provides an Alternative to subclassing for extending functionality.
- One of the drawbacks is that it can lead to many small objects in our design.

<b>Examples:</b>

- The InputStream classes in the Java I/O package: The FileInputStream class is decorated by the BufferedInputStream class (improves performance by buffering data and adds ability to read lines) which is further decorated by the LineNumberInputStream class (adds ability to keep track of line numbers as data is read).

