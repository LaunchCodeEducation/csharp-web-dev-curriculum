---
title: "Exercises: Exceptions"
date: 2023-02-08T10:27:25-06:00
draft: false
weight: 4
originalAuthor: <no value> # to be set by page creator
originalAuthorGitHub: <no value> # to be set by page creator
reviewer: # to be set by the page reviewer
reviewerGitHub: # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

You will find the starter code for the exercises in the [csharp-web-dev-exercises](https://github.com/LaunchCodeEducation/csharp-web-dev-exercises) repo in the `Exceptions` project.

## Divide By Zero!

The professor you TA for, Professor Jackson, shared with you the code she uses to auto-grade students’ work. She and the other TAs have encountered some problems with the code in the past when they enter the total possible point value for an assignment. Occasionally, they accidentally enter `0` for the total number of possible points and the program encounters a fatal error when trying to divide by 0.

To help out with this issue, complete a function called `Divide()` in `Program.cs`.

   - The `Divide()` method takes in two parameters: `x` and `y`.
   - Your function should return the result of x/y.
   - However, if y is zero, you should throw an exception, such as `ArgumentOutOfRangeException`.

{{% expand "Check your solution" %}}

```csharp
   static double Divide(double x, double y)
   {
      if (y == 0.0)
      {
         throw new ArgumentOutOfRangeException("y", "You cannot divide by zero!");
      }
      else
      {
         return x / y;
      }
   }
```

{{% /expand %}}