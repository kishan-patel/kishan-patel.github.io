---
layout: post
title:  "Main Points in Effective Java"
date:   2015-11-25 12:52:23
categories: quick-reference 
---

**Effective Java** by Joshua Bloch is widely believed to be one of the better books to read for those who are looking to polish their skills in Java. Each time I sat down to read this book however, I always found myself very locked in at the start, but as I read more, I realized that I was just skimming through the content. This time around, I want to be more thorough and absorb as much of the information that this books has to offer. To accomplish this, I'm going to try to create a post where I jot down the key points for each item.  

<br/>

## Creating and Destroying Objects

> # Item 1: Consider static factory methods instead of constructors  
  
- One of the advantageous is that it has a name, and this makes the client code easier to use and read.
- A class can only have one constructor with a given signature, and often times, to get around this, programmers just change the order of the types. This however, is not good practice because we can easily call the wrong constructor by mistake.
- In cases where a class needs multiple constructors, we can use static factory methods to highlight key differences.
- Static factory methods are not required to create a new instance of the class each time they are invoked.