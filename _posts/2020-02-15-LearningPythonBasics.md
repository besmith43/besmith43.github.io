---
layout: post
title: Learning the Basics of Python
date: 2020-02-15 08:00:00 +0900
category: python
---

#### What is the Goal of Programming
Previously I stated that Python is basically a functional suedocode.  I believe that as I have used Python for roughly 4 years on various projects.  However before we start learning the language let\'s establish a very high level understanding of what all computer programming seeks to do.  First and foremost, computers are electrified rocks that we have manipluated into having short term and long term memories, and taught to perform 3 basic types of actions at blazing speeds.  Now a days that speed is on the order of billions of times per second per computer core.  The 3 types of actions that we\'ve taught these electrified rocks to perform are arithmetic, branching, and memory management.  Seeings as these are the only operations that a computer has, they are also the only operations that we as programmers have to use.  So we had better understand what they are and why we need them.  Arithmetic is the same 4 math operations that we were taught in elementary school such as addition, subtraction, multiplication, and division.  Branching is decision making done through comparisons with commands given based on the outcome of those comparisons.  Programmers will generally do this with if/else statements, and loops.  Memory management is the simplest of the 3 but the most important, because at the end of the day everything that you see on your computer screen is data that is a representation of a stored number.  At the smallest capacity that stored number is called a bit, a single 1 or 0.  This is physically done by the computer recognizing a voltage below a predefined threshold as 0 and a voltage above that threshold as 1.  Used in groups of 8, we get a byte of data.  This data is known to the computer as a number based on a mathematical power of 2 but to the application using it, it could be a letter or a pointer to another group of data\'s location in system memory.  It all depends on the context of that numbers use in a wider framework of software.  So today, we\'re going to see how Python handles these 3 actions.

#### Arithematic
Performing math in python isn\'t something that you\'ll do very often as you get into higher difficulty applications but for now, it will be common.  Fortunately it is also incredibly easy.  Simply write it out like you would a math problem on paper, and with few exceptions, you\'re be right.  For example, to add 5 and 3, you would write **5 + 3**.  This will work and in the Python Interactive Shell, it will print out the answer of 8.  But we need to place the answer, or result, into a variable before we can use it elsewhere.  Therefore, you can write **c = 5 + 3**.  Then the value stored at the variable c is 8.  Now anytime that we want to reference this value, we simply need to use c.  Likewise we can replace 5 and 3 with a and b respectively, and use them to do the same arithmetic.

```python
a = 5
b = 3
c = a + b
```

Pleae note that in the above code (and this is actual python code), that value assignment is always variable on the left and value on the right of the equals sign.  This is a very important distinction as if you try to assign a value on the left to a variable on the right, you could get errors or very unexpected results.  More over as I\'ve walked you through addition, subtraction, multiplication, and division work the exact same.

```python
a = 5
b = 3
c = a - b
c = a * b
c = a / b
```

In this example, the value of c is overwritten with each statement.  Therefore if you reference c after this chunk of code runs, it will be the division of a / b, or  5 divided by 3.

#### Branching
Branching is commonly referred to as logic.  It is the process of using defined parameters to decide what the next operation performed should be.  This is done through comparisons.  Typically with if/else statements.  For example if we wanted to validate that an addition had been done correctly and if not (else) then print out to the user that it failed, then we could use the following code.

```python
a = 5
b = 4
c = a + b
	
if c == 8:
	print("The addition worked correctly")
else:
	print("The addition failed")
```

