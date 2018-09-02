---
layout: default
title:  "Desing Patterns"
date:   2018-05-21 
categories: other
---

<!--
  1- Single Responsibility Principle: a class should only do one thing
  2- Open Closed Principle: classes should be open for extension but closed for modification
    - because we are only adding new code, the chances of introducing bugs or causing un-intended side effects in pre-existing code are reduced
  3- Liskov Substitution Principle: if s extends t then objects of type t may be replaced by objects of type s without altering the correctness of the program
  4- Interface Segregation Principle: many client specific interfaces are better than one general-purpose interface
  5- Dependency Inversion Principle: one should depend upon abstractions not concretions (both high level classes and low level classes should depend upon abstractions)
-->

<!--
what to strive for when programming:
1- extendible code
2- maintainable code
3- easy to understand code / readable code 
-->

<!--
pillars of oop:
1-abstraction
  -you don't need to worry about all the inner details of a class 
2-encapsulation
  -you have control over the state of an object
3-inheritance
  -you could re-use code
4-polymorhpishm
  -when you program to an interface, you're code is more flexible, maintainable, and extensible.
-->

<!--
why new is bad:
it commits the class to a particular object and this is bad because:
1/it makes it impossible to change the instantiation independently from (without having to change) the class
2/it stops the class from being re-usable if other objects are required
3/it makes the class hard to test because real objects cannot be mocked

why dependency injection is useful:
-->

## Creational Patterns

Creational Patterns are used to construct objects and reduce design problems and added complexity which may result if done improperly.

<!-- ################################################################### -->
<!--                        ABSTRACT FACTORY                             -->
<!-- ################################################################### -->

### Abstract Factory Pattern

<strong>When:</strong>  
The Abstract Factory Pattern should be used when you want to create a family of related objects and you want to decouple the client from the actual factory that creates these objects. The Abstract Factory Pattern provides an interface to the client for creating such family of objects.

<strong>What:</strong>  
Parts of the Abstract Factory Pattern:

Client: The client has a reference to the factory which it uses to create the product. The client only knows about the interfaces of the factory and product.

Factory: The interface which specifies the family of objects you can expect this factory to create. 

Product: The interface used to represent a product to be created by a factory.

