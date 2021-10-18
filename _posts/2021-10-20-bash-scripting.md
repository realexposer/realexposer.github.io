---
title: "Bash Scripting"
date: 2021-10-20T15:34:30-04:00
categories:
  - blog
tags:
  - 
---
Bash is a powerful Linux terminal application and bash scripting can be used to automate repetitive tasks easily. In this post, we will look at some basic bash scripting.

### Create a script file
```bash
vim temp.sh
```

### Enter the following into that file
```bash
#!/bin/bash
echo “Hello world…”
Sleep 1
echo “How are you?”
read ans
echo “you typed $ans”
```
### Make the script executable
```bash
chmod +x temp.sh
```

### Execute the script
```bash
./temp.sh
```

## How to run a bash script from anywhere
Create a directory say "bin" under your home directory and update your path variable to include this bin directory.  
Include the following in .profile or .bash_profle file to make it permanent.  
```bash
export PATH=$PATH":$HOME/bin"
```
Or use the following if you want the directory to precedent system directories
```bash
PATH=$HOME/bin:$PATH;
```
### create a script say, "hello" and keep it in your bin directory and give execute permission to the hello script.

```bash
#!/bin/bash
echo My first program
```

### From any directory, you simply type:
```bash
hello
```
You will get the following output
```bash
My first program
```