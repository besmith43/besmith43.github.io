---
title: Building Custom Profiles
date: 2020-02-01 08:00:00 +0900
categories: [ powershell ]
tags: [  ]
---

#### What is PowerShell

PowerShell started life as a Windows native alternative to bash or unix shell.  It was built with the also Microsoft designed .Net Framework using the C# language.  It was first introduced in Windows XP.  Now in 2020, we have PowerShell version 5.0 and 5.1 in Windows 10, and PowerShell Core that is crossplatform and built with .Net Core.  This shell has the ability to automate nearly everything that you\'d like a computer to do, but in order to do that, you\'ll need to make yourself at home with this shell.  Customization is the best part of bash and other unix shells, and everyone\'s shell is different.  Even though they have the same pieces to start with.  Likewise what you\'ll see here in my profiles, I have goals and actions that the profile needs to meet.  You\'ll need to use PowerShell for awhile to see what you want from it, but my goal is to walk you through a method to setup your own customizations while following the dry programming methodology.

#### Where to Place the Profile

With there being 2 different versions of PowerShell and it being available on at least 3 different operating systems, file placement is paramount to getting things to work as expected.  With version 5 (the Windows only version), the profile needs to be placed at **~\Documents\WindowsPowerShell** with the name of **Profile.ps1**.  While the Core version needs to be placed at different places depending on the operating system.  Because of this I use the PowerShell profile variable of **$profile** to allow PowerShell to place the file where ever it needs to go for the platform I\'m on at the moment like so.

```powershell
if (!(test-path -itemtype file -path $profile))
{
    new-item $profile -force
}
```

This will set a blank file at the specific location for your platform.  For Windows, this location is **~\Documents\PowerShell** and the file name is **Microsoft.PowerShell_profile.ps1**.  Why they do the naming convention like this I have no idea, but with Linux the location is **~/.config/powershell** and the same file name.  Please note that all of these detailed locations only place the profile file where it will be loaded under your user account.  If you\'d like to have a profile that runs for all users on the machine please reference the [Microsoft Documentation](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_profiles?view=powershell-7).

#### Now that it\'s placed, what do I do with it

For anyone who has used and customized a Unix environment, this is easy, but for the average Windows user that doesn\'t need to use the command line on a daily basis, it\'s just a blank file and no idea what to put in it.  Basically we\'re just going to start filling it with every custom function, alias, or module import that we want to have available everytime that you open PowerShell.  This process is mostly discovery as you find more things that you want to do consistantly and easily or as you find more things that PowerShell can do.  I have a blank file setup that you can download to get started [here](https://github.com/besmith43/Blank-PWSHRC).

#### Looking at the components

If you downloaded my blank profile setup, you\'ll notice that it is far more than one file.  That is because I like to separate concerns.  For example, there is a aliases.ps1, and functions.ps1.  Both of these files should contain only their namesakes.  This way when you need to go back and add something new or modify something, you\'ll have a precise place to go to.  This is the base concept of maintainability and one that will save you a lot of headaches in the future.  To get started, the setup is currently hard coded to be stored at **~\Documents\PWSH**.  You can change it to where ever you\'d like as you get more comfortable with PowerShell and how it works, but for now just place the PWSH folder into your Documents folder.  Then from a powershell prompt, run the following command **~\Documents\PWSH\install.ps1**.  This will place the PowerShell version 5.0 profile where it needs to go if you\'re on Windows, and the PowerShell Core profile where it needs to go.  These 2 files do nothing but point back to the PWSH folder and more specifically the **pwshrc.ps1**.  This script then imports the others at startup of a new shell.  The **programs.ps1**, **modules.ps1**, and **variables.ps1** files are currently set as I have them on my personal machines so that you can see what this level of automation can look like, while the **aliases.ps1** and **functions.ps1** files are basically blank.  At the end of this article I\'ll have my full setup available for download as it maybe helpful to see and use a unified setup to get a feel for what is possible.

[My PowerShell Profile](https://github.com/besmith43/PWSHRC)

