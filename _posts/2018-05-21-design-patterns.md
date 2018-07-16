---
layout: default
title:  "Desing Patterns"
date:   2018-05-21 
categories: other
---

## Behavioral Patterns  

Behavioral Patterns are used to improve flexibility when it comes to communication between objects.

### Command Pattern

The command pattern should be used when you want to decouple the invoker of a command from the command itself. It allows a command to be executed at a later time.

Parts of the Command Pattern:

Client: Creates the commands and stores it in the invoker

Invoker: Causes the command to be executed

Command: Binds the operation to the receiver and decides which operation is to be performed on the receiver. Generally, the command object implements the Command interface and has an execute() method.

Receiver: The object that knows how to perform the command. This logic in the receiver can be added to the command itself.

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

### Strategy Pattern

The strategy pattern should be used when you have a set of algorithms that can be interchanged. The algorithms are encapsulated and the client does not have any knowledge of them. Each strategy essentially represents a behavior.
 
It decreases the cyclomatic complexity because it reduces the number of if/else statements that would be present in your code.
 
It is better for testing because rather than testing one large method and multiple execution paths, you can test multiple smaller strategies, reducing the possibility of missing an exeuction branch.
 
It helps your code abide by the open-closed principle, as the client code does not need to be modified whenever there is a new behavior that is added.

{% plantuml %}
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
<!--
https://softwareengineering.stackexchange.com/questions/302612/advantages-of-strategy-pattern
http://java-x.blogspot.ca/2006/12/strategy-pattern.html
--> 

### Observer Pattern

<strong>What/When?</strong>  
Comprises of the following objects: Publisher and Observer.

Publisher: The Publisher maintains some state and notifies all interested observers of some even that takes place.

Observer: The Observer registers itself via the Publisher whenever it wants to get notifications for a particular event, and de-registers itself when it is no longer interested.

The pattern should be used when you need to implement a subscribe/publish scenario.

<strong>Advantages?</strong>  
It promotes lose coupling between the Subject and the Observer, which allows us to build more flexible systems that can handle change better, as it minimizes the interdepency between objects:  
&nbsp;1/ The Publisher only needs to know that the Observer can be notified of a given event and nothing else specific about it  
&nbsp;2/ The Observer only needs to know that they can register/de-register via the Publisher  
&nbsp;3/ We can change and re-use the Publisher and Observer objects independently of each other  

<strong>Disadvantages?</strong>  
<font color="red">TODO</font>

<strong>Example:</strong>  
{% plantuml %}
{% endplantuml %}

### State Pattern

<strong>What/When?</strong>  
Comprises of the following objects: Context and State. 

State: There is one object per possible state in the system. The State object contains methods which represent the possible events that can occur at any given time. The handling of each event will be different for different states, as well, for each event, the state that a system will transition into after executing an event is dependent on the current internal state of the object.

Context: Keeps track of the current state. It delegates any request that it may receive to one of the State objects.

This pattern should be used when the behavior that an object is expected to perform is dependent on its internal state. We can view it as overseeing the State.

<strong>Advantages?</strong>    
&nbsp;1/State transitions are made more explicit as the logic is not buried in conditional statements  
&nbsp;2/We encapsulate what varies thereby adhering to the Open Closed Principle

<strong>Disadvantages?</strong>    
<font color="red">TODO</font>

<strong>Example:</strong>


### The Chain of Responsibility Pattern



### Visitor Pattern

The Visitor pattern allows you to separate operations from the objects on which the operation is performed, thus allowing you to add new operations without modifying the classes which get operated on.

The objects performing the operation implement the Visitor interface, and those objects on which the operation is being performed on, implement the Visitable interface. The Vistor interface has a method called visit for each object in the hierarchy that implements the Visitable interface.

It promotes the open/closed principle because the set of objects don't need to be modified each time there is a new operation that is added. In the example below, if we wanted to add a new feature to say, calculate pay, we would be able to easily accomplish this by adding a new class, and the existing classes would not be impacted at all.

The Visitor pattern helps to solve the problem of double-dispatch. Java and other object oriented programming languages only support single dispatch, where the method to execute is chosen at run time based on the type of the object the method is being invoked on. This mechanism of selecting the method does not work for arguments being passed, and this is where the Vistor pattern may help out.

<!-- <img src="http://www.plantuml.com/plantuml/png/hLHDRzGm4BtxLupsj2iaYo9nuGCLjKXme22euEnrPhjM7JlOaorLuR_ZREBOSQgeMd6AyzxBc-UPsJtt91orjMRiao5qEo4HVYYlI6mrmWC3E5XLWP0I6reV6UlWq3ytx2-xqC9xUE_aNX5AWeSH--firKhwScVGPV1dOSJD1Bb6JnFW4W-eRTDZPJ3hnbXzZdKgBk9fCrLCeZJPIw6BsUh-MR13JWgF6PSYL_6KklFDQapP8_hXTn0fD7B2fURpT_726VZc3-UfsoKnv2_XFdY9niWp8kyMYzawXkStAPZPRPYnXE3KpPx0xj9IzRZ6NG4lxTbnuX1VUTzosYk_UHrQXgQ2O3euRosHhOFt9EpokiG2t-yzOSrjIxnnof0swzKbIbMX1skIldN8LyVQx4bRzhXzvtxjXF5Q47hOjbuPz1uS_cgLmneD-R9CkQIBvXzHDvrTRGy8pefggwsydNkMgxtGZKxeWVO8qbQf2Gi_X6M_dquHveQB4vqlsUbpVV7o6ToZS3uOnvPN_scgPyypRnn3bsMMftgw-UdZlR9FT9oF-MJVOjh2mzKPkz11IgyOo_yxNNP-2mRl86FNmMks7wbgyM5IPfy_ia63V6Gw6HjPFlnVPS42FwFB446KBitEmx6jzJy0"/> -->


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
Visitable <|.. Architect
Visitable <|.. Manager
Visitable <|.. Tester
Visitable <|.. Developer
Visitable <|.. ProductOwner
Visitor <|... RoleVisitor
Visitor <|... ExperienceVisitor
note right of Visitable
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

<!--
https://manski.net/2013/05/the-visitor-pattern-explained/
-->

## Structural Patterns

### Composite Pattern

### Decorator Pattern

### Flyweight Pattern

### Proxy Pattern

### Adapter Pattern

### Bridge Pattern

### Facade Pattern