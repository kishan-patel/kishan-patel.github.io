---
layout: post
title:  "Main Points in Effective Java"
date:   2015-11-25 12:52:23
categories: quick-reference 
---

**Effective Java** by Joshua Bloch is widely believed to be one of the better books to read for those who are looking to polish their skills in Java. Each time I sat down to read this book however, I always found myself very locked in at the start, but as I read more, I realized that I was just skimming through the content. This time around, I want to be more thorough and absorb as much of the information that this books has to offer. To accomplish this, I'm going to try to create a post where I jot down the key points for each item.  

<br/>

## Chapter 1: Creating and Destroying Objects

> # Item 1: Consider static factory methods instead of constructors  

1. Makes the client code easier to understand because you are able to tell from the name what type of object you are getting, rather than having to rely on the arguments. It is also helpful in cases where you have multiple constructors that differ only in the order of the arguments: with static factory methods, a programmer is less likely to call the wrong constructor.

2. You don't have to return a new object each time the constructor is invoked; this means that objects are not created unnecessarily, and that classes can maintain strict control over which objects exist at any time.

3. You can return any subtype of the return type which gives you the flexibility of choosing the class of the returned object. This is beneficial because it reduces the size of the API (not all classes need to be exposed - e.g. Collections) and it forces the client to refer to the returned object by it's interface rather than it's implementation. One more thing, the impelentation of the subclass may not even exist at the time the static factory method is written (e.g. service providor frameworks like JDBC).

4. Static factory methods also reduce the verbosity required to create parameterized type instances.


> # Item 2: Consider a builder when faced with many constructor parameters

- The alternatives to using the buider patter are: the telescoping constructor pattern (a constructor is required paramters and then one constructor for each optional field) and the Javabeans pattern (an object is created first, and then the fields are set using setter methods). The disadvantage with the telescoping constructor pattern is that (in the worst case), you may have to pass a lot of parameters to the constructor, and you may not necessarily want to set all of them. The disadvantage with the Javabeans pattern is that, the object may be in a inconsisten state partway through it's creation. 

- Steps in the builder pattern: (1) the client calls the static factory method with all of the required parameters; (2) the client calls the setter method on the build object for each optional parameter; (3) the client calls the build method to actually create the object - the object is immutable.


> # Item 3: Enforce the singleton property with a private constructor or an enum type


> # Item 4: Enforce noninstantiability with a private constructor

- A default constructor is generated only if there are not constructors provided. To ensure that no default constructor is generated, and to ensure that a class is noninstantiable, you can include a private constructor.


> # Item 5: Avoid creating unnecessary 


> # Item 6: Eliminate obsolete object references

- When a program manages its own memory, the programmer is responsible for setting obsolete references to null


> # Item 7: Avoid finalizers

- Finalizers are unpredictable, often dangerous, and generally unnecessary. 


## Chapter 4: Classes and Interfaces

> Item 13: Minimize the accessibility of classes and members

- A well-designed module hides all of its implementation details, cleanly seperating its API from its implementation. Modules then communicate only through their APIs and are oblivious to each others' inner workings.

- Information hiding is important because it decouples the modules from the system, which allows them to be developed, tested, optimized, used, understood and modified in isolation. This speeds up system development because modules can be developed in parallel.

- "Instance fields should never be pulbic...classes with public mutable fields are not thread safe"

- "A nonzero-length array is always mutable, so it is wrong for a class to have a public static field array field, or an accessor that returns such a field."


> Item 14: In public classes, use accessor methods, not public fields

- "...if a class is accessible outside its package, provide accessor methods, to preserve the flexibility to change the classe's internal representation. If a public class exposes its data fields, all hope of changing its representation is lost, as client code can be distributed far and wide."


> Item 15: Minimize mutability

- "An immutable class is simply a class whose instances cannot be modified. All of the information contained in each instance is provided when it is created and is fexed for the lifetime of the object."

- "To make a class immutable, follow these five rules: (1) Don't provide any methods that modify the object's stat2. (2) Ensure that classes can't be extended. (3) Make all fields final. (4) Make all fields private. (5) Ensure exclusive access to any mutable components"

