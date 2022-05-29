---
layout: post
title: First Python Program Part 3
date: 2020-04-11 08:00:00 +0900
category: python
---

#### Reorganization
In this third part, we\'re going to add a graphic user interface option.  This is where things will leave the command line and start looking like applications that most people are accustomed to.  So to start we\'re going to reorganize the code.  This is done for 2 reasons.  The first is readability and maintainability.  This may sound like 2 different things, but as your projects get larger and larger, you\'ll find that they become very much the same thing.  Ultimately what we\'re looking for is a balance between performance, and simplicity.  As you try to optimize projects for performance, it tends to get harder to understand what is actually going on and why.  Therefore we need to make sure that code remains readable so that we can reason through what is the goal that is being accomplished and how is the code going about reaching that goal.  The second reason why we need to reorganize the code base is that we don\'t want to lose any functionality, but we don\'t want to needlessly waste time calling code that won\'t get run.

So first things first.  How do we start reorganizing the code?  I tend to start by looking at what I want to do, and the basic structure that the application needs to run through.  This is case our application will have 2 distinct paths.  The first is the command line option that we\'ve already done.  The second is the graphical user interface or gui that we want to add to it.  Now both paths will still need to call our random number generator code, and we\'ll want to same options for both, so we\'ll need to add an additional command line option for rolling multiple of the same kind of dice, and one for chosing the gui option.

After adding the necessary command line arguments, we need to turn some parts of out code base into functions.  For example, the code that we use to generate a random number can be turned into a stand alone function so what it can be called as needed like so.

```python
def roll(sides):
	return random.randint(1, sides)
```

We\'ll need another function to be the command line logic.

```python
def cmdcall(sides, times):
	count = times
	result = 0
	
	while(count != 0):
		result += roll(sides)
		count = count - 1
	
	print()
	print()
	print(result)
	print()
	print()
```

Finally before looking at the gui code, we\'ll need to change the base method by which the application runs to call these new functions and others that we haven\'t made yet.  This will go after the command line argument parser.

```python
if (gui_flag):
	guicall()
else:
	cmdcall(sides, times)
```

#### Graphical User Interface
GUI\'s are the primary way that we interface with our computers.  Fortunately for use there is one that comes with python that is a great primer for getting used to programming gui applications.  There are basic components called widgets that we can use to fill the window.  Some of these widgets are things like Labels, SpinBoxes, Progress Bars, and Text Boxes.  The library that we\'ll be using is called TKinter.  It is a Python only library, but it works on all platforms that Python runs on.

To get started with actually building a gui application, we\'ll need to import the library and use 2 lines of code to get a basic blank gui.  That code looks like this.

```python
from tkinter import *

window = Tk()

window.mainloop()
```

Let\'s take a look at these lines of code.  The first is an import statement, but it\'s a little unlike any that we\'ve used before.  Basically we\'re importing all sublibraries of the main tkinter library.  In the second line of code, we\'re initializing the base gui class and assigning it to the variable window.  This is important because we\'ll be referencing this variable for everything that we do to build out the interface.  Finally we have last line of code that actually runs the gui.  Something to make note of here is a basic difference between utility software and user interface software design is this concept of a mainloop.  It is literally in some cases a while loop that checks for various updates and then updates the interface until the application is closed.  Everything up to this point has been finite where we start the program, it runs through a set number of instructions, and then ends.  However with this loop, it can truly go forever.

So now that we have this basic but empty interface, let\'s define a starting size for the window and put some widgets into it.  We\'ll need 5 of them.  They\'re going to be 2 labels (so our user knows what each option is going to do), a combobox to pick the dice that you want to roll, a spinbox to pick the number of dice that need to be rolled, and a button to trigger the rolling of the dice.  It\'s a large code block, but ultimately each part goes like this.  First part, declare the widget and give it some information.  The second part is to place it on the grid based on column and row.

```python
window.geometry(\'350x80\')

sideslabel = Label(window, text="Number of Sides: ")

sideslabel.grid(column=0, row=0)

combo = Combobox(window)

combo[\'values\']= (4, 6, 8, 10, 12, 20, 100)

combo.current(5) #set the selected item

combo.grid(column=1, row=0)

timeslabel = Label(window, text="Number of times to be rolled: ")

timeslabel.grid(column=0, row=1)

spininitvalue = IntVar()

spininitvalue.set(1)

spin = Spinbox(window, from_=1, to=10, width=1, textvariable=spininitvalue)

spin.grid(column=1,row=1)

btn = Button(window, text="Roll Dice", command=lambda: clicked(combo, spin))

btn.grid(column=1, row=2)
```

