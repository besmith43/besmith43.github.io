---
title: Vim All the Things
date: 2022-05-30 08:00:00 +0900
categories: [ vim ]
tags: [  ]
---

#### What is Vim?
Vim is a modal text editor.  One of the things that makes this complicated user interface great is that it allows the user to capitalize on letting the computer do alot of work for you while keeping your hands on the keyboard's home rows as much as possible.  It's a command line application by design and therefore doesn't come out of the box with support for a mouse.  Thus you can't/shouldn't need to leave the keyboard to select something with your mouse.  As you get more used to this workflow, it becomes very difficult not to want to use this same modal and keyboard approach to using the computer with everything like web browsers, file browsers, email clients, and all kind of other applications.

#### What are the advantages of using Vim?
As an IDE (or Integrated Development Environment), it is endlessly customizable.  That goes for everything from what keybindings trigger what actions, to custom actions, to having actions run automatically based on predefined environmental conditions.  Vim allows you to put work into configuration and get real world benefits where the only limitation is your willingness to work at it.  For example, I have set a custom function that will build the current project that I'm working on.  This is a feature of any IDE so it's nothing special and the fact that vim doesn't have this out of the box should be a negative point against it.  Right?  To me, absolutely not.  I got to build the build system so that it works the why I want it to, and can handle whatever build process I want.  Not what the IDE's designers had in mind.  It also allows me to embed my own assumptions into the development environment.  So for example, if I wanted to have a custom run.sh script to handle special builds, all I have to do is add in an if statement to check for a run.sh file, and of it exists, run it.  Is this possible in normal IDE's?  Probably.  But that vim spends its development time on supporting the plugin ecosystem and making the experience of editting text as good as it can, they aren't wasting time trying to handle every usecase possible.  That becomes the job of each user trying to use vim.  It can grow and change as you do, when you want it to and how you need it to.  Not how the devs think you should.

#### Is Vim Really Faster?
As you get better, the answer is most certainly yes.  However, that will take some time to achieve.  I'll use myself as an example.  I've been using vim on and off for the last 4 years.  I'm learning new things all the time and have achieved various levels of speed increases during that time.  Though I'm still very much new to the whole thing at the end of the day.  So far I've got vim configured pretty much on par or better than any IDE that I've tried, vifm (aka vim file manager) in the extreme early stages of adaption, and vimari (vim like extension for Safari) and vimium (another vim  like extension for Chrome, Firefox, and Edge).  The only missing application to get the vim treatment is my email client but as Apple's mail app and Outlook are rather large applications in their own rights, I don't think I'm going to try and shoehorn in vim keybindings into them.

#### Concluding Thoughts
I encourage you to watch some videos on youtube and get a feel for how it works.  Once you get over the beginning stages, it can be a work life changing experience.  I just realized that I forgot about the macro system entirely, but that's alright because I entend to have more posts discussing vim, so you'll just have to what and see how that works.



