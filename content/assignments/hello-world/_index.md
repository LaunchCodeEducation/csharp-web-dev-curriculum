---
title: "Assignment 0: Hello, World!"
date: 2023-01-05T09:57:32-06:00
draft: false
weight: 100
originalAuthor: Courtney  # to be set by page creator
originalAuthorGitHub: <no value> # to be set by page creator
reviewer: # to be set by the page reviewer
reviewerGitHub: # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

### Table of Contents
1. Getting Started
1. Running the Auto-graded Tests
1. Your Task
1. Submitting Your Work

Use this assignment as a tutorial for running tests in Visual Studio, working in C#, and submitting to GitHub Classroom. Parts 1 and 2 will help you get familiar with both C# and Visual Studio.  Part 3 is where you will code.  Part 4 reviews the submission process.

## Getting Started
Let’s set up the assignment on our computer and learn about its basic structure.

<!-- TODO: Update Link for Canvas-->
1. Find Assignment #0 in Canvas and click on the invitation link. After accepting the assignment on the Github Classroom page, go to your assignment repository on GitHub.

1. Follow the instructions to clone your repository and open it in Visual Studio.

1. When the solution opens, check out the contents of the Solution Explorer.  You will find two **projects** within the solution:
 
   * The `HelloWorldAutoGraded` contains the code that you will work with for this assignment. 
   * The `Hello.Tests` project contains auto-grading tests. You do not need to change any of the code in the testing project.

   {{% notice blue "note" "rocket" %}}
   If you do not see the **Solution Explorer**, you can open it by selecting the **View** option in the toolbar.
   * Windows Users: **View** > **Solution Explorer**
   * Mac Users:  **View** > **Solution** 
   {{% /notice %}}

1. Inside `HelloWorldAutoGraded`, open up the `SayHelloClass.cs` class.  This is where you will write any code for this assignment.  Within this     class, you will see the following:
   * The `SayHello()` method which is returning `&&&`.
   * `SayHelloClass()` constructor which is empty.  This will remain empty for this assignment.


1. Now, turn your attention to Program.cs in the `HelloWorldAutograded` project. This class will print two strings to the console using the `Console.WriteLine()` method.  
   * The first returns the string value of the `SayHello()` method from the `SayHelloClass`.
   * The second returns the data type of the `SayHello()` method’s output.


1. You are now ready to run the program.  Do the following:
   * **Mac Users:** Hit the Run button at the top right-hand corner of the window.  Right-clicking on the `HelloWorldAutograded` project and selecting Run Project will also work.
   * **Windows Users:** Click on the solid green triangle next to the name of the `HelloWorldAutograded` project. You can also press F5 to run the project.


1. Visual Studio opens a pane and displays any program output when you run a program. Currently, the program output contains the following:
   
   <!-- Note: for console output -->
   ``` console 
   &&&
   System.String
   ```
1. You are ready to run the auto-grading tests.

## Running the Auto-grading Tests

The tests provide feedback about your code before you submit your work.  Use the tests to check your work as you complete the assignment.

The tests are unit tests for you to use to check your work.  We call them auto-graded tests instead of unit tests in these projects. 

Let’s learn how to run the tests in Visual Studio.

1. Each assignment will contain a test **project**.  This project contains all of the auto-grading tests and may have more than one test class.  In the Solution Explorer, navigate to HelloTests.cs inside the `Hello.Tests` project. 

   {{% notice note %}}
   You will not need to open the `Using.cs` file.  This file connects the testing project to the testing library.  This is not a test class.
   {{% /notice %}}

   A test is a single method in a test file with `[TestMethod]` above it. 

   


