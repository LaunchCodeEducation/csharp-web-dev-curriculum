---
title: "Assignment 0: Hello, World!"
date: 2023-01-05T09:57:32-06:00
draft: false
weight: 100
originalAuthor: Courtney  # to be set by page creator
originalAuthorGitHub: speudusa # to be set by page creator
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

   {{% notice blue "Note" "rocket" %}}
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

   {{% notice blue "Note" "rocket" %}}
   You will not need to open the `Using.cs` file.  This file connects the testing project to the testing library.  This is not a test class.
   {{% /notice %}}

   A **test** is a single method in a test file with `[TestMethod]` above it. 

      ```csharp
      [TestClass]
      public class AutogradingTests
      {
         [TestMethod]
         public void TestToDemonstrateWhatATestMethodLooksLike()
         {
            //test code here
         }
      }
      ```

      A test class may contain many tests. 


      ```csharp
      [TestClass]
      public class AutogradingTests
      {
         [TestMethod]
         public void TestToDemonstrateWhatATestMethodLooksLike()
         {
            //test code here
         }

         [TestMethod]
         public void SecondTestToDemonstrateWhatATestMethodLooksLike()
         {
            //test code here
         }
      }
   ```
1. Run all of your tests using the Test Explorer window.
   1. Mac Users: 
      1. **View** > **Tests**  
      1. Select the green triangle on the left of the Test Explorer. 
      1. Step through the solution until you find the test that failed. 
      1. [Guide](https://learn.microsoft.com/en-us/visualstudio/mac/testing?view=vsmac-2022#running-tests) to running tests in Visual Studio for Mac
   1. Windows Users 
      1. **Test** > **Windows** > **Test Explorer**
      1. Select the `Run All` icon to run all of your tests. 
      1. In the Test Explorer, step through your solution until you find the failed test.
      1. [Guide](https://learn.microsoft.com/en-us/visualstudio/test/run-unit-tests-with-test-explorer?view=vs-2022) to running tests in Visual Studio.


1. Visual Studio opens a Test Pane to display test results every time it runs a test. 
You should see that one of the tests has failed and the other passed.  We have not touched any code yet. Use the Test Pane to navigate into which specific test has failed.

   In this case, the `TestIfSayHelloReturnsCorrectValue()` test, expected our code to output `Hello, World!` Instead, it provided `&&&` causing it to fail.  This particular test has a message about why it failed.  `&&&` is not the correct message.

   The `TestSayHelloReturnTypeIsString()` test passed.  This should pass because the `SayHello()` method is a string method.  You can verify this in line 8 of the `SayHelloClass`.  Use this test to help you explore the Test Pane and testing process. 

1. Try running each test individually before moving on to the next step.  You can select individual tests by right-clicking on the test name either directly in the test class or the Test Explorer window.

   You will still have the same results as before, but now you have the skills to run tests all together or one at a time.  This is something that may come in handy as you work on larger assignments that may have many tests.

## Your Task

Your task is simple: make the program print out the string `Hello, World!`. Edit the code in the `SayHelloClass` class, within the `SayHello()` method. Verify your code with the auto-grading tests. 

  {{% notice orange "Warning" "rocket" %}}
   The auto-grading tests are VERY exacting. A difference of a single character will result in a failed test. The tests are also case-sensitive. You’ll need to pay attention to detail to correctly complete your assignments.
  {{% /notice %}}

## Submitting Your Work

Once you pass all of the tests, `add`, `commit` and `push` your code to GitHub.

Visit your assignment repository page to see the results of your assignment.  If you passed, you'll see a green checkmark. If you see a red X, then your assignment is not yet correct.

This process will be the same for all of your assignments in this unit. Revisit this page as needed to review instructions on running tests in C# projects.
