## Research

The main outcomes of this exercise are to understand the following:
* How do I navigate the file system?
* How do I combine commands together?
* What do I need to know to write a script file?

Please use the questions as a guide to your research. Consult our [resources document](./resources.md) for some useful links, and use the internet!

Don't worry if you don't get through all the questions. If you do, try the extension questions.

### Group 1
#### 4. How do I navigate the file system?
* How do I find out my current directory, change directory, and list files within my directory?
* What is the difference between the home directory and the root directory?
* What is the difference between ./ and / and ~/?
* What’s the $PATH? (also, what does `which <cmd>` do?)
* Imagine you've created a new script file named `script.sh`. You now need to run it. Why will typing `script.sh` not work, when `./script.sh` does?
* What are some useful shortcuts for navigating quickly on the command line?

Extension:
* What are the common locations for different files? Hint: look up FHS
* Can you think of any Guardian specific locations? (e.g. `./gu` VS `/etc/gu`)
* Are there any commands that can help you find particular files?
* Are there any commands that can help you find particular lines within files?

### Group 2
#### 5. How do I combine commands together?
* `cat file.txt | grep sport | wc -l` - What is this command doing? (Hint: look up 'pipes')
* What is the difference between piping and redirecting?
* What are the three ‘standard streams’?
* How can we perform commands conditionally?
* How can we repeat commands?
* What are exit codes?
* What are some useful shortcuts for navigating quickly on the command line?

Extension:
* Explain what the following commands are for:
  * sed
  * awk
  * tr
  * cut


### Group 3
#### 6. What do I need to know to write a script file?
* What is the purpose of a script file?
* How does my shell know to interpret a file as a script file? (shebang)
* What permissions does a file need to be executable?
* What settings can I apply when running a script file?
  * eg. What do set -e, set -u, set -x do?
  * How do you unset a setting?
  * How many other settings can you find? What do they do?
* How do I define variables in bash?
* How do I pass arguments from the command line?
* How do you access those arguments from inside the script?

Extension:
* What effects do single quotes, double quotes and backticks have?
* How do I write a bash function?
* What is the difference between `NAME=value`, `local NAME=value` and `export NAME=value`?
