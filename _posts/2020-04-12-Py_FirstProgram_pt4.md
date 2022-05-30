---
layout: post
title: First Python Program Part 4
date: 2020-04-12 08:00:00 +0900
category: python
---

#### Distribution
One part of software development that is the hardest is distributing your finished product to your friends, family, and hopefully customers.  There are many ways to accomplish this is python but today, let\'s look at PyInstaller.  It is a wonderful project that seeks to bundle python scripts with the interpreter and their dependencies into a executable that can be run by others without the need to install python like you did for development.  Before we can use PyInstaller, we\'ll need to install it.  This can be done by using the following command on the commandline: **pip install pyinstaller**.  This will use the pip python package manager to install the module onto your computer.  Once it is done, you\'ll simply need to go to the folder that your script resids in, and run the following to bundle it: **pyinstaller --onefile .\dice.py**.  Before running this command, your folder should look like this.
![image]({{ site.baseurl }}/assets/img/py-firstprogram_pt4-before_pyinstaller.png)
After running the command, it should look like this.
![image]({{ site.baseurl }}/assets/img/py-firstprogram_pt4-after_pyinstaller.png)
Now you may be asking yourself, what are all these new things?  It is a perfectly reasonable question to ask, and another good question would be where is the executable?  Let\'s just say that all of the new stuff is necessary to build the executable and go straight to the important bits.  The executable is in the dist folder.  You can take that file and drop it onto anyone\'s computer and they can use your app.  They will need to use the -g flag to get the gui though.  You can rewrite the app to be gui first by default and recompile the executable to make it simpler for your end users.  Or you could use other programmatic solutions like system installers and shortcuts to give it the appearance of just working gui first when actually there are a number of mechanisms operating seamlessly to give such an appearance.  As the programmer the choice is up to you.

[Github Repo](https://github.com/besmith43/Py_FirstProgramPt4)



