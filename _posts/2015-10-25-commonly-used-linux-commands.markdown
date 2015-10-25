---
layout: post
title:  "Useful Linux Commands"
date:   2015-10-25 12:52:23
categories: quick-reference 
---
My objective for this post is to come up with a list of Linux commands that I commonly use so that I can always have a quick reference and don't waste time googling things around.

As you would guess by looking at this post, it's still under development.  
<br/>

# Finding Files 
{% highlight bash %}
#Find all files with the given name
find -name "file_name"		           	

#Find all files that don't match the given name
find -not -name "file_name"		  	 

#Find all files that contains the given string in the name
find . -type f -name "*some_string*"  
{% endhighlight %}
<br/>



