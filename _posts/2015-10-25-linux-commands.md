---
layout: default
title:  Linux Commands 
date:   2015-10-25 12:52:23
categories: linux 
---

<h1>Finding Files</h1>

<b>Find all files with the given name</b>: 
{% highlight bash %}
find -name 'some_file_name'
{% endhighlight %}  

<b>Find all files that don't match the given name</b>: 
{% highlight bash %}
find -not -name 'some_file_name'  
{% endhighlight %}

<b>Find all files that contain the given string</b>: 
{% highlight bash %}
find . -type f -exec grep -l 'some_string' {} +  
{% endhighlight %}

<b>Find all files with the given extension(s) that contain the given string</b>: 
{% highlight bash %}
find . -type f -name "*.'some_extension'" -exec grep -l 'some_string' {} +
find . -type f -name \( -name "*.'some_extension'" -o -name "*.'some_extension'" \) -exec grep -l 'some_string' {} + 
{% endhighlight %}


<b>Find all files without the given extension that contain the given string</b>:
{% highlight bash %}
find . -type f ! -name "*.'some_extension'" -exec grep -l "some_string' {} +
{% endhighlight %}

<br/>

<h1>Searching/Manipulating Strings</h1>
<b>Finding and replacing a string in all the files in the current directory</b>:
{% highlight bash %}
sed -i "s/'some_string_to_replace'/'some_string_to_replace_with'/g" *
{% endhighlight %}

<b>Finding and replacing a string in all the files in the current directory + subdirectories</b>:
{% highlight bash %}
#TODO
{% endhighlight %}

<b>Split a string based on a delimiter and print it</b>:
{% highlight bash %}
echo "*'some_delimeter'*" | awk -F "'some_delimeter'" "{print $1}"
{% endhighlight %}

<b>Printing the first string in the second row</b>:
{% highlight bash %}
echo "some_string" | awk "NR==2 {print $1}"
{% endhighlight %}
<br/>