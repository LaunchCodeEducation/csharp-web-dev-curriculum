---
title: "Task 1: Getting Started"
date: 2023-01-05T09:57:32-06:00
draft: false
weight: 1
originalAuthor: Courtney  # to be set by page creator
originalAuthorGitHub: speudusa # to be set by page creator
reviewer: Kimberly # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: Courtney # update any time edits are made after review
lastEditorGitHub: speudusa # update any time edits are made after review
lastMod: copy edits and links for the debugger added, created separate page for this section
---


Let’s set up the assignment on our computer and learn about its basic structure.

1. Find **Assignment #0** in Canvas and click on the invitation link. After accepting the assignment on the Github Classroom page, go to your assignment repository on GitHub.

1. Follow the instructions to clone your repository and open it in Visual Studio.

1. When the solution opens, check out the contents of the Solution (Mac) or Solution Explorer (Windows). You will find two **projects** within the solution:
 
   * The `HelloWorldAutoGraded` contains the code that you will work with for this assignment. 
   * The `Hello.Tests` project contains auto-grading tests. You do not need to change any of the code in the testing project.

   {{% notice blue "Note" "rocket" %}}
   If you do not see the **Solution Explorer**, you can open it by selecting the **View** option in the toolbar.
   * Windows Users: **View** > **Solution Explorer**
   * Mac Users:  **View** > **Solution** 

      <!-- TODO: Link back to chapter 1 -->
   Review the Visual Studio walkthroughs from chapter 1 if you need help navigating Visual Studio.
   {{% /notice %}}

1. Inside `HelloWorldAutoGraded`, open up the `SayHelloClass.cs` class. This is where you will write any code for this assignment. Within this class, you will see the following:
   * The `SayHello()` method which is returning `&&&`.
   * `SayHelloClass()` constructor which is empty.  This will remain empty for this assignment.


1. Now, turn your attention to Program.cs in the `HelloWorldAutograded` project. This class will print two strings to the console using the `Console.WriteLine()` method.  
   * The first returns the string value of the `SayHello()` method from the `SayHelloClass`.
   * The second returns the data type of the `SayHello()` method’s output.


1. You are now ready to run the program. Do the following:
   * **Mac Users:** Hit the Run button at the top left-hand corner of the window. Right-clicking on the `HelloWorldAutograded` project and selecting Run Project will also work.
   * **Windows Users:** Click on the solid green triangle next to the name of the `HelloWorldAutograded` project. You can also press F5 to run the project.


1. Visual Studio opens a pane and displays any program output when you run a program. Currently, the program output contains the following:
   
   ``` console 
   &&&
   System.String
   ```
1. You are ready to run the auto-grading tests.


You are now ready to move on to [Task 2: Running the Auto-grading Tests]({{< relref "../hello-world/auto-grading-test.md" >}}).