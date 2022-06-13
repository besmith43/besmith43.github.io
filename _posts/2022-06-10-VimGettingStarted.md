---
title: Getting Started with Vim
date: 2022-06-10 08:00:00 +0900
categories: [ vim ]
tags: [  ]
---

#### How to Quit?

Because Vim is a modal editor, the first question to answer is how to close it.  It's kind of a meme at this point.  However you can close vim by pressing ":q" followed by the enter key.  This only works if you are in "Normal" mode.  Vim has 4 primary modes: Normal, Insert, Visual, and Command.  Normal is the default mode and the one that you should spend the most time in.  Insert is the mode where the keyboard works like normal and inserts text into your file.  Visual is the mode where you can highlight text to copy or delete the highlighted content.  Command is the mode where you either give Vim commands or the environment.  By pressing the colon while in normal mode, you switch to command mode, and the "q" in the original example is a shortcut for the quit command.

#### Basic Navigation

While keeping within normal mode, you can move around the file without the arrow keys.  The replication of the arrow keys are 'h', 'j', 'k', and 'l' which are left, down, up, and right respectively.  However that's not very different from a normal editor.  So what gives?  This is merely step one on the way to a fully, and I truly mean fully, customizable text editor.

However lets go to step 2 with some more movement commands.  You can press 'w' to jump the cursor forward by a word.  Then there's 'b' to jump the cursor back by a word.  Furthermore, you can search by typing '/' followed by the text that you want to search for.  Then press enter to jump to the first instance below the cursor's current location.  Then you can press '/' and enter to jump to the next one.

#### Insert Mode

With Insert mode, there are alot of different ways to get into it, but the basic way to get into Insert mode press 'i'.  While in insert mode, you can type into your file like you normally would.  Press the escape key to get back to normal mode.  I personally end up remapping escape to my caps lock key on my computers for this reason alone.  I also never use caps lock, so it doesn't tend to bother me much.  Some other ways to get into Insert mode are by using 'A' or 'I'.  These allow you to go into insert mode at the end or beginning of the current line respectively.  There are many other ways to get into and out of Insert mode.  These will get you started until you get more muscle memory.

#### Visual Mode

Visual mode isn't something that I use very often, but it is great when you need it.  I'm still relatively new with vim, as I'm been using it on and off for about 4 years now.  However Visual mode allows you to highlight text.  Once highlighted, you can copy, or delete it.  To delete, you'll need to press the 'd' key, and to copy you'll need to press the 'y' key.  Then to paste, you can press the 'p' key.  However if you have multiple lines selected, you can press shift + 'i' and get into an insert mode that will apply you edits to all selected lines.

#### Conclusion

This is only the beginning of your journey with Vim should you choose to undergo it.  While it takes time and requires more than a fair bit of effort to develop the muscle memory to get up to speed, it is well worth it.  As the old saying goes, anything worth having takes time and effort to obtain.

#### Vim Chart

| Key | Mode | Action |
|----------|----------|-----------|
| h | normal | move the cursor left |
| l | normal | move the cursor right |
| j | normal | move the cursor down |
| k | normal | move the cursor up |
| w | normal | jump the cursor forward by a word |
| b | normal | jump the cursor back by a word |
| i | normal | enter insert mode at the cursor's current location |
| A | normal | move cursor to the end of the line and enter insert mode |
| I | normal | move cursor to the beginning of the line and enter insert mode |
| escape | insert or visual | enter normal mode from insert or visual |
| d | normal or visual | delete character under the cursor or the selected text |
| y | visual | copy the highlighted text |
| p | normal | paste the copied text |
| v | normal | enter visual mode at the cursor's current location |
| : | normal | enter command mode, followed by the command that you'd like to run |
|----------|----------|-----------|

