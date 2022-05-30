---
layout: post
title: Break and Continue Keywords in .Net Core
date: 2020-06-28 08:00:00 +0900
category: c#
---


#### Break
Break is a keyword that we\'ve seen already with switch statements previously, but what if I told you that you can use break in any loop?  Well the first question that may come to mind is why would you want to use it in a loop like a for or a while loop?  Additionally you may be asking what does break even do in that context?  Both are good questions and very reasonable reactions as up to this point, we have only talked about break using used to end a selected case from a switch statment.  However in a loop, it ends execution of the loop.  So for example, if we have a while loop that would run 5 times, but add in an if statement that has a break inside its code block, then if the condition for the if statement is true on say the third loop, the while loop would not run the 2 additional times.  This can be very useful to speed up execution by not running needless loops if the purpose of the loop has been accomplished.  Let\'s take a look at what this example would look like in C# code.

```c#
int num = 0;

while (num < 5)
{
	Console.WriteLine("Running contents of while loop");

	if (num == 3)
	{
		Console.WriteLine("If statement is true, and now exiting the while loop");
		break;
	}
}
```

Now in this example we\'re using a new comarison operator that we haven\'t seen before, the equal sign.  So far we\'ve used the equal sign to mean value assignment, however in most programming languages and particular to our purposes this is the case for C#, but a double equal sign is the equal operator.  So the if statement\'s conditional is checking to see if the variable, num, equals 3.  Though the example above is a little pointless, it does demonstrate the utility of the break keyword.  This can be used to break out of an intentional infinite loop, or a variety of other use cases.

#### Continue
Continue is a variation break, so where break exits the loop.  Continue instead ends that current iteration of the loop, and returns to the conditional.  So let\'s say that you wanted to only run a loop on the odd iterations and not the even ones.  One way to accomplish this would be to have an if condition statement that used an arithmetic operation called modulo.  This operation is basically a division operation that returns the remainder and not the quotion of the dvision.  Therefore any iteration that would be evenly divisible by 2 would be even and thus skipped while every odd iteration would not return 0 and be executed.

```c#
for (int i = 1; i < 10; i++)
{
	if (i % 2 == 0)
	{
		continue;
	}

	Console.WriteLine($"{i} is an odd number");
}
```

#### Conclusion
These 2 keywords can be very important when determining the flow of code execution and are useful utilities to have when you need to divert from the normal flow of execution.

	
#### -- Program.cs --
```c#
using System;

namespace DNC_Break_Continue
{
    class Program
    {
        static void Main(string[] args)
        {
            int num = 0;

            while (num < 5)
            {
                Console.WriteLine("Running contents of the while loop");
                num++;

                if (num == 3)
                {
                    Console.WriteLine("If statement is true, and now exiting the while loop");
                    break;
                }
            }

            for (int i = 1; i < 10; i++)
            {
                if (i % 2 == 0)
                {
                    continue;
                }

                Console.WriteLine($"{i} is an odd number");
            }

            Console.ReadLine();
        }
    }
}
```


[GitHub Repo](https://github.com/besmith43/DNC_Break-Continue)



