---
title: Variables in .Net Core
date: 2020-05-26 08:00:00 +0900
categories: [ c# ]
tags: [  ]
---

#### What are Variables?

Variables are the containers that we use as programmers to store information.  That information can be as simple and small as a number or a character to as large as a game engine or movie with everything inbetween.  Let\'s look at some of the primitive variable times.

#### What are the different types of variables?

Firstly let\'s explain what primitives are.  In computer science, primitives are the simplist data types available.  These data types are variable types like Integers, Characters, Floats, Doubles, Booleans, Strings, and Arrays.  This isn\'t necessarily all primitives, but these are alot of the common ones.  So let\'s look at each one of them.

* **Integers:** These are whole numbers that can be zero or negative.

* **Doubles:** These are decimal numbers such as 3.5 or 5.0.

* **Floats:** These are doubles with a higher level of precision such as 3.5000005.

* **Booleans:** This variable type is just true or false.  The perfect example of simplicity.

* **Characters:** These are individual letters, numbers, or special characters.

* **Strings:** These are a series of characters, typically an array of characters.

* **Arrays:** These are an ordered collection of a singular datatype.

#### Strongly Typed vs Weakly Typed

"What is all of this strong and weak stuff?" you may be asking.  Well it is a simple explanation that comes with a very long conversation.  Quickly put, strongly typed variables are variables that have to be declared at the point that it is created and will never be changed for the life of that object.  Therefore a variable that is declared to be an integer will only hold integers until the variable is deleted.  You\'ll never be able to put a letter into this integer variable.  However in a weakly typed language, you don\'t need to declare the variable type at the point of creation because the variable can have a string when it\'s created, and later store an integer.  C# is a C based language and because of that a variable will get declared at creation and remain so until it\'s deleted.  C# does come with a nice keyword to skill having to write alot of variable declaration.  That keyword is var.  With var, when a function returns a value, you can declare a new variable with var as the data type and then you as the programmer don\'t need to write a long variable datatype.

