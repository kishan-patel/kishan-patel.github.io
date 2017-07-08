---
layout: post
title: "Design Patterns"
date: 2017-07-01
---

## Creational Patterns 

### The Builder Pattern 

### The Abstract Factory Pattern 

### The Singleton Pattern 

## Structural Patterns 

### The Composite Pattern 

#### <u>Summary</u>

The Composite pattern is useful when you want to model a tree-like-structure. There are two type of objects: <code>Composite</code> and <code>Leaf</code>. <code>Composite</code> can contain other <code>Composite</code> objects or <code>Leaf</code> objects. <code>Leaf</code> objects on the other hand are simple, and do not contain other objects. Both <code>Composite</code> and <code>Leaf</code> objects extend the abstract <code>Component</code> class.

#### <u>Example</u>

### The Decorator Pattern 

### The Flyweight Pattern 

### The Proxy Pattern 

### The Adapter Pattern 

### The Bridge Pattern 

### The Facade Pattern 

## Behavioral Pattern 

### The Command Pattern 

### The Visitor Pattern 

#### <u>Summary</u>

The Visitor Pattern is useful when you have a fairly stable structure of objects and you need to perform a set of operations on those objects. The objects performing the operation implement the <code>Visitor</code> interface, and those objects on which the operation is being performed on, implement the <code>Visitable</code> interface. It promotes the open/closed principle because the set of objects don't need to be modified each time there is a new operation that is added.  

The drawback to this pattern is that, whenever there is a new class implementing the <code>Visitable</code> interface that is added to the structure, all of the classes implementing the <code>Visitor</code> interface will need to be updated.

#### <u>Example</u>

<div class="plantUml">
{% plantuml %}
Interface Visitable {
  void accept(Visitor visitor)
}
Class Architect {
}
Class ProductOwner {
}
Class Manager {
}
Class Tester {
}
Class Developer {
}

Interface Visitor {
  void visit(Architect architect)
  void visit(ProductOwner productOwner)
  void visit(Manager manager)
  void visit(Tester tester)
  void visit(Developer developer)
}
Class RoleVisitor {
}
Class ExperienceVisitor {
}

Visitable <|.. Architect
Visitable <|.. ProductOwner
Visitable <|.. Manager
Visitable <|.. Tester
Visitable <|.. Developer
Visitor <|... RoleVisitor
Visitor <|... ExperienceVisitor
note right of Visitable
void accept(Visitor visitor) {
    visitor.visit(this);
}
end note
note bottom of RoleVisitor
void visit(Architect architect) {
    System.out.println("Decides on architecture.");
}

void visit(ProductOwner productOwner) {
    System.out.prinln("Translates business requirements.");
}

void visit(Manager manager) {
    System.out.prinln("Helps remove roadblocks.");
}

void visit(Tester tester) {
    System.out.println("Tests the code.");
}

void visit(Developer developer) {
    System.out.println("Writes the code.");
}
end note
note bottom of ExperienceVisitor
void visit(Architect architect) {
    System.out.println("25+ years of required.");
}

void visit(ProductOwner productOwner) {
    System.out.prinln("10+ years of experience required.");
}

void visit(Manager manager) {
    System.out.prinln("10+ years of experience required.");
}

void visit(Tester tester) {
    System.out.println("No experience required.");
}

void visit(Developer developer) {
    System.out.println("No experience required.");
}
end note
note as N1
Client:

RoleVisitor roleVisitor = new RoleVisitor();
ExperienceVisitor experienceVisitor = new ExperienceVisitor();
Architect architect = new Architect();

architect.accept(roleVisitor);
architect.accept(experienceVisitor);
end note

{% endplantuml %}

</div>

In the above example, if we wanted to add a new feature to say, calculate pay, we would be able to easily accomplish this by adding a new class, and the exising classes would not be impacted at all. 

### The Observer Pattern 

### The State Pattern 

### The Strategy Pattern 

### The Chain of Responsibility Pattern 

### The Interpretor Pattern 

### The Mediator Pattern 

### The Momento Pattern 

