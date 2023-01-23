---
title: "Cloning a C# Project"
date: 2022-12-15T09:16:07-06:00
draft: false
weight: 5
originalAuthor: Sally Steuterman # to be set by page creator
originalAuthorGitHub: gildedgardenia # to be set by page creator
reviewer: # to be set by the page reviewer
reviewerGitHub: # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

Follow along with the provided walkthroughs to learn how to clone repos into Visual Studio. Try it out on your own by forking and cloning the [LaunchCodeEducation/csharp-web-dev-datatypes](https://github.com/LaunchCodeEducation/csharp-web-dev-datatypes) repository page. First, fork the repository into your own GitHub account by selecting Fork from the top right of the page and then clone the repository to your own machine to start working on it locally.

## Windows Users

[Clone a Git Repository in Visual Studio](https://learn.microsoft.com/en-us/visualstudio/version-control/git-clone-repository?view=vs-2022)

Note the path where you save this repo.

## Mac Users

[Cloning an Existing Repo](https://learn.microsoft.com/en-us/visualstudio/mac/set-up-git-repository?view=vsmac-2022#clone-an-existing-repository)

Be sure to note the Target Folder where this repo is saved.

{{% notice blue "Note" "rocket" %}}
   You can also find the option to clone a Git repository under *File*.
{{% /notice %}}

## Exploring the Cloned Repo in Your Terminal

While you can do this through the Visual Studio interface, you should practice using the terminal as well.
The interface may change or some places may test your comfort with the terminal. Keep practicing those command line skills!

Once you have cloned it in Visual Studio, locate the repo using your terminal.

On a Windows machine, it is a path you saved your repo at. On a Mac, it’s in the Target Folder.

Once you find the repo, `cd` into it. Look for the Solution file which uses the `.sln` file type.

```bash-session
students-computer:csharp-web-dev-datatypes student$ ls
HelloMethods                 csharp-web-dev-datatypes.sln
TempConverter
```

{{% notice blue "Note" "rocket" %}}
The `csharp-web-dev-datatype` solution contains 2 separate projects: `HelloMethods` and `TempConverter`. A single solution can hold multiple projects.
{{% /notice %}}

Try to open the solution using the command line prompt:

Windows Users: `start *.sln`

Mac Users: `open *.sln`

{{% notice blue "Note" "rocket" %}}
It may take a while for Visual Studio to start up. Be patient! Sometimes just clicking on the icon can help bring the solution pane to the forefront of your screen.
{{% /notice %}}

Return to the terminal. Locate your `Program.cs` file for the `HelloMethods` project. This will be contained in the project directory of the same name.

```bash-session
students-computer:csharp-web-dev-datatypes student$ ls
HelloMethods                 csharp-web-dev-datatypes.sln
TempConverter
students-computer:csharp-web-dev-datatypes student$ cd HelloMethods
students-computer:csharp-web-dev-datatypes student$ ls
HelloMethods.csproj  Message.cs              Program.cs
```

You have now stepped into the project files for `HelloMethods`. All of the files here are related to the `HelloMethods` project.

As you work with repos in this unit, some solutions may contain a single project and others may contain multiple.

## How to Work with a Cloned Repo

We recommend using the terminal to open and work with your repos. You will be able to interact with git easily this way.

Use the terminal to locate the repo you wish to open. `cd` into the solution. You can verify this by looking for a file that has the `.sln` type. Use the command prompt above for your operating system.

Open the solution file tree in Visual Studio. If you see multiple projects, you can select which one to run two ways:

1. Right-clicking on the name of the project and selecting the *Run* option.
1. Open the project’s `Program.cs` file then use the run button in the menu bar.

## Check Your Understanding

1. Which file is the solution?

   ```bash-session
   students-computer:csharp-web-dev-datatypes student$ ls
   HelloMethods                      csharp-web-dev-datatypes.sln
   TempConverter
   ```

   1. `TempConverter`
   1. `HelloMethods`
   1. `csharp-web-dev-datatypes.sln`
   1. `Program.cs`

1. Where would Willow find the `Program.cs` file for the `TempConverter` project?

   ```bash-session
   students-computer:csharp-web-dev-datatypes student$ ls
   HelloMethods                      csharp-web-dev-datatypes.sln
   TempConverter
   ```

   1. Inside the `TempConverter` project
   1. Inside the `HelloMethods` project
   1. Inside `csharp-web-dev-datatypes.sln`
   1. None of the above