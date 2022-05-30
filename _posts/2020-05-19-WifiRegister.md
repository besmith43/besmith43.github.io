---
title: Wifi Register
date: 2020-05-19 08:00:00 +0900
categories: [ python ]
tags: [  ]
---

#### Problem
The internet has become and important part of modern life, and with that comes the persistent question from house guests: "What\'s the wifi password?"  It can be annoying both as the host and the guest.  Now some people will simply post their wifi password within sight of the door so that there\'s no need to ask.  However let\'s see what programming can do for us?

#### Proof of Concept
So let\'s look at how Windows manages wifi profiles.  This can be seen using the command line.  So pull up an administrative console, and run the following command: **netsh wlan show profiles**.  
![an image]({{ site.baseurl }}/assets/img/py-netsh-show-profiles.png)  
For my laptop, it only has my home network so that makes it pretty simple.  Now I just need to export it to a file with the following command: **netsh wlan export profile \"NERD HOUSE_5G\" key=clear folder=C:\\**.  This will put an xml file at the root of your C drive, and this xml file contains all the information for your wifi connection that Windows stores.  Now that we\'ve exported it, we\'ll need to add the contents of this file to a python script so that it can write that data to a file, then call CMD or powershell to import it onto another computer.  To do this, we\'ll need to start a new python file with a shebang, an import statement for the os library, and the open function to create a new file of a given name in write mode.

```python
#!/usr/bin/env python3

import os

file = open("home-wifi.xml","w")
```

Then open the xml file, select all of it\'s contents, copy them, and paste them into the python script file.  Now before each line of the xml\'s data, we\'ll need to write **file.write("**, and end each line with **\n")**.  This is rather tedious but lets see what we\'re actually doing with this.  So file is the name of the variable that we named earlier for a new file.  The .write is calling a write function to place the text passed to the function into the file.  At the end of each line we\'re adding a \n then closing the double quotes and parathesises.  But what is this \n?  Well it is a carriage return.  It is a special symbol that means new line.  Now we need to close the file by putting in **file.close()**.  The final section of code will get the current path, call powershell to run the proper command to import our xml file, and delete the xml file.

```python
cur_path = os.getcwd()
os.system(\'powershell.exe netsh wlan add profile filename="\' + cur_path + \'\home-wifi.xml"\')
os.remove("home-wifi.xml")
```

So how does this code work?  We know what it is supposed to do, but let\'s break it down a bit.  We\'re storing the current working directory, or cwd, into the variable cur_path.  It\'s done by calling the os library module and using one of its functions called getcwd().  Then we\'ll use the os module again but call the system function.  This function is how we interact with the host operating system.  In this case, we\'re calling powershell, and telling it to run the command **netsh wlan add profile**.  The plus sign in this instantance isn\'t performing arithmetic addition but instead it\'s performing string concatentation.  So what\'s a string you may be asking?  Well it is a type of data that is a series of characters.  It also doesn\'t have a specific length.  Finally after powershell finishes running, the next line of code will execute.  In this case, that is the os module deleting the home-wifi.xml file that we spent so much time working with already.

#### Solution
Now that we have a functional proof of concept for Windows, how about MacOS or Linux?  Also how are we going to package this so that we can give something simple to our guests?  Well, let\'s start off by making everything we\'ve done so far a part of a function called **def Run_Windows():**.  Then we\'ll have to figure out how to do the same for MacOS and Linux, but also how do we have python check which platform we\'re on?
        
#### MacOS
For MacOS, we need to make a bash script by calling **file = open("home-wifi.sh","w")**, and fill it with the following.

```bash
#!/bin/bash
    
networksetup -setairportnetwork en0 SSID_OF_WIRELESS_NETWORK WIRELESS_NETWORK_PASSPHRASE
```

Now here SSID_OF_WIRELESS_NETWORK is the name of your wifi, so like in Windows, mine was NERD HOUSE_5G.  The WIRELESS_NETWORK_PASSPHRASE is the password.  Now we can write this content into our home-wifi.sh file in a single command, like so.

```python
file.write("#!/bin/bash\n\nnetworksetup -setairportnetwork en0 SSID_OF_WIRELESS_NETWORK WIRELESS_NETWORK_PASSPHRASE")
```

Now we need to close the file, make it executable, run the script, and then delete it.  This can be done with the below python instructions.

```python
file.close()
cur_path = os.getcwd()
os.system("chmod +x " + cur_path + "/home-wifi.sh")
os.system(cur_path + "/home-wifi.sh")
os.remove("home-wifi.sh")
```

