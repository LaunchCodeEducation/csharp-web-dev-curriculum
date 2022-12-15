---
title: "Setup for C#"
date: 2022-12-15T09:16:07-06:00
draft: false
weight: 1
originalAuthor: Sally Steuterman # to be set by page creator
originalAuthorGitHub: gildedgardenia # to be set by page creator
reviewer: # to be set by the page reviewer
reviewerGitHub: # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

For the entirety of this course, we will be coding in C# with the help of Visual Studio and .NET.

##  The Integrated Development Environment

Visual Studio (VS) is an **integrated development environment (IDE)**. An IDE is like a text editor on steroids. We can write and edit code and make use of additional features that enhance our coding experience. VS offers code completion hints, debugging, and even it’s own compiler.

We’ll be using it throughout this course, so it’s time to get familiar with some of the basics.

{{% notice orange "Note" "rocket" %}}
Visual Studio IDE is not the same application as the source-code editor called Visual Studio Code (VS Code). If you already have VS Code installed on your machine, you will still need to install and configure VS.
{{% /notice %}}

## Development Frameworks

### .NET
**.NET** is a set of tools for developing software in a number of different programming languages, including C#. The tools together make what is known as a **software development kit**, or **SDK**.

Some of its features:

1. Open-source and available on several operating systems.
1. The SDK provides the runtime environment and the virtual machine for compiling and running C# programs.
1. Contains the base class libraries which include the built-in code that takes care of common programming items, such as object types.
1. Able to be extended using additional frameworks such as ASP.NET.

You can learn more about .NET [here](https://dotnet.microsoft.com/en-us/learn/dotnet/what-is-dotnet).

### ASP.NET Core

As we progress through this portion of the course, we will start creating web projects. .NET will compile C#, but does not contain any libraries for web development. ASP.NET Core is an open source collection of libraries specifically for web development and creating dynamic web applications.

We will use ASP.NET Core midway through this course; however, you can to learn more about this framework at [this site](https://dotnet.microsoft.com/en-us/learn/aspnet/what-is-aspnet-core).

## C# and the Frameworks

A summary of the relationship between the code you write in C# and tools provided by .NET:

1. We write code in C#.
1. The source code is compiled (like translating) into another intermediate language.
1. The intermediate code is read by a runtime program included in the .NET SDK.
1. The runtime environment translates the intermediate code into machine-readable language.

Fortunately for us, .NET can be installed along with Visual Studio IDE.

## Windows Users vs. Mac Users

Windows users will setup their C# development environment with a community version of Visual Studio. Mac users need to download and install a different version of Visual Studio called Visual Studio for Mac. While the names of these two programs are very similar, the user-experiences are quite different.

An important note for this class: The content of this book is designed to inform both Windows and Mac users on the basics of web programming in C#. There are sometimes significant, and other times more minor, discrepancies between how to use the IDE tools provided in Visual Studio on Windows machines and Visual Studio for Mac. We will do our best to provide either instructions that are application neutral, or instructions that are tailored to the development experiences on both operating systems. There may be times when your C# project view will not look exactly like that in the book because you are on a different operating system and are therefore using a different Visual Studio application. The actions you take or buttons to click may be slightly different from what you see in the book.

## C# Naming Conventions

C# has some very straightforward [naming conventions](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/coding-conventions#naming-conventions). These are universally used by C# programmers, and differ in some cases from conventions commonly used in Python or other coding languages.

Again, these are conventions. Not following them will not prevent your code from running, as long as you are following [C#’s naming rules](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/identifier-names).

| Identifier Type | Convention | Examples |
|------|------|-----|
| Method parameters, local variables, and fields | Start with a lowercase letter and use camelCase | `id`, `firstName` |
| Methods, properties, and class names | Start with an uppercase letter and capitalize each word; do not use hyphens or underscores (aka PascalCase) | `Program`, `HelloWorld`, `TempConverter` |

Microsoft provides [more detailed naming guidelines here](https://learn.microsoft.com/en-us/dotnet/standard/design-guidelines/naming-guidelines?redirectedfrom=MSDN).

## Check Your Understanding

1. True or false: Visual Studio is a framework.
1. .NET contains: (Select all that apply)

   1. A C# compiler
   1. A virtual machine
   1. Visual Studio IDE
   1. C# class library