- "Immutable objects are inherently tread-safe; they require no syncrhonization. They cannot be corrupted by multiple threads accessing them concurrently. This is far and away the easiest approach to achieving thread safety."

- "The only real disadvantage of immutable classes is that they require a seperate object for each distince value."


> Item 16: Favor composition over inheritance

"Unlike method invocation, inheritance violates encapsulation...a subclass depends on the implementation details of its superclass...the superclass's implementation may change from release to relase, and if it does, the subclass may break."

"...superclass can acquire new method in subsequen release. [each element added into some collection must satisfy some predicate to meet security concers. this can be guaranteed by overriding all of the add methods and including and ensuring that each item that is to be added satisfies your predicate, but if new add methods and added to the superclass in subsequent releases, there is a risk that an illegal element may be inserted into the collection]."

"If the superclass acquires a new method in a subsequent release and you have the bad luck to have given the subclass a method with the same signature and a different return type, your subclass will no longer compile."

"Instead of extending an existing class, give your new class a private field that references an instance of an existing class. This design is called composition because the existing class becomes a component of the new one."

"Inheritance is appropriate only in circumstances where the subclass really is a subtype of the superclass. In other words, a class B should extend a class A only if an "is-a" relationship exists between the two classes. If you are tempted to have class B extend a class A, ask yourself the question: Is every B really an A?"


> Item 17: Design and document for inheritance or else prohibit it

"the class musst document precisely the effects of overriding any method...the class must document its self-use of overridable methods. For each public or protected method or constructor, the documentation must indicate which overridable methods te method or constructor invokes, in what sequence, and how the results of each invocation affect subsequent processing."


> Item 18: Prefer interfaces to abstract classes

- "Existing classes can be easily retrofitted to implement a new interface. All you have to do is add the required methods if they dont' yet exist and add an implements clause to the class declaration."

- "Interfaces are ideal for defining mixins. Loosely speaking, a mixin is a type that a class can implement in additin to its \"primary type\" to declare that it provides some optional behavior."


> Item 19: Use interfaces only to define types

- "The constant interface pattern is a poor use of iterfaces. That a class class uses some constants internally is an implementation detail...it represents a commitment: if in a future release, the class is modified so that it no longer needs tu use the constants, it still must implement the itnerface to ensure binary compatibility. If a nonfinal class implements a constant interface, all of its subclass will have their namespace polluted by teh constant in the interface." 


##Chapter 6: Enumbs and Annotations

> Item 30: Use enums instead of int constants

- "An enumerated type is a type whose legal values consist of a fixed set of constants, such as teh seasons of the year, the planets in the solar system, or the suits in a deck of playing cards."

- "...the int enum patter, has many shortcomings. It provides nothing in the way of type safety and little in the way of convenience."

- "...Because int enums are compile-time constants, they are compiled into the clients that use them. If the int associated with an enum constant is changed, its clients must be recompiled. If they aren't thye will still run, but their behavior will be undefined..."

- "...There is not easy way to translate int enum constants into printable strings...There is not reliable way to iterate over all the int enum constants in a group, or even to obtain the size of an int enum group..."

- "...the String enum pattern, is even less desirable...it can lead to performance problems because it relies on string comparisons...it can lead to naive users to hard-code string constants into the client code instead of using field names...if such a hard-coded string constant contains a typographical error, it will escape detection at compile time and result in bugs at runtime..."

- "...[enum types] are classes that export one instance for each enumeration constant via a public static final field. enum types are effectively final, by virtue of having no accessible constructors..."

- "...enum types let you add arbitrary method and fields and implement arbritrary interfaces. They provide high-quality implementations of all the Object methods..."

- "...Enums are, generally speaking, comparable in performance to int constants..."

- "...So when should you use enums? Anytime you need a fixed set of constants...it also includes other sets for which you know all the possible values at compile time, such as choices on a menu, operation codes, and command line flags..."


> Item 31: Use instance fields instead of ordinals

- "...Never derive a value associated with an enum from its ordinal; store it in an instance field instead..."


> Item 32: Use EnumSet instead of bit fields


> Item 33: Use EnumMap instead of ordinal indexing