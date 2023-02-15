---
title: "Exercises: Exceptions"
date: 2023-02-08T10:27:25-06:00
draft: false
weight: 4
originalAuthor: Courtney Frey # to be set by page creator
originalAuthorGitHub: speudusa # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
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

## Checking Student Submissions

After mentioning to Professor Jackson that you would like to get some more practice with exceptions, she offered to let you write some grading software! Before she gives you full control over auto-grading students’ work, she asked if you could write a function called `CheckFileExtension()`.

The `CheckFileExtension()` function should do the following:

- Take in one parameter: `fileName`.

- Return an integer representing the number of points a student receives for properly submitting a file in C#.

- If a student’s submitted file ends in `.cs`, they get 1 point.

- If a student’s submitted file doesn’t end in `.cs`, they get 0 points.

- If the file submitted is `null` or an empty string, an exception should be thrown. What kind of exception is up to you!

{{% expand "Check your solution" %}}

This example uses the `ArgumentNullException` to check for student submissions.

```csharp
  static int CheckFileExtension(string fileName)
   {
      if (fileName == null || fileName == "")
      {
         throw new ArgumentNullException("fileName","Student did not submit any work!");
      }
      else
      {
         if (fileName.Substring(fileName.Length - 3, 3) == ".cs")
         {
            return 1;
         }
         else
         {
            return 0;
         }
      }
   }
```
{{% /expand %}}

In `Program.cs`, Professor Jackson has provided a dictionary of students and the names of their submitted files for you to test out your work. If an exception is caught, make sure to print out the error message.