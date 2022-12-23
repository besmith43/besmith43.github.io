---
title: Cross Compiling Rust on a MacBook
date: 2022-06-18 08:00:00 +0900
categories: [ rust ]
tags: [ rustup, cross compile ]
---

#### Rustup

The main tool for installing rust tools!  With it, we can install new "toolchains".  Basically, the parts of the rust compiler needed for platform specific compilation.  Unfortunately, because of the way that rust compiles our code into a binary, it needs the appropriate C libraries to be able to produce the final binary that we'll run on a client computer.  In this post, we'll discuss how to setup your MacBook to target several prominent architectures and platforms.

#### Quick Refresher on Compiling Programs in Rust

Rust is an llvm based language and what that means is that the rustc compiler compiles our rust source files down to llvm-ir.  IR in this context stands for intermediate representation.  Then the normal llvm compilers take that output and compiles it down to architecture specific assembly.  Once it becomes assembly, a linker goes through, links all the files together and then compiles it down to both a platform and architecture specific machine code that we refer to as a binary.  This binary file is our application in a runnable state that we can distribute to others.

#### Installing Rustup

Firstly we'll need to get rustup install on our MacBook.  This can be done by going [here](https://rustup.rs), and running the command they have in your terminal.

#### Mac x86

Now that we have Rustup installed, let's look at the simplest target for cross compiling our rust programs, Intel equipped Macs.  First we'll need to install the rust toolchain for it with the following command:

```bash
rustup target add x86_64-apple-darwin
```

Now we have everything installed, and we just need to tell cargo to use the new tooling.  To do so for each build run cargo like so:

```bash
cargo build --target x86_64-apple-darwin
```

However that is a lot to type every time and we like being lazy.  So how can we tell cargo to build a particular project without having to type in the target option every time?  Make a config file.  This file needs to be in a .cargo folder within the same directory as the Cargo.toml file, and you'll need to put the following text in a config file within it.

```
[build]
target = "x86_64-apple-darwin"
```

To test that these compiles actually worked, let's make use of the file command.  In case you aren't already familiar with it, the file command will tell you what kind of file you pass it.  When it comes to binaries, it will tell us the cpu architecture and operating system that a binary was compiled for.  We can use file to check our binaries with the following:

```bash
file ./target/x86_64-apple-darwin/debug/<program binary>
```

We should get the following output:

```
target/x86_64-apple-darwin/debug/<program binary>: Mach-O 64-bit executable x86_64
```

The next thing to do would be to move this file to an Intel processor equipped mac and run it.

#### Windows x86

