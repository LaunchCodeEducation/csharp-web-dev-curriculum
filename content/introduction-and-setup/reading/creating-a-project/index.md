---
title: "Creating a C# Project"
date: 2022-12-15T09:16:07-06:00
draft: false
weight: 4
originalAuthor: Sally Steuterman # to be set by page creator
originalAuthorGitHub: gildedgardenia # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

Following the “Hello World” trend, let’s create a new Visual Studio project.

1. Create a new folder to hold your C# practice files. Since you will be creating lots of small projects as you move through this course, we suggest that you also add sub-folders with names corresponding to the related chapters and projects. Something like `csharp-practice/chapter-name/project-name`.
1. In Visual Studio, from the project opener window, select the option to create a new Visual Studio project.
1. You next need to choose what project template to use. For this first project (and those in the next several lessons), select the *.NET Core Console Application* option for C#.
   1. **Mac Users**:
      1. You can find this under *Web* and *Console* in the left menu.
      1. Select the *App* subdirectory.
      1. Select *Console Application* from the *General* menu option in the center menu pane and press *Continue*
   1. **Windows Users**:
      1. Select *Console App*.
      1. If you can’t find it easily, you can search “Console App”.
1. Select *.NET 6.0* as your Target Framework and press *Continue*.
1. Then, give your new project a name. Following C# Naming Conventions, call your project `HelloWorld`. The solution name will be the same. Choose where you want this project to be saved, ideally somewhere inside the directory you created in Step 1 of this tutorial.
   1. **Mac Users**: Pick the options for “Use git for version control.” and “Create a .gitignore file to ignore inessential files”.
1. Visual Studio will now create a **Solution** to hold your console **Project**. The project is your current app. The project contains all of the files that app needs to build and run. The solution is a workspace that combines multiple projects, which are usually related to each other. The solution file type is **.sln**. Once created, Visual Studio opens a new project window that displays your `Program.cs` file.
1. To see the other files inside this solution, you will need to turn your attention to either the Solution (Mac Users) or the Solution Explorer (Windows Users) on the left. You’ll see the project file tree containing a file called `Program.cs` in a pane called Solution Explorer.
1. You are new to C# and we’ll go over the syntax present in Program.cs in time. For now, can you guess what line 2 accomplishes?

   {{< highlight csharp "linenos=true" >}}
      // See https://aka.ms/new-console-template for more information
      Console.WriteLine("Hello, World!");
   {{< / highlight >}}
  
   Click on the *Run* button (a triangle button located above the `Program.cs` panel for Windows users and above the solution for Mac users) to run the project and see the output.

1. A console window should pop up with the line “Hello World” printed. That’s it. You have created and executed your first C# application!

{{% notice green "Tip" "rocket" %}}
The first time you run a console app in Visual Studio, you may be prompted to allow VS to access the terminal. This is ok.
This may also take longer than a few seconds to run the very first time.
{{% /notice %}}

## Troubleshooting

This app is printing to the terminal. If you are not able to see the output, look inside the project’s terminal.

If you would like more instructions on creating and running this project check out the following documentation:

[Windows Users](https://learn.microsoft.com/en-us/visualstudio/get-started/csharp/visual-studio-ide?view=vs-2022)

[Mac Users](https://learn.microsoft.com/en-us/visualstudio/mac/ide-tour?view=vsmac-2022)

### Hello, Solution!

You’ve just created your first C# project. Congrats! In fact, you’ve also just created your own C# solution. A solution is a container that holds different projects like a folder that contains subfolders. Your `HelloWorld` project is nested within a solution called `HelloWorld`. It is normal for a project to have the same name as the solution.

{{% notice green "Tip" "rocket" %}}

   In the Solution Explorer, you may notice that next to the solution name is the name of the current branch in parantheses. As you create more branches, you may find this a helpful tip to keep track of which branch you are currently working on.

{{% /notice %}} 

A C# project contains all the code to run a particular application. Along with the `Program.cs` file you ran just a moment ago, you may have also noticed a `Dependencies` folder. Many applications require extra code like access to another project in the same solution or other compiling configurations, such as testing libraries, to execute.

You can create another project inside of the `HelloWorld` solution very easily. Right click on the solution name to add a new project, another console app as above, and name it `Hello<YourName>`. Change the starter code in `Program.cs` to greet you by name.

Now that you have more than one project in your solution, you need to select which one you want to run. Select the project name from the menu next to the Run button.

### Check Your Understanding

The two questions will use the following code:

```csharp {linenos = true}
// See https://aka.ms/new-console-template for more information
Console.WriteLine("Hello, World!");
```

{{% notice green "Question" "rocket" %}}
   Given the code above, which line is responsible for printing a message?
   1. Line 1
   1. Line 2
   1. None of the above
{{% /notice %}}

{{% notice green "Question" "rocket" %}}
   Where does the code above print out?
   1. In line 3 of the `Program.cs` file
   1. In the browser
   1. In the terminal
   1. None of the above
{{% /notice %}}