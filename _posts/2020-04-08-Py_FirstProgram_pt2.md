---
layout: post
title: First Python Program Part 2
date: 2020-04-08 08:00:00 +0900
category: python
---

#### Arguments
What are arguments?  Simply put they are paramters (options) that are given to the application at the time that it\'s called to be run.  We\'re going to use a built in Python Library called ArgParse to implement a new feature to make this application a little more useful to anyone use plays Dungeons and Dragons.  So let\'s take a moment to look at what ArgParse gives us, and why we need it.  Passing in arguments gives our program the ability to be more flexible in it\'s use at runtime.  For example, with our dice rolling application, DnD requires the use of 7 different dice.  These are 4, 6, 8, 10, 12, 20, and 100 sided dice.  However while we also want to give the user a default setting as well.  This library gives us the ability to do all of this and more.  It\'s all down to how we use it.

#### Implementation
Now to implement a solution, we\'ll need to start by importing ArgParse.  Fortunately it\'s a library that is bundled with the base install of Python, so we don\'t need to install it separately.  Now that we have it imported, we can use the library.  To use the library, we\'ll need to add the following code between the imports and the random number generation from the first part.

```python
parser = argparse.ArgumentParser()
parser.add_argument(\'-s\', \'--sides\', default=20, choices=[4, 6, 8, 10, 12, 20, 100], type=int, help="Number of sides on the dice to be rolled")
args = parser.parse_args()
sides = args.sides
```

Let\'s look at what this code does.  So the first line creates a command line parser and stores it into the variable named "parser".  Then we have the longest line of code yet that defines an argument to be searched for in all of the arguments given to the application.  Now what it does with all of the parameters is set a default value of 20, names the variable and stores the value passed in at "sides", sets a short name of "s", sets the available options to the defined list of numbers that we need, mandates that the value be stored as an integer, and sets a help message.  This is alot, but at the end of the day it is pretty much does exactly what one would think that it does.  The third line of code, has the parser calling a function to actually parse the arguments given at runtime and store them into the variable args.  Then we take the one stored value from args and store it in the variable "sides".  After this, you\'ll need to edit the random number generator code to use sides in place of 20.

#### Conclusion
Once you make these changes, you should be able to run the application 2 different ways.  The first being the default roll a 20 sided dice: **./dice.py**.  Then the second is by selecting a different dice either with the long name or the short name like so: **./dice.py --sides 8** or **./dice.py -s 8**.

#### -- dice.py --
```python
#!/usr/bin/env python3

import random
import argparse

parser = argparse.ArgumentParser()
parser.add_argument(\'-s\', \'--sides\', default=20, choices=[4, 6, 8, 10, 12, 20, 100], type=int, help="Number of sides on the dice to be rolled")
args = parser.parse_args()
sides = args.sides

result = random.randint(1, sides)

print()
print()
print(result)
print()
print()
```
        
        
[Github Repo](https://github.com/besmith43/Py_FirstProgramPt2)



