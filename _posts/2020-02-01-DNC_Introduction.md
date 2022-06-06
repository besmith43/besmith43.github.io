---
title: Introduction to .Net Core Programming
date: 2020-02-01 08:00:00 +0900
categories: [ c# ]
tags: [  ]
---

#### What is .Net Core

.Net Core is an extension of the .Net Framework that is designed first and formost to be cross-platform.  It makes building command line programs and websites easy on the major desktop and server platforms (Windows, Linux, and MacOSX).  It has recently started breaking into GUI\'s, or Graphic User Interface, with the introduction of WinForms to .Net Core 3.0.  However this is only on Windows, and cannot be used on the other .Net Core available operating systems.  There do exist other projects such as Avalonia to bridge this gap and give a single design process to make .Net Core Gui\'s truly cross-platform.

#### Why should I use .Net Core

As previously stated, .Net Core is designed and supported by Microsoft to bring a subset of the .Net Framework to all major platforms.  This means that if you are a .Net Framework developer, you can get up to speed with the changes, and start building command line utilities in an afternoon.  Because of the JIT, or just-in-time compiler, aspect to .Net, .Net Core gives you the ability to compile complete binaries from all the supported platforms from any of the supported platforms.  Meaning that if you only have a Windows computer, you can still release binaries for Linux and MacOSX without having to maintain virtual machines or purchase dedicated hardware to run those platforms.  This is unique when compared to most compiled languages such as C, C++, or until recently GoLang.  Java has always had this ability, so .Net Core is by far not the first to do it.  However with .Net Core being completely open source, it invites the community to mold it into the framework that they need it to be.  Not just what Microsoft wants it to become.

#### How do I get .Net Core

It can be downloaded by going to [Mircosoft](https://dotnet.microsoft.com/download/dotnet-core) directly, or their [Github](https://github.com/dotnet/core) page.  Once it\'s downloaded, simply run the installer and you\'re ready to go.  If you are on Linux, I suggest adding the repository if possible so that you are always on the latest version.  Instructions for this process can be found [here](https://docs.microsoft.com/en-us/dotnet/core/install/linux-package-manager-ubuntu-1904).

