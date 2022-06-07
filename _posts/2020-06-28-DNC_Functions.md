---
title: Functions in .Net Core
date: 2020-06-28 08:00:00 +0900
categories: [ c# ]
tags: [  ]
---

#### What are Functions?

Put simply, a function is a collection of instructions under a specified name, but what do I mean by that and why should you care?  Well functions serve 2 main purposes in programming.  The first is to group repeated instructions together so that when you need to modify how it works, you don\'t need to make the same modification 15 or more times.  This is referred to as a part of the maintainability of a code base.  The second part is that we can name the collection something meaningful to the task that it\'s performing.  This is referred to as a part of the readability of a code base.<\p>

#### When should I use a Function?

Now some people will tell you that if you are writing more than 4 lines of code, it should be in a function.  I\'ve heard it before and I understand the idea behind it, but I find that determining when to and when not to use a function is down to 2 things: the complexity of the code, and the bulk of it.  For example, if there is a couple lines of code that don\'t immediately make sense when I look at it, I\'ll put it into a function so that I can name the action being taken.  Even if the code is only used once.  That way, I know exactly where a chunk of code is when I need to modify it, but also so that I can abtract that complexity away and replace it with an easily understood name.  Another name is when it\'s simply alot of code.  I\'ll put that into a function or several functions so that I dont have to at line after line of code, but instead easily disgustable function names.  One of the things that you may have noticed is that I\'m talking about the naming portion of functions quite a bit, and you\'d be right.  Part of the complexity of programming is the organization that it takes to set the order of operations properly to achieve the desired effect, but also to manage that complexity through abstracting it away into easier to flow chucks.  As projects get larger, it is beneficial to be able to trust your abstractions and keep the eagle\'s eye view in your head as opposed to having to keep each and every detail.

#### How do I make a Function?

This part is pretty easy.  There are 2 parts of a function: the function declaration, and the body of the function.  The body of the function is something that we\'re already familiar with as it is a curly brace, {}, with lines of code inside just like the loops that we\'ve dealt with already.  The function declaration, on the other hand, is made up of 5 parts: the scope of who can use the function, the type of function that it is, the return type, the function name, and the parameters.  For the scope, at the moment everything will be public, but a function can be private, or protected, and we\'ll look at what those mean when we look at classes.  The type of function will be important later but for now they\'ll be static functions.  The return type is what type of value does the function return.  This could be an integer, or a string, but in the event that it doesn\'t return a value, then the return type is void.  The function name is just that.  Its name.  The parameters are the values that it needs to do its job.  Now keep in mind that the names of the parameters only matter within the function as we declare it.  Because of this, you don\'t need to worry about what the variables are named when you\'re calling the function.

#### -- Program.cs --

```c#
using System;

namespace DNC_Functions
{
    class Program
    {
        static void Main(string[] args)
        {
            int num1 = 3;
            int num2 = 5;

            int num3 = add(num1, num2);

            Console.WriteLine($"The total is {num3}");

            int answer = getUserChoice();

            Console.WriteLine($"You chose {answer}");
        }

        public static int add(int a, int b)
        {
            return a + b;
        }

        public static int getUserChoice()
        {
            int choice;

            Console.WriteLine("Pick a number between 1 and 10");
            string user_input = Console.ReadLine();

            try
            {
                choice = Int32.Parse(user_input);
            }
            catch
            {
                choice = 0;
            }

            return choice;
        }
    }
}
```

[Github Repo](https://github.com/besmith43/DNC_Functions)

