---
layout: default
title:  Linux Commands 
date:   2015-10-25 12:52:23
categories: linux 
---

<b>Find all files with the given name in current + child directories</b>: 
```bash
find . -name 'some_file_name'
```

<b>Find all files with the given name in current directory</b>:
```bash
find . -maxdepth 1 -name 'some_file_name' 
```

<b>Find all files that don't match the given name</b>: 
```bash
find -not -name 'some_file_name'  
```

<b>Find all files that contain the given string</b>: 
```bash
find . -type f -exec grep -l 'some_string' {} +  
```

<b>Find all files with the given extension that contain the given string</b>: 
```bash
find . -type f -name "*.'some_extension'" -exec grep -l 'some_string' {} +
```

<b>Find all files with the given extensions that contain the given string</b>:
```bash
find . -type f -name \( -name "*.'some_extension'" -o -name "*.'some_extension'" \) -exec grep -l 'some_string' {} + 
```

<b>Find all files without the given extension that contain the given string</b>:
```bash
find . -type f ! -name "*.'some_extension'" -exec grep -l "some_string' {} +
```

<b>Find and replace string in all files in the current + child directories</b>:
```bash
find . -type f -name -exec sed -i "s/'some_string_to_replace'/'some_string_to_replace_with'/g" *
```

<b>Compressing directory/files:</b>
```bash
tar -zcvf 'some_file_name.tar.gz' 'some_directory_name' 'some_file_name' 'some_file_name'
#z: compress using gzip
#c: create archive
#v: enable verbose mode
#f: archive file name
```

<b>Split a string based on a delimiter and print it</b>:
```bash
echo "*'some_delimeter'*" | awk -F "'some_delimeter'" "{print $1}"
```

<b>Printing the first string in the second row</b>:
```bash
echo "some_string" | awk "NR==2 {print $1}"
```
