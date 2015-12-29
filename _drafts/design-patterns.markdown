---
layout: post
title:  "Main points in Head First Design Patterns"
date:   2015-12-28 12:52:23
categories: quick-reference 
---

1. [OO Basics](#oo-basics)  
1.1 [Abstraction](#abstraction)  
1.2 [Encapsulation](#encapsulation)  
1.3 [Polymorphism](#polymorphism)  
1.4 [Inheritance](#inheritance)  
2. [OO Principles](#oo-principles)
3. [OO Patterns](#oo-patterns)  
3.1 [The Strategy Pattern](#strategy-pattern)  
3.2 [The Observer Pattern](#observer-pattern)  
3.3 [The Decorator Pattern](#decorator-pattern)  
3.4 [The Factory Pattern](#factory-pattern)  
3.5 [The Command Pattern](#command-pattern)  
3.6 [The Template Method Pattern](#template-method-pattern)  
3.7 [The State Pattern](#state-pattern) 
3.8 [The Builder Pattern](#builder-pattern) 
<br/><br/>



## OO Basics

#### Abstraction

Abstraction involves only focusing on the details that are necessary when modelling an object in a system. When abstracting, we are not concerned about the nitty-gritty implementation details, but rather, we would like to describe to the client of the object, the operation and behaviors that the given object is capable of performing (i.e. how to use it). 

E.g. 1: Suppose you are modelling an employee. You can have many different types of employees: full-time, part-time, consultant, student etc. The behavior of an Employee object can vary from one type to another. For example, there can be a restriction on the number of hours that the employee can work, the formula for their pay calcuation may also vary, or the number of vacation days that they are entitled to may be different. If you are abstracting the Employee object however, you should not get caught up in theses implementation details, and just look to provide the methods that are common to all employee types. So, we would provide methods like: <code>getMaxHoursEmplIsAllowedToWork()</code>, <code>calculatePay()</code>, <code>getVacationDaysEmplIsEntitledTo()</code>, and the child classes would then be responsible for writing the implementation details later on.


#### Encapsulation

Encapsulation (also known as data hiding) is a mechanism by which information in an object can be hidden from the client. In Java, this mechanism can be accomplished through the use of access modifiers (<code>private</code>, <code>protected</code>, <code>default</code> and <code>public</code>). The advantage of making attributes and methods <code>private</code> is that we can change the implementation without having to worry about breaking the client code and it also gives us more control over the state of the object. For this reason, it's always better to make an attribute or method as least accessible as possible.

E.g. 2: Suppose you are writting a class for a remote-controlled car, and suppose you make the <code>speed</code> field (which represents the current speed of the car) public. If the client (remote control program) for some reason updates the <code>speed</code> field while the car is running, invocation of the car's <code>accelarate()</code> and <code>decelerate()</code> methods may result in unexpected behaviors.


#### Polymorphism

Polymorphism in code is the ability to replace the object of a supertype with an object of a subtype. That is to say, when we are declaring variables, defining the return type of a method, or specifiying the arguments of a method, we should always use the supertype (i.e. program to an interface) so that we have more flexibility whenever we want to change something. If we always program to a supertype, whenever there is a change in the implementation, it will be transparent to the client, and there will be no changes that are required on their part.

<font color="red">TODO: ADD EXAMPLES</font>


#### Inheritance

Inheritance is the ability to extend a class so that we can reuse the attributes and behavior of the parent class. It's main purpose is to promote code reuse and prevent duplication. It's an essential concept in OO programming, but it is not always beneficial to use inheritance. One reason why is because, inheritance violates encapsusulation since the subclass depends on the implementation details of its superclass, and due to this, if there is an implementation change in the superclass, there is a risk that the subclass may break. If possible, it's advisable to use composition in place of inheritance.

<font color="red">TODO: ADD EXAMPLES</font>
<br/><br/>




## OO Principles

1. Encapsulate what varies from what stays the same.
2. Program to an interface instead of an implementation.
3. Favor composition over inheritance.

<br/><br/>




## OO Patterns  

#### Strategy Pattern  

<b>Definition:</b> Defines a family of algorithms, encapsulates each one, and makes them interchangeable. Strategy lets the algorithms vary independently from the clients that use them.

The example that the book uses to show how the pattern is used is a game that simulates a duck pond, where there are various duck species that are swimming around and making noise.

Here are the classes that are there to begin with:

{%highlight java%}
class Duck {
	quack()
	swim()
	display() // This method is abstract
}

class MallardDuck extends Duck {
	display() { /* Looks like a mallard duck */ }
}

class RedheadDuck extends Duck {
	display() { /* Looks like a red head */ }
}

class RubberDuck extends Duck {
	quack() { /* Squeak */ }
	display() { /* Looks like a rubber duck */ }
}
{%endhighlight%}

<b> There is a requirement which comes in that says the pond should have flying ducks. <b/>

The first approach that is taken is to add a fly method in the duck class, which all of the subclasses will inherent. The problem with this is that there are some ducks which should not be able to fly (e.g. RubberDuck) which can now fly. They consider overriding the fly method to do nothing if there is a duck that isn't expected to fly, but you'll have to override the fly method each time we add a duck that doesn't fly. The same applies for quack behavior as well.

{%highlight java%}
class Duck {
	quack()
	swim()
	fly()
	display() // This method is abstract
}

class MallardDuck extends Duck {
	display() { /* Looks like a mallard duck */ }
}

class RedheadDuck extends Duck {
	display() { /* Looks like a red head */ }
}

class RubberDuck extends Duck {
	quack() { /* Squeak */ }
	display() { /* Looks like a rubber duck */ }
	fly() { /* Do nothing */ } 
}
{%endhighlight%}

The second approach that is taken is to make two interfaces: Flyable and Quakable, and these two interfaces will contain the fly() and quak() methods respectively. This again is not a good idea, because all of the duck classes will have to implement these two methods, even though their implementation may only vary slightly across the ducks (i.e. it will lead to a lot of duplicate code.)

{%highlight java%}
class Duck {
	quack()
	swim()
	fly()
	display() // This method is abstract
}

interface Flyable {
	fly()
}

interface Quakable {
	quack()
}

class MallardDuck extends Duck implements Flyable, Quakable {
	display() { /* Looks like a mallard duck */ }
	fly() {  ... }
	quack() {  ...  }
}

class RedheadDuck extends Duck implements Flyable, Quakable{
	display() { /* Looks like a red head */ }
	fly() {  ... }
	quack() { ... }
}

class RubberDuck extends Duck {
	quack() { /* Squeak */ }
	display() { /* Looks like a rubber duck */ }
}

class DecoyDuck extends Duck {
	display() { /* Looks like a decoy duck */ }
}
{%endhighlight%}

The end solution involves extracting the fly() and quack() behaviors into an interface into an interface of their own, and then there we be a set of classes that will implement these behaviors. The Duck class will then have two methods that will allow behaviors to be assigned and changed at runtime. This is advantageous to the previous two choices because it is more flexible: in the previous two cases, the behavior came from a concrete implementation (either in the superclass or the subcless itself), and because of this we are locked into a specific implementation and there is no room for changing the behavior.

Here is how the final classes look like:

{%highlight java%}
interface FlyBehavior {
	fly()
}

class FlyWithWings {
	fly() { /* Implements duck flying */ }
}

class FlyNoWay {
	fly() { /* do nothing */ }
}

interface QuackBehavior {
	quack() 
}

class Quack {
	quack() { /* Implements duck quacking */ }
}

class Squeak {
	quack() { /* Implements ducks squeaking */ }
}

class Duck {
	FlyBehavior flyBehavior;
	QuackBehavior quackBehavior;

	display()
	perfromQuack()
	performFly()
	setFlyBehavior()
	setQuackBehavior()	
}

class MallardDuck extends Duck {
	display() { /* Looks like a mallard duck */ }
}

// ... Other concrete duck classes
{%endhighlight%}