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

The Composite pattern is useful when you want to model a tree-like-structure. There are two type of objects: Composite and Leaf. Composite can contain other Composite objects or Leaf objects. Leaf objects on the other hand are simple, and do not contain other objects. Both Composite and Leaf objects extend the abstract Component class.

#### <u>Example</u>

### The Decorator Pattern 

### The Flyweight Pattern 

### The Proxy Pattern 

### The Adapter Pattern 

### The Bridge Pattern 

### The Facade Pattern 

## Behavioral Pattern 

### The Command Pattern 

#### <u>Summary</u>

The command pattern should be used when you want to decouple the invoker of a command from the command itself. It allows a command to be executed at a later time.

Parts of the Command Pattern:

Client: Creates the commands and stores it in the invoker

Invoker: Causes the command to be executed

Command: Binds the operation to the receiver and decides which operation is to be performed on the receiver. Generally, the command object implements the Command interface and has an execute() method.

Receiver: The object that knows how to perform the command. This logic in the receiver can be added to the command itself.
 

#### <u>Example</u>
<div class="plantUml">
{% plantuml %}
Class RequestProcessor {
  -Executor executor
  --
  +void processRequest(Request request)
}
Class Executor {
  +void addToQueue(long delay, Command command)
}
Interface Command {
  +void execute()
}
Class CreateUser {
}
Class RetrieveUser {
}
Class UpdateUser {
}
Class DeleteUser {
}
note left of RequestProcessor
void processRequest(Request request) {
  switch(request.getType()) {
    case CREATE:
        executor.addToQueue(0, new CreateUser(request));
    case RETRIEVE:
	executor.addToQueue(0, new RetrieveUser(request));
    case UPDATE:
        executor.addToQueue(0, new UpdateUser(request));
    case DELETE:
        executor.addToQueue(0, new DeleteUser(request));
    default:
        throw new UnsupportedOperationException();
  }
}
end note
note bottom of CreateUser
void execute() {
  System.out.println("User successfully created.");  
}
end note
note bottom of RetrieveUser
void execute() {
  System.out.println("User successfully retrieved.");
}
end note
note bottom of UpdateUser
void execute() {
  System.out.println("User successfully updated.");
}
end note
note bottom of DeleteUser
void execute() {
  System.out.println("User successfully removed.");
}
end note
RequestProcessor .> Executor
Executor .> Command
Command <|... CreateUser
Command <|. RetrieveUser
Command <|.... UpdateUser
Command <|.. DeleteUser
{% endplantuml %}
</div>

### The Visitor Pattern 

#### <u>Summary</u>

The Visitor pattern allows you to separate operations from the objects on which the operation is performed, thus allowing you to add new operations without modifying the classes which get operated on.

The objects performing the operation implement the Visitor interface, and those objects on which the operation is being performed on, implement the Visitable interface. The Vistor interface has a method called visit for each object in the hierarchy that implements the Visitable interface.

It promotes the open/closed principle because the set of objects don't need to be modified each time there is a new operation that is added. In the example below, if we wanted to add a new feature to say, calculate pay, we would be able to easily accomplish this by adding a new class, and the existing classes would not be impacted at all.

The Visitor pattern helps to solve the problem of double-dispatch. Java and other object oriented programming languages only support single dispatch, where the method to execute is chosen at run time based on the type of the object the method is being invoked on. This mechanism of selecting the method does not work for arguments being passed, and this is where the Vistor pattern may help out.

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
Visitable .> Visitor
Visitable <|.... Architect
Visitable <|. ProductOwner
Visitable <|.. Manager
Visitable <|.. Tester
Visitable <|.. Developer
Visitor <|... RoleVisitor
Visitor <|... ExperienceVisitor
note left of Visitable
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

https://manski.net/2013/05/the-visitor-pattern-explained/

### The Observer Pattern 

SATURDAY

### The State Pattern 

SATURDAY

### The Strategy Pattern 

The strategy pattern should be used when you have a set of algorithms that can be interchanged. The algorithms are encapsulated and the client does not have any knowledge of them. Each strategy essentially represents a behavior.

It decreases the cyclomatic complexity because it reduces the number of if/else statements that would be present in your code.

It is better for testing because rather than testing one large method and multiple execution paths, you can test multiple smaller strategies, reducing the possibility of missing an exeuction branch.

It helps your code abide by the open-closed principle, as the client code does not need to be modified whenever there is a new behavior that is added.

<div class="plantUml">
{% plantuml %}
@startuml
Class MessageHandler {
-Storage storage
--
+void handleMessageToUser(Message message)
+void handleResponseFromUser(Response response)
}
note left of MessageHandler
void handleMessageToUser(Message message) {
  ...
  storage.store(message.getId(), message) // Message implements Storable.
  ...
  sendMessage(message)
}
void handleResponseFromUser(Response response) {
  ...
  if (response.getStatus() == DELIVERED) {
    storage.delete(response.getId());
  }
  ...
}
end note
interface Storage {
+void store(String key, Storable value);
+void update(String key, Storable value);
+void delete(String key);
+Storable retrieve(String key);
}
class FileSystemStorage {

}
class DatabaseStorage {
}
class InMemoryStorage {
}
MessageHandler *.. Storage
Storage <|-- FileSystemStorage
Storage <|-- DatabaseStorage
Storage <|-- InMemoryStorage
note bottom of FileSystemStorage
void store(String key, Storable value) {
  System.out.println("Storing on the file system.");
}
void update(String key, Storable value) {
  System.out.println("Updating on the file system.");
}
void delete(String key, Storable value) {
  System.out.println("Deleting from the file system.");
}
Storable retrieve(String key) {
  System.out.println("Retrieving from the file sysytem.");
}
end note
note bottom of DatabaseStorage
void store(String key, Storable value) {
  System.out.println("Storing on the file system.");
}
void update(String key, Storable value) {
  System.out.println("Updating on the file system.");
}
void delete(String key, Storable value) {
  System.out.println("Deleting from the file system.");
}
Storable retrieve(String key) {
  System.out.println("Retrieving from the file sysytem.");
}
end note
note bottom of InMemoryStorage
void store(String key, Storable value) {
  System.out.println("Storing in cache.");
}
void update(String key, Storable value) {
  System.out.println("Updating cache.");
}
void delete(String key, Storable value) {
  System.out.println("Deleting from cache.");
}
Storable retrieve(String key) {
  System.out.println("Retrieving from cache.");
}
end note
@enduml
{% endplantuml %}
</div>

https://softwareengineering.stackexchange.com/questions/302612/advantages-of-strategy-pattern
http://java-x.blogspot.ca/2006/12/strategy-pattern.html

### The Chain of Responsibility Pattern 

FRIDAY/SATURDAY/SUNDAY

### The Interpretor Pattern 

### The Mediator Pattern 

### The Momento Pattern 