There are 2 things to point out in this code that breaks the mold.  The spinbox needs an initial value.  The second is that when initializing a button you need to give it a command.  This command is the function that you want to be called when the button is clicked.  However most functions need parameters passed to them.  For the tkinter library button to have a function called with paramters, you need to declare the function as a lambda.  It\'s a relatively unimportant thing at the moment.  Just know that lambda\'s are a huge topic in itself.  We\'ll explain them later as they can be incredibly useful but it is anything but simple.  What remains at this point to have a functioning program is to implement the clicked function that we told the button to call.  Let\'s take a look at that function.

```python
def clicked(combo, spin):
	sides = combo.get()
	times = int(spin.get())

	result = 0
	count = times

	while(count != 0):
		result += roll(int(sides))
		count = count - 1

	messagebox.showinfo(\'Dice Roll Results\', \'A D\' + sides + \' was rolled \' + str(times) + \' times with a result of \' + str(result))
```

Now when the button is clicked, the clicked function will be called.  It will roll the dice with the right number of sides and the right number of times.  Then it will make a message box that will tell you the dice that was rolls, the number of times that it was rolled and the sum total of the rolled dice.  Because of the message box, and the combo box we need to add 2 more import statements.  The reason for this is that we need to explicitly import the messagebox, and the combo box doesn\'t come from the root library.

```python
from tkinter import messagebox
from tkinter.ttk import *
```

#### Conclusion
Now we have an application that when run with the following command: **.\dice.py -g** will give us the the below application.  However we can still use the command line functionality without all the need for the gui if we so chose.  From here, you have the ability to build next to any application that you can imagine.  There\'s many more topics to discuss, but these are all the basic tools that you need to be productive.  Enjoy your new found powers and play responsibly. 

![image]({{ site.baseurl }}/static/img/py-firstprogram_pt3-conclusion.png)


#### -- dice.py --
```python
#!/usr/bin/env python3

import random
import argparse
from tkinter import *
from tkinter import messagebox
from tkinter.ttk import *

def roll(sides):
    return random.randint(1, sides)

def clicked(combo, spin):
    sides = combo.get()
    times = int(spin.get())

    result = 0
    count = times

    while(count != 0):
        result += roll(int(sides))
        count = count - 1

    messagebox.showinfo(\'Dice Roll Results\', \'A D\' + sides + \' was rolled \' + str(times) + \' times with a result of \' + str(result))

def cmdcall(sides, times):
    count = times
    result = 0

    while(count != 0):
        result += roll(sides)
        count = count - 1

    print()
    print()
    print(result)
    print()
    print()

def guicall():
    window = Tk()

    window.title("Dice Roller")

    window.geometry(\'350x80\')

    sideslabel = Label(window, text="Number of Sides: ")

    sideslabel.grid(column=0, row=0)

    combo = Combobox(window)

    combo[\'values\']= (4, 6, 8, 10, 12, 20, 100)

    combo.current(5) #set the selected item

    combo.grid(column=1, row=0)

    timeslabel = Label(window, text="Number of times to be rolled: ")

    timeslabel.grid(column=0, row=1)

    spininitvalue = IntVar()

    spininitvalue.set(1)

    spin = Spinbox(window, from_=1, to=10, width=1, textvariable=spininitvalue)

    spin.grid(column=1,row=1)

    btn = Button(window, text="Roll Dice", command=lambda: clicked(combo, spin))

    btn.grid(column=1, row=2)

    window.mainloop()


parser = argparse.ArgumentParser()
parser.add_argument(\'-s\', \'--sides\', default=20, choices=[4, 6, 8, 10, 12, 20, 100], type=int, help="Number of sides on the dice to be rolled")
parser.add_argument(\'-t\', \'--times\', default=1, type=int, help="Number of dice to be rolled")
parser.add_argument(\'-g\', \'--gui\', action=\'store_true\')
args = parser.parse_args()

gui_flag = args.gui
sides = args.sides
times = args.times

if (gui_flag):
    guicall()
else:
    cmdcall(sides, times)
    
```


[Github Repo](https://github.com/besmith43/Py_FirstProgramPt3)

<iframe width="560" height="315" src="https://www.youtube.com/embed/NwMr_Pf3NPU" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


