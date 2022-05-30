---
layout: post
title: Branching in .Net Core
date: 2020-06-28 08:00:00 +0900
category: c#
---

#### Branching
What is branching?  Basically it is the name give to the broad classification of operations that a computer uses to make decisions.  Because a computer can really only move where data is stored and arithmetic, branching is decision making through arithematic.  Essentially the computer takes 2 pieces of data, say for example 3 and 5, and subtracts 3 from 5.  Then it looks a some special flags based on the result, and finally choices to go down path A or path B.

#### If/Else
In dotnet core and most programming languages, there are a few basic keywords to be familiar with for most decision making needs.  The first and maybe the most used is If/Else.  This does exactly what you would expect.  If the statement is true, do what is within the If block, but if the statement is false, do what is within the else block.  Let\'s take a look at a simple example.

```c#
if (3 < 5)
{
    Console.WriteLine("3 is less than 5");
}
else
{
    Console.WriteLine("3 is greater than 5");
}
```

Let\'s take a look at what\'s happening in this code snippet.  Effectively, the processor is being asked is 3 less than 5?  The processor then does some arithmetic and decides that it is a true statement.  Because it is true, the code with the first curly bracket is run and everything below that is skipped.  If some whatever reason the laws of math changed and 3 became greater than 5 or the numbers order was switched, then the code within the curly bracket pair under else would be run and the first pair would be skipped.  Now this example isn\'t very useful as it is what\'s called hard coded.  This means that the decision will never change as it will always be a true statement.  There are times when you would want such a thing but not with if statements.

There is another keyword to be familiar with when it comes to If/Else statements, and that is the "else if" statement.  This works exactly as you\'d expect, but let\'s see it in a more realistic situation.

```c#
int a = 3; 
int b = 5; 

if (a < b) 
{ 
    Console.WriteLine($"{a} is less than {b}"); 
} 
else if (a > b) 
{ 
    Console.WriteLine($"{a} is greater than {b}"); 
} 
else 
{ 
    Console.WriteLine($"{a} and {b} are equal");
}
```

Here we\'re seeing a code snippet that when executed will output **3 is less than 5**, because it again entered the first if statement.  It will do this everytime because 3 will always be less than 5 and that comparison will happen before the other 2 are checked.  It is suggested to always have an else, but it is not mandatory.  You can also use as many else if\'s as you need to take care of the decision tree that you need to.  It is also acceptible to embed if\'s within if\'s.  However I would be careful as you want to make sure that you keep your code easy to reason through.

#### Switch
Much like If/Else, switch statements are effectively a specific If/Else decision tree.  With a switch, it is given a single variable, and then depending on the value stored within that variable, a particular code block is selected, and if it is not any of the specific options, it is good coding practice to have a default code block.  This default is the switch equivalent of an else statement.  Each code block is ended with a break keyword.  This keyword can be used in any code block to stop the flow of execution of that code block.  We\'ll discuss this further in a later post.

```c#
int choice = 2; 

switch (choice) 
{ 
	case 1:
		Console.WriteLine("The Choice was 1"); 
        break; 
    case 2: 
        Console.WriteLine("The Choice was 2"); 
        break; 
    default: 
        Console.WriteLine("The Choice wasn\'t 1 or 2"); 
        break; 
}
```

#### While Loops
While loops ae pretty simple but incredibly useful.  At the top of the loop is a condition check, then the block of code to be run as long as that condition is true.  Let\'s take a look at one.

```c#
int count = 0; 
 
while(count < 5) 
{ 
	Console.WriteLine($"The count is {count}"); 
	count++; 
}
```

Sometimes you need to go through the code block once before the condition check happens.  To accomplish this, you can use a do while loop.  Basically you\'ll start the code block with a do keyword instead of the while keyword and condition, and finish the code block with the while keyword and condition statement.

```c#
int count = 0; 
 
do 
{ 
	Console.WriteLine($"The count is {count}"); 
	count++; 
} while(count < 5);
```

#### For Loops
For loops are a concise way to interate a defined number of times.  Like with the previous while loop examples, there is a defined format to be followed.  It works by declaring a new variable, then setting the truth condition, and then the modification operation that needs to happen between each loop.  Seeing is simpler than explaining.

```c#
for(int i = 0; i < 5; i++) 
{ 
	Console.WriteLine($"The count is {count}"); 
}
```

#### Foreach
Up to this point all of the different loop examples have done the same thing.  They\'ve outputed a sentence 5 times with the current count.  A ForEach loop can do this same thing but in a fundamentally different way.  Before we had a variable keeping up with a count that got updated at the end of each loop.  However a ForEach loop, it will iterate over a collection of items.  An example of this would be to have an array of items, and perform the instructions given in the code block on each of them.  This can be a handy way to work with a a collection of items in a unified fashion.

```c#
int[] numbers = new int[] {0, 1, 2, 3, 4}; 

foreach (number in numbers) 
{
	Console.WriteLine($"The count is {number}"); 
}
```

#### Conclusion
This is an introductory list of some of the most commonly used branching instructions used in programming.  Keep in mind that all of them can be used interchangably, but they are each geared differently.  I encourage you to play with each of them and get familiar with them.


#### -- Program.cs --
```c#
using System;

namespace DNC_Branching
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("If/Else Statement\n");

            int a = 3;
            int b = 5;

            if (a < b)
            {
                Console.WriteLine($"{a} is less than {b}");
            }
            else if (a > b)
            {
                Console.WriteLine($"{a} is greater than {b}");
            }
            else
            {
                Console.WriteLine($"{a} is equal to {b}");
            }

            Console.WriteLine("\n\nSwitch Statement Block\n");

            int choice = 2;

            switch(choice)
            {
                case 1:
                    Console.WriteLine("the Choice is 1");
                    break;
                case 2:
                    Console.WriteLine("The Choice is 2");
                    break;
                default:
                    Console.WriteLine("The Choice was not 1 or 2");
                    break;
            }

            Console.WriteLine("\n\nWhile Loop\n");

            int count = 0;

            while (count < 5)
            {
                Console.WriteLine($"The count is {count}");
                count++;
            }

            Console.WriteLine("\n\nDo-While Loop\n");

            count = 0; // can't redeclare a variable, so I am just resetting the value to zero

            do
            {
                Console.WriteLine($"The count is {count}");
                count++;
            } while(count < 5);

            Console.WriteLine("\n\nFor Loop\n");

            for (int i = 0; i < 5; i++)
            {
                Console.WriteLine($"The count is {count}");
            }

            Console.WriteLine("\n\nForEach Loop\n");

            int[] numbers = new int[] {0, 1, 2, 3, 4};

            foreach (int number in numbers)
            {
                Console.WriteLine($"The count is {number}");
            }

            Console.ReadLine();
        }
    }
}
```

      
[Github Repo](https://github.com/besmith43/DNC_Branching)



