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

3. You can return any subtype of the return type 