Let\'s walk through each step of what we just did and why.  Firstly we assigned a and b to 5 and 3 respectively.  Then we performed the addition of a and b, and assigned that to the variable c.  Nothing new so far.  However next we have an if statement, which begins with the keyword of "if" and ends with a colon.  Inside of that we ca **c == 8**.  Why is there 2 equal signs?  That is done because there are 2 different types of equals.  The first is assignment.  The second is equality.  Basically are the 2 values on either side equaliviant to one another.  If so, the if statement is true and it executes whatever code is inside its code block.  Otherwise it moves on and skips all the code in the code block.  In this case, that would be the else statement.  There are 2 things to note at this point.  The first is that you do not always want or need an else statement.  That is not required as part of the if statement.  Additionaly on this point you may have more than 1 check to do before defaulting to the else statement.  That can be done with an if else statement which in Python looks like this: **elif c < 8:**.  Note that it must end in a colon, and you can even put in multiple comparisons into a single statement with the "and" and "or" keywords like so: **elif c < 8 or c > 8**.  This brings me to the second point.  A code block in many compiled languages is denoted by anything with curly braces, {}.  In Python however white space matters, and a code block is denoted by being tabbed in.  What that means is that after the else statement, Python would see any code not indented as being outside of the else statement\'s code block.  This code would be run regardless of the outcome of the if/else statements and there can be as many lines of code in the code blocks as you need.  However if remaining code is indented, Python will only execute it if the if/else statement chooses to run the else statement\'s code block.  Let\'s see an example of what I\'m talking about.

```python
a = 5
b = 4
c = a + b

if c == 8:
	print("This will only run if c is equal to 8.")
elif c ==0:
	print("This will only run if c is equal to 0.")
else:
	print("This will only run if c is not equal to 8 or 0.")
	print("This will always run regardless of the previous code.")
```

There are many different types of branching operations, but the other most common branching statement is a try/catch statement.  In this bracnhing operation, the computer will try to perform an action, however if an error is thrown, then it will run the catch code block instead.  Let\'s see what that looks like.

```python
try:
	user_number = int(input("Please pick a number between one and ten.\n"))
	except ValueError:
	print("You did not pick a number.")
```

Now as you can see, "try" is the keyword to start the operation, but instead of using catch, the designers of Python decided to use the keyword "except".  Again note that both of the statements end with a colon, and their code blocks are indented to let the Python Interpreter know where they start and stop.  This particular example has lot of new ideas in it, but at the core of what\'s happening is a request for the user to pick a number between one and ten, then if the user inputs something other than an integer, like a character or a string, or even a decimal number, it will run the exception code block.  Now that we know what is intended to happen, let\'s see how we tell Python to do it.  Inside the try code block, there are a few new keywords.  The first is "int".  This is actually what\'s called a function because it takes the remaining code as a parameter inside a set of parentheses, but we\'ll talk about functions some other time.  All that you need to know right now, is that int() will take the result of whatever you put inside the parentheses and output that as an integer.  Therefore the variable "user_number" from the example should always be an integer by the end of this code block provided that no exceptions are thrown.  Inside of int() is the "input" function.  This function takes a string as a parameter, and reads in input from the user.  This is the most basic interaction a program can have with a user.  The string is all the text between the double quotes, and inside that string you\'ll notice that there is a \n.  But "what does that do?" you might ask.  Simply put, it is a special class of character called an escape character.  The backslash is called the escape, and signifies that the next character is special while the n stands for newline.  Therefore the keystrokes that the user puts in will be on a new line in the console instead of appended to the end of the prompt.  Once the user has put in their chosen number, they need to press the enter key, and the program will continue to it\'s execution.

#### Memory Management
This last function is the easiest in Python because you\'ve been doing it this whole time without even thinking about it.  Everytime we place a number into a variable, or assign a string to one, that is the basics of memory management.  Additionally in the try/catch example, when we converted the input functions result into an integer, that was also memory management.  In Python, this process is simple when compared to compiled languages, but is gets far more complex as you get more advanced with your program\'s complexity.  For example, later on there will be variables that can only be accessed by particular means.  Ultimately this is a good thing because it serves to protect data from code that shouldn\'t be messing with it, or ensures that data is only used in certain ways.

#### --basic.py--
```python
var1 = "Hello World"

print(var1)

a = 5
b = 3

c = a + b

print(c)

c = a - b

print(c)

c = a * b

print(c)

c = a / b

print(c)

try:
    user_number = int(input("Please pick a number between one and ten \n"))
except ValueError:
    print("You did not pick a number")

if user_number < 1 or user_number > 10:
    print("You selected a number outside of the requested parameters")
else:
    print("You selected " + str(user_number))
```
	
[Github Repo](https://github.com/besmith43/Py_Basics)


<iframe width="560" height="315" src="https://www.youtube.com/embed/6zEBDU4w4mg" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>



