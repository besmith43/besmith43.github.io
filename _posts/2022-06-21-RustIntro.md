---
title: Introduction to the Rust Programming Language
date: 2022-06-21 08:00:00 +0900
categories: [ rust ]
tags: [  ]
---

#### Rust

Let's me be transparent.  Rust is the latest programming language to catch my eye and solve a problem that I was encountering.  As a member of an IT office, it is incredibly helpful to be able to build simple tools to automate common tasks.  However, I'm not exactly in a position to go around installing scripting language runtimes on all the machines that I support so languages like Python and Ruby are out of the question.  I do tend to use them as proof of concept or to handle things on my personal machines.  So for a long time, I had done a significant amount of work in C# to leverage the power of Microsoft's latest iteration of the .Net runtime in the new cross platform .Net Core and later just renamed to .Net.  It was and is a great language and runtime for this effort as I had set the standard that not only did I want to build tools that had no dependencies on the client system, but also that could be built for x86 and arm cpu architectures as well as Windows, MacOS, and Linux from the same dev machine.  .Net Core fit this perfectly because of the amazing work that the Microsoft team had put into it, but as with all good things, there were drawbacks.  .Net didn't allow for files, such as images and text files, to be bundled into the completed binary, and even if it had the Microsoft GUI's didn't work outside of the Windows platform.  For me, the lack of a GUI wasn't a big deal, but if I'm going to give these tools to others, it's ideal to have the interface be a graphical one instead of a terminal one.  So I kept my eye out for other languages and runtimes that would allow these 2 additional checkboxes until rust came on my radar.

Now to actually talk about rust instead of how I got to it.  For my purposes, it can be compiled for all 6 of the target architectures and operating systems I'm looking for, as well as bundling in required files into the completed single binary with no runtime dependencies.  What makes rust a great investment is it's ability to morph from a low-level "systems" programming language to a developer friendly high level language, and all the while having memory safety through use of a borrow checker system.  This is a section of the compiler that enforces a set of rules on your code to verify that you don't have any pointer errors like what you'd find in languages such as C or C++ but without a garbage collector.  This means, among other things, that nothing is pausing execution of your code at runtime to check for memory allocations that need to be freed.  Now don't be fooled by the marketing of the language, it is not safe.  It is merely safer because of these compiler enforced rules.  The reason being is quite simple when you pull it back.  Rust allows those that know what they're doing, or at least think they do, to have direct access to pointers all the problems that come with them through the unsafe keyword.  This is great for library authors and those who need to use rust at lower levels of abstraction relative to the hardware, but for those like me that need to build applications, I get nearly identical performance characteristics to C or C++ without any of their headaches.  I just get the enjoy of all new rustaceans, the name the rust community gave its members, of butting heads with the compiler until I learn the rules through experience.  Something that far more experienced programmers have mentioned that rust is unique to them as they feel that they normally need to take 2 passes at a project to get it right.  However with rust, they feel like they do it the right way the first time due to the compiler and language features.  I personally can say that much, but it definitely is a really confidence building experience with the comfort of the strong type system and the compiler making the computer do what it does best to allow me to focus on the logic and documenting my assumptions in code instead of fritting that the language and runtime are allowing me to misuse something.

#### Rustup and Cargo

Rustup is the main management tool for rust, and cargo is the main build tool.  The 2 together with all their different components make for a wonderful and feature rich platform to get up to speed building applications quickly.  The icing on top is that both can be extended by the community without needing to go through the central authority of the language maintainers.  I'm not saying that because they aren't great, but the modular design of these tools allows for them to focus on core components while the community is allowed to solve their own problems.  Not to compare, but when compared against Microsoft's .Net project, the community is beholden to the problems that Microsoft's team wants to solve.  While they can build on top of that base, nothing stops Microsoft from breaking it.  With rustup and cargo from what I can tell, the core dev teams are only concerned with building out the core functionality and minimum modules to make it work out of the box.

#### Wonderful CLI Tools

Currently rust is being used to create some of the best cli tools I've ever used.  For an example, look at [ripgrep](https://github.com/BurntSushi/ripgrep).  It is one of many bash replacements written in rust, that are far superior to the tools that they're replicating.  In some cases, they're even more user friendly than the original ones written in C.

#### Geared toward helping Beginners

The community and the maintainers are gearing their efforts toward lower the barrier to entry for newbies to the language.  I think that's a great goal and they've done a pretty good job.  You can see for yourself with the following resources below:

[The Rust Language Book](https://doc.rust-lang.org/book/)

[Crates.io](https://crates.io)

[Are We Web Yet](https://www.arewewebyet.org)

[Are We Game Yet](https://arewegameyet.rs)

[Rust Library Search](https://lib.rs)

#### Conclusion

Rust is a great language, and I truly believe that it has a really good shot of hitting its goal of being the programming language for the next 50 years.  They really want to replace C and from it's humble side project roots inside Mozilla to topping the Stack Overflow favorite programming language for the last 5 years, I think it has a real chance at it.