<strong>Advantages:</strong>  
The client is only aware of the interface for creating the objects. This means factories can be easily substituted to get different behaviors at run-time. The decoupling of the client code from the object creation code will result in the application being more maintainable (the client code won't have to be changed whenever there is a change to the object creation code), extensible (different implementations of object creation code can be utilized), and testible (object creation code can be mocked).

It helps prevent duplication as all the object creation code is localized in one place which will be helpful during maintenance because we will only need to perform bug fixes in one place.  

<strong>Example:</strong>
<img src="http://www.plantuml.com/plantuml/png/XLNBRjim4BppAmZqOWE5Vg1DaS9eqKFJvf0Ve2NQ8KAJ1aMsS5N_UwdbAcjAgmO876fsPlP1YhhlemendQmmBkfmKAsMEnKUCzX_LMtquI87ySKTZTEo3Lf5NHusM_7D-mwnSPcHfv3S2qAmpjXLt5YZqJ12ygZZZtJQw_3piBjOupeT-YomtXrlOzzD3Be79pA2t8FOUUl3I8R5Z0CLy2GXMglwFjkuJYtxlMBuoLzy_4_yGVrXvRK_DZsp9RXo8xJom7vh1m99ZrYjnadKSaHdUW8HpUqzA9VoH6CAEfJG76oQvjFytF2aqXyV6sld8r2L4FDHV_pRDEmUiansEtagkxDYUWyeRG4g799m0R147DuTW6bx2KCF0aaF6Bvd98TdGj6WWibYPPPDjJri49Bp8JHrFceP_Ldwm_pWY7CmlrGE7unJTenE3kthyiE2LETgwRdGnJdjhMddkJQi-_kt_BPo45B6PzCtf99tLO4KhvpkbhLTRuh3Et5JCk2fqF1lAMtgUtRC2QVWEV-iiaT6uPRzZl2xnWPEeUU_e6CAxgRDZ4dPz3fY3QNIxIiCoSPo22gEa1N1VJAsWzjMkqwE9wC-7_pbEWsD_UJ8WQfr-ZTQqA2kOf8llasy56ALaFc4yT9fXAlzpI-oTq5tOcUDTd5LKSy259_tVGmPa8ZoMfnNaJm6twLsBGkCvcqUJe8dtkTLEjb_">

<!--
@startuml
interface CarPartsFactory {
Engine createEngine()
Hood createHood()
Trunk createTrunk()
}

interface Engine {
int getNumberOfCylinders()
long getNumberOfLitres()
}
interface Hood {
Color getColor()
}
interface Trunk {
Color getColor()
}


class HondaCarPartsFactory {
}
class ToyotaCarPartsFactory {
}
class MazdaCarPartsFactory {
}


class HondaEngine {
}
class ToyotaEngine {
}
class MazdaEngine {
}

class HondaHood {
}
class ToyotaHood {
}
class MazdaHood {
}

class HondaTrunk {
}
class ToyotaTrunk {
}
class MazdaTrunk {
}

class CarManufacturer {
}

CarManufacturer ...> CarPartsFactory
CarManufacturer ...> Engine
CarManufacturer ...> Hood
CarManufacturer ...> Trunk

CarPartsFactory <|.. HondaCarPartsFactory
CarPartsFactory <|.. ToyotaCarPartsFactory
CarPartsFactory <|.. MazdaCarPartsFactory

Engine <|.. HondaEngine
Engine <|.. ToyotaEngine
Engine <|.. MazdaEngine

Hood <|.. HondaHood
Hood <|.. ToyotaHood
Hood <|.. MazdaHood

Trunk <|.. HondaTrunk
Trunk <|.. ToyotaTrunk
Trunk <|.. MazdaTrunk

CarPartsFactory ....> Engine
CarPartsFactory ....> Hood
CarPartsFactory ....> Trunk

note top of CarManufacturer
private final CarFactory carFactory;
private final CarPartsFactory carPartsFactory;

public CarManufacturer(CarFactory carFactory, CarPartsFactory carPartsFactory) {
  this.carFactory = carFactory;
  this.carPartsFactory = carPartsFactory;
}
public Car create() {
  Engine engine = carPartsFactory.createEngine();
  Hood hood = carPartsFactory.createHood();
  Trunk trunk = carPartsFactory.createTrunk();
  
  return carFactory
    .setEngine(engine)
    .setHood(hood)
    .setTrunk(trunk)
    .build()
}
end note

note top of ToyotaCarPartsFactory 
public Engine createEngine() {
  return new ToyotaEngine();
}

public Hood createHood() {
  return new ToyotaHood();
}

public Trunk createTrunk() {
  return new ToyotaTrunk();
}
end note

note top of CarManufacturer #red
Client
end note

note top of CarPartsFactory #red
Abstract Factory
end note

note top of Engine #red
Product
end note

note top of Hood #red
Product
end note

note top of Trunk #red
Product
end note
@enduml 
-->

<!--
Side Notes:

Difference between Factory Method Pattern and Abstract Factory Pattern:
-They are both responsible for the creation of objects. The Factory Method Pattern does it through inheritance whereas the Abstract Factory Pattern does it through composition.
-The Abstract Factory Pattern is more suitable when you want to create an entire family of products whereas the Factory Method Pattern should be used when you only want to create one product.
  -->

<!-- ################################################################### -->
<!--                        BUILDER                                      -->
<!-- ################################################################### -->

### Builder Pattern

<!-- ################################################################### -->
<!--                        SINGLETON                                    -->
<!-- ################################################################### -->

### Singleton Pattern

## Behavioral Patterns  

Behavioral Patterns are used to improve flexibility when it comes to communication between objects.

<!-- ################################################################### -->
<!--                          COMMAND                                    -->
<!-- ################################################################### -->

### Command Pattern

<strong>When:</strong>

The command pattern should be used when you want to decouple the invoker of a command from the command itself. It allows a command to be executed at a later time.

<strong>What:</strong>  
Parts of the Command Pattern:

Client: Creates the commands and stores it in the invoker

Invoker: Causes the command to be executed

Command: Binds the operation to the receiver and decides which operation is to be performed on the receiver. Generally, the command object implements the Command interface and has an execute() method.

Receiver: The object that knows how to perform the command. This logic in the receiver can be added to the command itself.

<strong>Advantages:</strong>  
It decouples the logic that will be executed (command) from the object that performs the execution (invoker) making it possible to add new commands without changing existing code.  

It provides a structured technique to store the users command thereby making it easier to perform undo/redo operations.

<img src="http://www.plantuml.com/plantuml/png/fPH1ZzCm48NF-5UCzfIANOipYv1GcqCb99RISZVsP3UIumdsUBlLqlyEgOEJagfKQYwsnlRtFEz55dEhGe0L_emO-C6JnX38mwi0k2jVK4Sc3zXFkkAT07ZxJBM1DktkpnRz23wDCx7luHdpceygOzRqDMB4mf9x18DMxMvXJasZd06TnWwnT8o-KXhpua19ry9Ya9fxL8oRW9tOFZV7liRdVykRraptBj3YgEY84InM35HDJ1ANk72uRjZMh9-AlYOVaTUx5ejPMWNGAY3CL-MdTVbUGFgowN9arhjRSBWTjLdyrPdT3wHLkLujo-z_M6_EGCQsdCHi7XQNNYXxUPgqA3-Nbv5o05EImKf5omE5dpnjaxmBiMt9CvelBNh5DRdoHMFRJOh3-RtO2tG6kaHJh3-8cHgWQcIdEFglKZpVTe6naHHPjhvsR5rnq-s547MNV1MjtO4-C8oycTq3dD7Ahb-bvXCbwPrHIxbSfnKxnd-LKcxNTjNGYPucZvFycDyKaIQfsByGeX_XmoyfvIZTyS9n44SdPB9jkZ9gyZS0"/>

<!--
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
-->

<!-- 
Links:
https://en.wikipedia.org/wiki/Command_pattern
-->

<!-- ################################################################### -->
<!--                          STRATEGY                                   -->
<!-- ################################################################### -->

### Strategy Pattern

<strong>When:</strong>

The strategy pattern should be used when you have a set of algorithms that can be interchanged. The algorithms are encapsulated and the client does not have any knowledge of them.

<strong>What:</strong>  
Parts of the Strategy Pattern:

Strategy: Each Strategy Essentially represents a behavior.

<strong>Advantages:</strong>  
It decreases the cyclomatic complexity because it reduces the number of if/else statements that would be present in your code.

It is better for testing because rather than testing one large method and multiple execution paths, you can test multiple smaller strategies, reducing the possibility of missing an exeuction branch.  

It helps your code abide by the open-closed principle, as the client code does not need to be modified whenever there is a new behavior that is added.

<!--

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

-->

<img src="http://www.plantuml.com/plantuml/png/xLFDSjem4BxhANPoCcsiF42RKo5JPfeBDBqBUmsUw8UH5cQOb7UlPNbngYOjpN3eeIU1zllPtK_-f5K8S8yXg3L-LhRMwE59b4jolhk1a4vHbkBzthKrR7hCGFZg7WBwOlW79fsJdw0B35jd0zvvPteqNu1FFphyKLX721eR0jTaxOYpVRl60QIK0hXl6Kyi1e1S8ythOd8zCcvkW5LQizLeq5A0VlgLHZdgeQqJaDNwjlzgpkVzjGqKV1_RMfAYNIWcS7iBqzcN-RVPOZPDX76O6ZKICkyqpkH3XpeEqaU1jeQuJj5QGj-e2e7JV1gIILjPac_j6XxnS7sQ6FPAxx1JJC3TjbPq5dBeRKJ6oWdhiRl7VLO_Ygf_VdUjnkKX49gnKQvD5QcL2lXhPMxlqJX_U5x97l8xANbsmR2FtyioTypAcMbMp7pJqrqv8cV0DIz8dxNob7KYIhSZkUsGf6rn5N6Hv2pG1g7fz24at5M_n36fjnayHEgV7JZXDpXC8pMo6k_CAnw_VIklAYyI-4Nj0ukFtqGU5WVzFwf_FYh-x2uSLMkXKjK6BnqGYru-4rQ-K1AicAt_1m00">

<!--
Links:
1/ https://softwareengineering.stackexchange.com/questions/302612/advantages-of-strategy-pattern
2/ http://java-x.blogspot.ca/2006/12/strategy-pattern.html 
--> 

<!-- ################################################################### -->
<!--                            OBSERVER                                 -->
<!-- ################################################################### -->

### Observer Pattern

<strong>When:</strong>  
The pattern should be used when you need to implement a subscribe/publish scenario.

<strong>What:</strong>  
Parts of the Observer Pattern: Publisher and Observer.

Publisher: The Publisher maintains some state and notifies all interested observers of some even that takes place.

Observer: The Observer registers itself via the Publisher whenever it wants to get notifications for a particular event, and de-registers itself when it is no longer interested.

<strong>Advantages:</strong>  
It promotes lose coupling between the Subject and the Observer, which allows us to build more flexible systems that can handle change better, as it minimizes the interdepency between objects:  
&nbsp;1/The Publisher only needs to know that the Observer can be notified of a given event and nothing else specific about it  
&nbsp;2/The Observer only needs to know that they can register/de-register via the Publisher  
&nbsp;3/We can change and re-use the Publisher and Observer objects independently of each other  

<strong>Example:</strong>  

<!-- ################################################################### -->
<!--                              STATE                                  -->
<!-- ################################################################### -->

### State Pattern

<strong>When:</strong>  

This pattern should be used when the behavior that an object is expected to perform is dependent on its internal state. We can view it as overseeing the State.

<strong>What:</strong>  
Parts of the State Pattern: Context and State. 

State: There is one object per possible state in the system. The State object contains methods which represent the possible events that can occur at any given time. The handling of each event will be different for different states, as well, for each event, the state that a system will transition into after executing an event is dependent on the current internal state of the object.

Context: Keeps track of the current state. It delegates any request that it may receive to one of the State objects.

<strong>Advantages:</strong>    
State transitions are made more explicit as the logic is not buried in conditional statements.

We encapsulate what varies thereby adhering to the Open Closed Principle.

<strong>Example:</strong>

<!-- ################################################################### -->
<!--                    CHAIN OF RESPONSIBILITY                          -->
<!-- ################################################################### -->

### The Chain of Responsibility Pattern

<strong>When:</strong>  
The Chain of Responsibility Pattern should be used when you want to decouple the sender of a request from the receiver of the request (i.e. the handler of the request).  

<strong>What:</strong>  
Parts of the Chain of Responsibility Pattern: Sender and Handler(s)

Sender:  Delegates the request to some handler. It does not rely on a concrete handler implementation. Instead, it has access to one handler which it delegates the request to. That handler will accept the request if a certain criteria is met, otherwise it will find the next handler in line to process the request - this process is repeated until a handler is found or until there are no more handler that remain.

Handler:  Responsible for processing a given request. A handler can contain one or more filters which it applies before deciding whether it should take ownership of the request.

<strong>Advantages:</strong>  
Promotes lose coupling because the sender of the request does not need to know who/what will handle the request.

<strong>Example:</strong>

<!-- ################################################################### -->
<!--                            VISITOR                                  -->
<!-- ################################################################### -->

### Visitor Pattern

<strong>When:</strong>  
The Visitor pattern allows you to separate operations from the objects on which the operation is performed, thus allowing you to add new operations without modifying the classes which get operated on.

<strong>What:</strong>  
The objects performing the operation implement the Visitor interface, and those objects on which the operation is being performed on, implement the Visitable interface. The Vistor interface has a method called visit for each object in the hierarchy that implements the Visitable interface.

<strong>Advantages:</strong>  
It promotes the open/closed principle because the set of objects don't need to be modified each time there is a new operation that is added. In the example below, if we wanted to add a new feature to say, calculate pay, we would be able to easily accomplish this by adding a new class, and the existing classes would not be impacted at all.  

The Visitor pattern helps to solve the problem of double-dispatch. Java and other object oriented programming languages only support single dispatch, where the method to execute is chosen at run time based on the type of the object the method is being invoked on. This mechanism of selecting the method does not work for arguments being passed, and this is where the Vistor pattern may help out.  

<strong>Example:</strong>
<img src="http://www.plantuml.com/plantuml/png/hLHDRzGm4BtxLupsj2iaYo9nuGCLjKXme22euEnrPhjM7JlOaorLuR_ZREBOSQgeMd6AyzxBc-UPsJtt91orjMRiao5qEo4HVYYlI6mrmWC3E5XLWP0I6reV6UlWq3ytx2-xqC9xUE_aNX5AWeSH--firKhwScVGPV1dOSJD1Bb6JnFW4W-eRTDZPJ3hnbXzZdKgBk9fCrLCeZJPIw6BsUh-MR13JWgF6PSYL_6KklFDQapP8_hXTn0fD7B2fURpT_726VZc3-UfsoKnv2_XFdY9niWp8kyMYzawXkStAPZPRPYnXE3KpPx0xj9IzRZ6NG4lxTbnuX1VUTzosYk_UHrQXgQ2O3euRosHhOFt9EpokiG2t-yzOSrjIxnnof0swzKbIbMX1skIldN8LyVQx4bRzhXzvtxjXF5Q47hOjbuPz1uS_cgLmneD-R9CkQIBvXzHDvrTRGy8pefggwsydNkMgxtGZKxeWVO8qbQf2Gi_X6M_dquHveQB4vqlsUbpVV7o6ToZS3uOnvPN_scgPyypRnn3bsMMftgw-UdZlR9FT9oF-MJVOjh2mzKPkz11IgyOo_yxNNP-2mRl86FNmMks7wbgyM5IPfy_ia63V6Gw6HjPFlnVPS42FwFB446KBitEmx6jzJy0">

<!--

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

-->

<!--
Links:
1/https://manski.net/2013/05/the-visitor-pattern-explained/
-->

<!-- ################################################################### -->
<!-- ################################################################### -->

## Structural Patterns

<!-- ################################################################### -->
<!--                      COMPOSITE                                      -->
<!-- ################################################################### -->

### Composite Pattern

<!-- ################################################################### -->
<!--                      DECORATOR                                      -->
<!-- ################################################################### -->
### Decorator Pattern
<strong>When:</strong>  
The Decorator Pattern should be used when you want to add additional functionality without having to subclass an object (i.e. you want to add additional functionality to one particular object as opposed to a class of objects). 

<strong>What:</strong>  
Parts of the Decorator Pattern:

Component: Some abstract class

Concreate Component: Some implementation of an Component class 

Decorator: Abstract class which is a subtype of Component and adds extra functionality to the Component

Concreate Decorator: Some implementation of the Decorator class

<strong>Advantages:</strong>  
It helps your code abide by the open-closed principle: you're adding new functionality without having to change existing code. This will help ensure that code that was already working will continue to do so.

<strong>Example:</strong>
<img src="http://www.plantuml.com/plantuml/png/bPFD3jem48JlVeeLlIG7o0EK8bHGVqwjrFR2pKasOCdsMlQczAUyUuEX2gcTgjoSsHdlDrXi0qlFlT5YfsK8yA5dr_CdzYWD_1INk_n6QPmVCVgPuHuxBPdcncyFxp_EZ7PQeUKeY8bb_MkvJ7XobeHBf5AqPYb5JepsX5e8IupWrV74GDqTNRY-rgg1hwHQE7l5-9cks4Kvb8BO088oJcCylWABPuY6HNKYWrKVq5Stnx8Rz1L_uqNvKi3qaUZnOxpbqLECUsB-CRAAQCNYYst8E8yXO0kCmwhL4VdrTyPGb6cgqHIm6FG_LNuevx3zLvMRuxagoMzThEjDjkAulrnNzMQsvo7wdcbu4MXRiCHuVsWc1zHDqLzuR47io3YoQ3aVYTH9R4ZPnYCZ_4USqQSNxB4XBvdytxcQcCdae-8TwJQ018yTUhHDUzq3qawAvKdIVqnQPeJANp6-R1gN-VnsEFL6_mO0">

<!--
  @startuml
Class OutputStream {
}
Class FileOutputStream {
}
Class FilterOutputStream {
}
Class DeflatorOutputStream {
}
Class GZIPOutputStream {
}
Class Client {
}

OutputStream <|-- FileOutputStream
OutputStream <|-- FilterOutputStream
FilterOutputStream <|-- DeflatorOutputStream
DeflatorOutputStream <|-- GZIPOutputStream

note right of Client
public void writeToFile() {
  File simpleFile = new File("/home/user/simple-file.txt");
  OutputStream outputStream = new FileOutputStream(simpleFile);
  outputStream.write("Uncompressed text".getBytes());
  outputStream.close();

  File zippedFile = new File("/home/user/zipped-file.txt");
  OutputStream outputStream = new GZIPOutputStream(<b>new FileOutputStream(zippedFile)</b>);
  outputStream.write("Zipped text".getBytes());
  outputStream.close();
}
end note

note top of OutputStream #red 
Component
end note

note top of FileOutputStream #red
Concrete Component
end note

note top of FilterOutputStream #red
Decorator
end note

note bottom of FilterOutputStream
Holds a referencde to an OutputStream
end note

note top of DeflatorOutputStream #red
Concrete Decorator
end note

note top of GZIPOutputStream #red
Concreate Decorator
end note
@enduml
-->

<!--
Side notes:
1/ The decorator adds its own behavior either before and/or after delegating to the object to do the rest of the job. 
-->

<!-- ################################################################### -->
<!--                      ADAPTER                                        -->
<!-- ################################################################### -->

### Adapter Pattern

<strong>When:</strong>  
The Adapter Pattern should be used when you want to take an interface and modify/adapt it to something that a client is expecting.
(real world example: Google Pixel's Easy Adapter which converts USB to USB-C)


### Bridge Pattern

### Facade Pattern

### Flyweight Pattern

### Proxy Pattern
