---
title: First Python Program
date: 2020-04-07 08:00:00 +0900
categories: [ python ]
tags: [  ]
---

#### Goal

Every program starts with an idea.  That idea is normally based around how to solve a problem.  For the first program, it\'s going to sound like alot and it is.  However we\'re going to take it in steps.  So let\'s start with the problem.  Make a program that will simulate a dice roll.  In this first step, we\'ll make a few assumptions.  Firstly we only want to roll a d20 or a 20 sided dice and output the result each time that program is run.
        
#### Implementation

To start get started, we\'ll need to get a blank file.  Once you have that done, you\'ll need to put the SheBang at the top of the file.  What is a SheBang you ask?  It is **#!/usr/bin/env python3**.  What does this do?  It tells your computer to look at /usr/bin/env to figure out what the interpreter is to run the file.  The space python3 is an argument for the program env to evalutate.  All of this is the same as typing **python3 ./dice.py**, but instead you can just do **./dice.py**.  Now this SheBang is a historically Unix thing, that Windows doesn\'t understand, but it works on Windows too.
Now you can start the actual python code.  First you\'ll need to import the random library.  Then you\'ll need to call the function random.randint(1, 20).  The parameters that we\'re passing to it are 1 and 20, which are start and stop points for the random number generator.  Additionally it\'ll need to store that into a variable.  Finally output the contents of the variable with the print statement.

#### Conclusion

This is a pretty simple idea, but we\'re going to build on this in the next post.  However try to read through the Goal and Implementation sections, then make your own implementation and compare it to mine.

#### -- dice.py --

```python
#!/usr/bin/env python3

import random

result = random.randint(1, 20)

print()
print()
print(result)
print()
print()
```

[Github Repo](https://github.com/besmith43/Py_FirstProgramPt1)

