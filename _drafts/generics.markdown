---
layout: page
title: "Generics"
subtitle: "Basics and Things I Didn't know about"
use-site-title: true
---

CATEGORY: PERSONAL NOTES

- Why? Generics allow you to use types as parameters when defining classes and methods.
- Advantages 
 1. You get type checking at compile time  
 2. You don't have to explicitly cast  
 3. You could use the same code that could work for multiple classes, reducing the need to duplicate code for different types  
- Given two concrete types A and B, MyClass\<A> has no relationship to MyClass\<B>, regardless of whether or not A and B are related. The common parent of MyClass\<A> and MyClass\<B> is object. Thus, let's say, A was the parent of B, you would not be able to pass MyClass\<B> wherever MyClass\<A> was used. <!-- [1] -->
- Upperbound, Lowerbound, and Unbound wildcards
 1. Upperbound: <? extends T> - ? must be T or a subtype of T
 2. Lowerbound: <? super T> - ? must be T or a supertype of T
 3. Unbound: <T> - T can be any type (it can be used to represent an unknown type, and it should be used when the functionality provided by the object class is to be used.)






<!-- 
[1]https://docs.oracle.com/javase/tutorial/java/generics/inheritance.html
-->
