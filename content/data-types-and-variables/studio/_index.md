---
title: "Studio: Area of a Circle"
date: 2023-01-17T16:28:22-06:00
draft: false
weight: 3
originalAuthor: Sally Steuterman # to be set by page creator
originalAuthorGitHub: gildedgardenia # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: Sally Steuterman # update any time edits are made after review
lastEditorGitHub: gildedgardenia # update any time edits are made after review
lastMod: 2023-07-03 # UPDATE ANY TIME CHANGES ARE MADE
---

To get started, create a new console application in Visual Studio for the studio.

## Calculate the Area of a Circle

Write a program that prompts the user for the radius of a circle.
Calculate the area of the user's circle and print the result.

{{% notice green "Tip" "rocket" %}}

   Recall that the area of a circle is `A = pi * r * r` where `pi` is
   3.14 and `r` is the radius.

{{% /notice %}}

Here’s an example of how your program should work:

```console
   Enter a radius: 2.5
   The area of a circle of radius 2.5 is: 19.625
```

Some questions to ask yourself:

1. What data type should the radius be?
1. What is the best way to get user input into a variable `radius` of
   that type?

{{% notice blue "Note" "rocket" %}}

   Use the `System.Math` class in C# to get the value of pi and square the radius. 
   The [documentation](https://docs.microsoft.com/en-us/dotnet/api/system.math?view=netframework-4.8) has guidance on how to use the `PI` field and the `Pow` method.

{{% /notice %}}

## More Calculations

1. Using the same radius, calculate the circumference (`2*pi*r`) and diameter of the circle (`2*r`).
1. Output the results.

## Road Trip!

1. Ask the user for the miles per gallon of their car. 
1. If the radius that they entered is in miles, output how many gallons of gas they will use to go around this circle. 

## Bonus Missions

1. Think about how we could make this program more modular by breaking out some of the code into a separate class. For example, we could pull out the circle information into a `Circle` class and leave the user questions and console messages in `Program`. Take a look at [the using statement]({{< relref "../reading/some-csharp-practice/index.html#using" >}}) for a refresher on how to reference another class file.
1. Extend your program further by using a [while or do-while loop](https://www.w3schools.com/cs/cs_while_loop.asp), so that when the user enters a negative number they are re-prompted for a radius.
1. Add additional validation to your program. If the user enters a non-numeric character or a empty string? Print an error message and quit. You’ll need to peek ahead to learn about [conditional syntax in C#](https://www.w3schools.com/cs/cs_conditions.asp).