The new bits here are things like making it executable, and how we\'re running the command.  Where with windows, we used powershell to run the command.  In MacOS, we are using the shebang to have MacOS determine to run our script through bash, or the bourne again shell.

#### Linux
For Linux, we\'ll be doing the same thing, but changing the command used in the bash script.

```bash
#!/bin/bash
    
iwconfig wlan0 essid NETWORK_NAME key WIRELESS_KEY
```

For this command, NETWORK_NAME is the name of your wifi, and WIRELESS_KEY is the password.

#### Determining What is the Current Operating System
So to determine, what the current operating system python is running on, we\'ll need the sys module.  Specifically the platform function of the sys library.  We\'ll use the below code block to run the correct function.

```python
import sys
    
cur_os = sys.platform()
    
if cur_os == "win32":
    Run_Windows()
elif cur_os == "darwin":
    Run_MacOS()
elif cur_os == "linux":
    Run_Linux()
else:
    print("this is an unsupported operating system")
```

#### Conclusion
Finally, we need to use pyinstaller to make the script into an executable.  Now with pyinstaller, the script will need to be feed to pyinstaller on a computer of each operating system.  That is its major limitation.  However once, completed, you\'ll have a single file that can be dropped onto any guest computer and run to add your wifi to a guest computer.  Realistically speaking this isn\'t the most practical thing, but if you have a complex password or need to setup wifi onto a large number of computers like in a business environment.  This type of solution can be quite handy.
        
####--register-wifi.py--
```python
#!/usr/bin/env python3

import os
import sys

def Run_Windows():
    file = open("home-wifi.xml","w")

    file.write("<?xml version=\"1.0\"?>\n")
    file.write("<WLANProfile xmlns=\"http://www.microsoft.com/networking/WLAN/profile/v1\">\n")
    file.write("	<name>Nerd House_5G</name>\n")
    file.write("	<SSIDConfig>\n")
    file.write("		<SSID>\n")
    file.write("			<hex>4E65726420486F7573655F3547</hex>\n")
    file.write("			<name>Nerd House_5G</name>\n")
    file.write("		</SSID>\n")
    file.write("	</SSIDConfig>\n")
    file.write("	<connectionType>ESS</connectionType>\n")
    file.write("	<connectionMode>auto</connectionMode>\n")
    file.write("	<MSM>\n")
    file.write("		<security>\n")
    file.write("			<authEncryption>\n")
    file.write("				<authentication>WPA2PSK</authentication>\n")
    file.write("				<encryption>AES</encryption>\n")
    file.write("				<useOneX>false</useOneX>\n")
    file.write("			</authEncryption>\n")
    file.write("			<sharedKey>\n")
    file.write("				<keyType>passPhrase</keyType>\n")
    file.write("				<protected>false</protected>\n")
    file.write("				<keyMaterial>xxxxxxxx</keyMaterial>\n")
    file.write("			</sharedKey>\n")
    file.write("		</security>\n")
    file.write("	</MSM>\n")
    file.write("	<MacRandomization xmlns=\"http://www.microsoft.com/networking/WLAN/profile/v3\">\n")
    file.write("		<enableRandomization>false</enableRandomization>\n")
    file.write("		<randomizationSeed>2955902897</randomizationSeed>\n")
    file.write("	</MacRandomization>\n")
    file.write("</WLANProfile>\n")

    file.close()

    cur_path = os.getcwd()
    os.system(\'powershell.exe netsh wlan add profile filename="\' + cur_path + \'\home-wifi.xml"\')
    os.remove("home-wifi.xml")


def Run_MacOS():
    file = open("home-wifi.sh","w")

    file.write("#!/bin/bash\n\nnetworksetup -setairportnetwork en0 Nerd\ House_5G xxxxxxxx")

    file.close()

    cur_path = os.getcwd()
    os.system("chmod +x " + cur_path + "/home-wifi.sh")
    os.system(cur_path + "/home-wifi.sh")
    os.remove("home-wifi.sh")

def Run_Linux():
    file = open("home-wifi.sh","w")

    file.write("#!/bin/bash\n\niwconfig wlan0 essid Nerd\ House_5G key xxxxxxxx")

    file.close()

    cur_path = os.getcwd()
    os.system("chmod +x " + cur_path + "/home-wifi.sh")
    os.system(cur_path + "/home-wifi.sh")
    os.remove("home-wifi.sh")



cur_os = sys.platform()

if cur_os == "win32":
    Run_Windows()
elif cur_os == "darwin":
    Run_MacOS()
elif cur_os == "linux":
    Run_Linux()
else
    print("This is an unsupported platform")
```

[Github Repo](https://github.com/besmith43/Py_RegisterWifi)




