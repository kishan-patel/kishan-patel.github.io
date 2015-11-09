---
layout: post
title:  "Useful Linux Commands"
date:   2015-10-25 12:52:23
categories: quick-reference 
---
My objective for this post is to come up with a list of Linux commands that I commonly use so that I can always have a quick reference and reduce the amount of time I spend Googling. Ideally, this list will continue to grow overtime.

<br/>

# Finding Files 
{% highlight bash %}
#Find all files with the given name
find -name 'some_file_name'		           	

#Find all files that don't match the given name
find -not -name 'some_file_name'		  	 

#Find all files that contain the given string in its name
find -type f -name 'some_string'  

#Find all files that contain the given string
find . -type f -exec grep -l 'some_string' {} +

#Find all files with the given extension(s) that contain the given string
find . -type f -name "*.'some_extension'" -exec grep -l 'some_string' {} +
find . -type f -name \( -name "*.'some_extension'" -o -name "*.'some_extension'" \) -exec grep -l 'some_string' {} + 

#Find all files without the given extension that contain the given string
find . -type f ! -name "*.'some_extension'" -exec grep -l 'some_string' {} +
{% endhighlight %}
<br/>

# Searching/Manipulating Strings
{%highlight bash %}
#Finding and replacing a string in all the files in the current directory
sed -i "s/'some_string_to_replace'/'some_string_to_replace_with'/g" *

#Split a string based on a delimiter and print it
echo "*'some_delimeter'*" | awk -F "'some_delimeter'" "{print $1}"
{% endhighlight %}
<br/>

# Miscallaneous
{% highlight bash %}
#Finding PIDs of a give process
ps -ef | grep 'some_process_name'

#Capture packets coming into/going out of a machine and save it to file
tcpdump -i any -s0 -w 'some_file_name'

#Finding name of process that is using a given port
netstat -na | grep 'some_port_number'
{% endhighlight %}




