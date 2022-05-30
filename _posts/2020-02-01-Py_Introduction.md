---
layout: post
title: Introduction to Python Programming
date: 2020-02-01 08:00:00 +0900
category: python
---

#### What is Python
Python is a scripting language that is cross-platform and can be used for anything from automating small tasks to production web servers.  It is a wonderfully easy language to learn and is designed to be readable.  Python is basically suedocode, and it makes for quick development.  In fact, I like to use it as a prove of concept to test ideas that I have.  It works by running your text file with the .py extension through a parser and then an interpreter.  This interpreter compiles the contents into python byte code, and then to platform specific machine code to be run on the processor.  The downside of Python and why one want to use it for everything is that Python is slow and predominantly single threaded.  This is because of the use of a GIL, or Global Interpreter Lock.  Meaning that each instance of the Python Interpreter can only run one thread of code logic at a time.  It can splice in as many of these threads as the programmer would like, but ultimately they are sharing the interpreter.  Therefore if your application needs to be fast and multithreaded, then a compiled language should be used for the finished product.  This type of discussion is a matter for another day.
	
#### How to get Python
The Python interpreter can be installed for your platform by going to their [website](https://www.python.org/downloads/).  However you\'ll need to pick between version 2 and 3.  Version 2 has been used in business projects for years and maintained to keep them from having to update their applications for version 3.  However it is becoming end of life, and it is highly adviced that any new projects use version 3.  Once downloaded, run the installer and you\'ll be ready to go.  Now something to keep in mind, and this goes especially for Windows, is that you\'ll need to make sure that the binary is within your System Path.  With the installer, there is a checkbox for it.

#### Now that you have Python Installed, how do you use it
Python comes with more than just the interpreter.  It includes a shell, which allows you to type in your code line by line and see the output in real time.  This can be incredibly useful as you\'re trying to learn the language and how it works.  However once you have a .py file and are ready to test your creation, simply open a command line, terminal shell, or PowerShell and navigate to your .py file.  Then run the following command: **python .\_your-filename_.py** along with any additionally arguments that it needs.  Let\'s get started with something simple.  Create a new blank file.  Name it **test.py**.  Then in your preferred text editor, write **print("Hello World")**.  Then save the file and close the text editor.  Finally run **python .\test.py** in your terminal application and press enter.  You should see a new line with the output <var>Hello World</var>.  You\'ve just successfully made your first Python application.  Next time, we\'ll make something a little more impressive than a simple hello world application, but in the meantime look up the [documentation](https://docs.python.org/3/) and see all the wonderful [applications](https://en.wikipedia.org/wiki/List_of_Python_software#Applications) made using the power of Python.