What most have probably come here for, let's up the difficulty to one of the most common platforms, Windows running on Intel and AMD processors.  To get started, you'll need to install mingw-w64.  I personally use [Homebrew](https://brew.sh).  With it, I can run the following command to install mingw-w64:

```bash
brew install mingw-w64
```

Then we'll need into install the rust toolchain.  To do that run the following:

```bash
rustup target add x86_64-pc-windows-gnu
```

Then to compile the program with the following:

```bash
cargo build --target x86_64-pc-windows-gnu
```

Like with the Intel Macs, we can make a config file if the project needs to default to build for the Windows x86 platform.

```
[build]
target = "x86_64-pc-windows-gnu"

[target.x86_64-pc-windows-gnu]
linker = "x86_64-w64-mingw32-gcc"
```

This config file is telling cargo that the build process needs to use the Windows options and that the linker is mingw32's version of gcc.  Now you don't have to use the build section, but the linker section is required.  Otherwise, cargo will give you an error that effectively means that it doesn't have a compile toolchain to compile for the Windows platform.

Now to check that the binary created shows as a Windows file.  The file command's output should look something like the below.

```
target/x86_64-pc-windows-gnu/debug/<program binary>.exe: PE32+ executable (console) x86_64, for MS Windows
```

#### Windows Arm64

As of the time of writing this, rustc doesn't have a toolchain for arm64 Windows gnu.  It only has a toolchain for arm64 Windows msvc.  Msvc is the Microsoft Visual C compiler.  It's a series of libraries and tools to build Windows native progresses.  It's also a runtime library that needs to exist on a client system.  However, mingw is the gnu project's open source and non-Microsoft C compiler that we can use on MacOS and Linux to make Windows binaries.  Until the toolchain is built to target Windows on arm64 within rust using mingw, we have to make Windows on arm64 binaries natively on Windows.

#### Linux (Both Arm64 and x86)

For Linux, we build both arm64 and x86 Linux binaries from our Macs without the need for a virtual machine just like we did with Windows x86 binaries.  To get started, we'll need to install compilers, and again I'm using homebrew to do this.

```bash
brew tap messense/macos-cross-toolchains

brew install x86_64-unknown-linux-gnu

brew install aarch64-unknown-linux-gnu
```

Where this differs from before with Windows, you'll need to add the following 4 lines to your shell's configuration files.

```bash
# needed to compile for x86 architecture
export CC_x86_64_unknown_linux_gnu=x86_64-unknown-linux-gnu-gcc
export CXX_x86_64_unknown_linux_gnu=x86_64-unknown-linux-gnu-g++
export AR_x86_64_unknown_linux_gnu=x86_64-unknown-linux-gnu-ar
export CARGO_TARGET_X86_64_UNKNOWN_LINUX_GNU_LINKER=x86_64-unknown-linux-gnu-gcc

# compile rust applications for arm64 linux
export CC_AARCH64_unknown_linux_gnu=aarch64-unknown-linux-gnu-gcc
export CXX_AARCH64_unknown_linux_gnu=aarch64-unknown-linux-gnu-g++
export AR_AARCH64_unknown_linux_gnu=aarch64-unknown-linux-gnu-ar
export CARGO_TARGET_AARCH64_UNKNOWN_LINUX_GNU_LINKER=aarch64-unknown-linux-gnu-gcc
```

Now like before we need to install the appropriate rust toolchains like so:

```bash
rustup target add x86_64-unknown-linux-gnu

rustup target add aarch64-unknown-linux-gnu
```

Following these commands, we can build applications for Linux operating systems on both arm64 and x86 cpu architectures out of our rust projects.  This can be done with the cargo build options.

```bash
cargo build --target x86_64-unknown-linux-gnu

cargo build --target aarch64-unknown-linux-gnu
```

You can also do the .cargo/config file with the following content:

```
[build]
target = "x86_64-unknown-linux-gnu"
```

For the file commands outputs, they should look something like the following examples:

```
target/x86_64-unknown-linux-gnu/debug/<program binary>: ELF 64-bit LSB pie executable, x86_64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 2.6.16, with debug info, not stripped

target/aarch64-unknown-linux-gnu/debug/<program binary>: ELF 64-bit LSB pie executable, ARM aarch64, version 1 (SYSV), dynamically linked, interpreter /lib/ld-linux-aarch64.so.1, for GNU/Linux 3.7.0, with debug info, not stripped
```

#### Checking the Assembly and LLVM-IR

One of the fun things that cargo can do is output the assembly code and LLVM-IR that it generates to a file.  This can be a good way to debug, if that becomes necessary, or to compare our cross compilation work.  To output those intermediate formats to file, you can use the following commands:

```bash
cargo rustc -- --emit asm

cargo rustc -- --emit llvm-ir
```

The output of these commands are stored in \<program-name\>.s and \<program-name\>.ll files respectively and are found at `target/x86_64-pc-windows-gnu/deps`.  When you look for a build on the native platform, you'll need to look at `target/debug/deps` for the same assembly, llvm-ir, and binaries we've discussed all throughout this article.

#### Conclusion

This is a solid start to cross compilation with rust from a Mac.  One last bit of wisdom is to use rustup to list all of the install toolchains on a system.

```bash
rustup target list
```

Enjoy your new found knowledge of Rust!

#### Reference Links

[Stack-Overflow: cross compiling from macos to windows with rust](https://stackoverflow.com/questions/70058542/cross-compiling-from-macos-to-windows-not-working-with-rust)

[Github Gist: Mefistophell](https://gist.github.com/Mefistophell/9787e1b6d2d9441c16d2ac79d6a505e6)

[Rustup Book: Toolchains](https://rust-lang.github.io/rustup/concepts/toolchains.html)

[Rustup Book: Components](https://rust-lang.github.io/rustup/concepts/components.html)

[Github: Messense/homebrew-macos-cross-toolchains](https://github.com/messense/homebrew-macos-cross-toolchains)

[Stack Overflow: how can i cross compile rust code into intel assembly on an arm m1 apple silicon](https://stackoverflow.com/questions/68139162/how-can-i-cross-compile-rust-code-into-intel-assembly-on-an-arm-m1-apple-silicon)

[Patrik Svensson: targeting arm for windows in rust](https://patriksvensson.se/posts/2020/05/targeting-arm-for-windows-in-rust)

