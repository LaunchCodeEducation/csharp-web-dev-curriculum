---
title: "Task 2: Running the Auto-grading Tests"
date: 2023-01-05T09:57:32-06:00
draft: false
weight: 2
originalAuthor: Courtney  # to be set by page creator
originalAuthorGitHub: speudusa # to be set by page creator
reviewer: Kimberly # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: Courtney # update any time edits are made after review
lastEditorGitHub: speudusa # update any time edits are made after review
lastMod: copy edits and links for the debugger added, created separate page for this section
---

We use unit tests in your graded-assignments to provide feedback on your progress. We will refer to them as auto-graded or auto-grading tests in these projects. 
Use the tests to check your work as you complete the assignment. The goal is to pass all tests.

Let’s learn how to run the tests in Visual Studio.

1. Each assignment will contain a test **project**. This project contains all of the auto-grading tests and may have more than one test class. In the Solution/Solution Explorer, navigate to `HelloTests.cs` inside the `Hello.Tests` project. 

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
      1. Select the green triangle on the left of the Test Explorer Window. 
      1. In the Test Explorer, step through the file tree until you find the failed test. 
      1. If you need more help running the tests, checkout this [guide](https://learn.microsoft.com/en-us/visualstudio/mac/testing?view=vsmac-2022#running-tests) for running tests in Visual Studio for Mac
   1. Windows Users 
      1. **Test** > **Windows** > **Test Explorer**
      1. Select the `Run All` icon to run all of your tests. 
      1. In the Test Explorer, step through your file tree until you find the failed test.
      1. If you need more help running the tests, checkout this [guide](https://learn.microsoft.com/en-us/visualstudio/test/run-unit-tests-with-test-explorer?view=vs-2022) for running tests in Visual Studio.


1. Visual Studio opens a Test Results Pane every time it runs a test. This pane provides you with detailed information about which tests passed and which tests failed.  The pane will also provide you with output for any failed tests, including what was expected and what was actually received.  This is a great place to look when dealing with a failing test.

   Now that you have run the tests, you should see that one of the tests has failed and the other passed. We have not touched any code yet. Use the Test Results Pane to navigate into which specific test has failed.

   In this case, the `TestIfSayHelloReturnsCorrectValue()` test, expected our code to output `Hello, World!` Instead, the method is returning is `&&&` causing the test to fail. Be sure to explore your test output. The output will show you what was expected and what was actually received.  Often messages will be provided for a failed test. In this test, the message is "Incorrect message displayed".

   The `TestSayHelloReturnTypeIsString()` test passed. This should pass because the `SayHello()` method is a string method. You can verify this in line 8 of the `SayHelloClass.cs`. Use this test to help you explore the Test Results Pane and testing process. 

1. Try running each test individually before moving on to the next step. You can select individual tests by right-clicking on the test name either directly in the test class or the Test Explorer window.

   You will still have the same results as before, but now you have the skills to run tests all together or one at a time. This is something that may come in handy as you work on larger assignments that may have many tests.


### Next Steps
You are now ready to move on to [Task 3: Start Coding]({{< relref "../hello-world/start-coding.md" >}}).