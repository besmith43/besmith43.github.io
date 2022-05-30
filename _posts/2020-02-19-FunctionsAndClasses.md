---
layout: post
title: Functions and Classes
date: 2020-02-19 08:00:00 +0900
category: python
---

#### Functions
Programming can be oversimplified by saying that it is organizing repetative tasks that manipluate data into small containers.  This is the point of abstractions.  This particular example of abstractions is what we call a function.  In Python, the keyword for declaring a function definition is "def", followed by the name of the function, parentheses, and ending with a colon.  Inside the parentheses, you can put an unlimited number of parameters.  These parameters are bits of data that your function will perform operations on.  You also have the ability to return one value back from a function with a "return" statement.  One question that you may be asking yourself, is what go through all of this work?  Why segment instructions so that you can\'t start at the beginning and work through to the end sequentially?  The answer is both easy and difficult to answer.  The short answer is that you may have the same instructions lined up the same way to perform the same task on different data multiple places in the code.  If you find a bug or need to change some of these instructions later on, would you prefer to find each occurance of that code to make the same modification, or go to a function definition and modify it once?  The lazy among you will go with option 2 immediately, and the rest should get used to that idea as well.  The reason being is that in large code bases (this being defined in some cases and millions of lines of code) finding and modifying each and every reoccurance of what should be a function can be an impossible task.  This is part of a design paradigm in programming called "Dry Programming".  The base idea is that your code base is structured such that code blocks are only written once.  But that\'s enough explaination, let\'s see some example code.

```python
def add(a, b):
	c = a + b
	return c
```

This example is really simple.  It takes the parameters, a and b, and adds them together, stores the result into the variable c, and returns it.  This can be rewritten to be simpler.

```python
def add(a, b):
	return a + b
```

The eagle eye\'d among you will realize that I\'ve removed the temporary storage of the addition\'s result in c and just have that as returned from the function straight away.  This can be done because just like in math, there is an order of operations when you have multiple things happening in the same line of code.  In this particular example, the addition happens before the return statement is processed.  Now let\'s see how we\'ll use this function after it has been defined.

```python
d = 5
e = 3
f = add(d, e)
```

Note firstly that the variable names used in the declaration don\'t need to be the same as the variables passed in when the function is called.  The only thing that matters is that the type of data is correct for the operations that a function needs to perform.  This is something that we\'ve seen a little of before, but will get deeper into at a later date.

#### Classes
Classes are the next level of organization.  They are a method of controlling access to data and functions so that not everything can modify data or call functions that should only be used in particular circumstances.  To define classes, it follows the same rules as a function in terms of white space rules.  However using them is a little different.  With classes, you need to make an instance of it.  That instance has it\'s own data, and you can make multiple instances of the class with different data in each.  For example, we can have a class of person.  Each instance of person has a first and last name, and an age.  However the data stored in each instance of person is different just like every real person doesn\'t have the same name and isn\'t the same age.  Let\'s see how this class definition looks in Python code.

```python
class Person:
	def __init__(self, first, last, age):
	self.first = first
	self.last = last
	self.age = age
	
def getFullName(self):
	return self.first + " " + self.last
	
def getAge(self):
	return self.age
```

In the example, we\'re doing a couple of things.  Firstly, we start the class declaration block and give the class a name.  Then we define a function called __init__.  This is a special kind of function called a Constructor.  A constructor is called anytime a new instance of a class is made.  The parameters to this function are self, first, last, and age.  The first parameter may look a little odd, because the idea of the keyword self, is literally that you are passing the instance of the class to itself.  This isn\'t explicitedly necessary, but in Python 3 to use self, you need to pass it in as a parameter in the definition.  This does not need to be done when you call the function as we\'ll see later though.  Now the next bit is the important part of the constructor.  It is assigning the parameters to variables inside the instance of the class.  It does this by using what is called dot notation.  Meaning that what is on the right of the dot is a part of the object on the left of the dot.  As stated before, the names of the variables don\'t have to be the same, but for readability, it doesn\'t hurt in this instance.  Next you\'ll see that we have 2 functions.  One that returns the person\'s age, and one that returns the person\'s full name.  Note that in the getFullName function, there is 2 oddities.  The first is that we\'re adding strings together.  This is permissible in Python as it interprets this form of addition as string concatenation, or combining strings together.  The second is that we have to add a space or what will be returned from the function is the first and last name mashed together.  No one wants that.  Now let\'s look at how we use this class is some code.

```python
p1 = Person("Jane", "Doe", "26")

print(p1.getFullName)
```

The first line of the example is the creation of an instance of the Person class, and it is stored in the variable p1.  The second line is a print function that writes to the screen the return statement of p1\'s getFullName function.  Now there is a concept in most languages that pertains to classes of public and private.  Each language does it a little differently but the basics are the same.  A class function or variable is by default public.  This means any code can call an instance\'s functions or modify it\'s variables.  If you don\'t want the functions or variables to be able to be called or modified by code outside of the instance, then those parts of the instance need to be set to private.  Now the question is how does Python do this.  Well any variable or function within a class that you want to be private, add a double underscore to the name.  For example this is how we would change the variables from our previous example to make them private.

```python
class Person:
	def __init__(self, first, last, age):
	self.__first = first
	self.__last = last
	self.__age = age
	
def getFullName(self):
	return self.__first + " " + self.__last
	
def getAge(self):
	return self.__age
```
	
#### --classes.py--
```python
# defining the class named Person
# it has 3 parameters that each instance of the class will need
# first name, last name, and age

class Person:
    def __init__(self, first, last, age):
        self.__first = first
        self.__last = last
        self.__age = age

    # declaring a public function that returns the full name of the instance of the class
    def getFullName(self):
        return self.__first + " " + self.__last

    def getAge(self):
        return self.__age

# creating an instance of the class
# we can do this as many times as we have people that we want to make a class instance for

p1 = Person("Jane", "Doe", 26)

# prints the full name of the individual

print(p1.getFullName())
print(p1.getAge())

try:
    print(p1.__first)
except:
    print("calling the __first variable failed")
```

#### --functions.py--
```python
# define function add
# parameters are a, and b.  They are assumed to be numbers
# the function returns the sum of the 2 parameters added together

def add(a, b):
    return a + b

# running code

d = 5
e = 3

# calls the add function and stores the result into the variable f

f = add(d, e)

# prints out the result stored in f

print(f)
```

	
[Github Repo](https://github.com/besmith43/Py_FunctionsAndClasses)




