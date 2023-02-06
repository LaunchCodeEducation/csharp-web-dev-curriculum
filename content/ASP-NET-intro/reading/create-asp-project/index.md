---
title: "Create a New ASP.NET Project"
date: 2023-02-06T14:44:12-06:00
draft: false
weight: 2
originalAuthor: Courtney Frey # to be set by page creator
originalAuthorGitHub: speudusa # to be set by page creator
reviewer: # to be set by the page reviewer
reviewerGitHub: # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

ASP.NET is a framework in the .NET Core family that is used to build web applications. While [ASP.NET](https://learn.microsoft.com/en-us/aspnet/core/?view=aspnetcore-6.0) can be used to build a wide variety of web applications, we will be focusing on using it to build MVC web applications.

## Getting Started

To create a new ASP.NET MVC project, start a new project in Visual Studio.


### Windows Users

1. Use the Get started Menu to Create a new project.

1. When selecting the type of project, select *ASP.NET Core Web App (Model-View-Controller)*.

   There are 2 ways to find this easily:
      1. Use the search bar.

      1. Select “Web” from the dropdown menu.

   Once you have your project type, click *Next*.

1. Name your project `HelloASPDotNET` and put it in the appropriate directory for all of your classwork. Hit *Next*.

1. Select the Framework. We are going to use .NET Core 6.0. You do not need to adjust any other options at this point. Select *Create*!

1. Visual Studio creates a fully-functional web application for you.

{{% notice green "Tip" "rocket" %}} 

**Troubleshooting:**
This [tutorial for Windows](https://learn.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/start-mvc?view=aspnetcore-6.0&tabs=visual-studio) can help you if you are stuck.

{{% /notice %}}

### Mac Users
1. Open Visual Studio for Mac and select  *New*

1. The type of project is a **Web Application (Model-View-Controller)**. In the left-side menu, select *App* from under the *Web and Console* list. Continue on to the next screen.

1. Target Framework will be `.NET 6.0`. You don’t need to adjust any other settings at this time.

1. Name your project `HelloASPDotNET` and put it in the appropriate directory for all of your classwork. Hit *Next*.

1. Visual Studio creates a fully-functional web application for you.

{{% notice green "Tip" "rocket" %}} 

**Troubleshooting:**
Microsoft created a tutorial for creating an MVC in Visual Studio, but for the Mac version they recommend the following [guide](https://learn.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/start-mvc?view=aspnetcore-7.0&tabs=visual-studio-mac).

{{% /notice %}}

{{% notice orange "Warning" "rocket" %}} 
The guide is working with `.NET 7.0`. Make you that you are using `.NET 6.0` as the process is identical.
 
{{% /notice %}}

### All Users

1. Now launch the application!

   1. **Mac Users:** Click *Run*.   

   1. **Windows Users:** Select `HelloAspDotNet` (or whatever you named your project) and try launching the application if it doesn't work initially.

1. Eventually, your browser will open and display your application. Take note of the port number in the address bar.

{{% notice green "Tip" "rocket" %}} 

**Troubleshooting:**
Refer to the guides mentioned above

{{% /notice %}}

{{% notice blue "Note" "rocket" %}} 

The home page of your application already contains a link to a tutorial from Microsoft on how to use ASP.NET MVC. If you want extra study materials, check out that [tutorial](https://learn.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/start-mvc?view=aspnetcore-6.0&tabs=visual-studio) from the home page Microsoft designed!

{{% /notice %}}

## Explore the Code
In the `Controllers` directory, check out `HomeController.cs`. Microsoft provided the code in `HomeController` and that is why our application ran immediately after we created it and was full of content. As we work on our new application, we will be adding a new controller, `HelloController`.

{{% notice blue "Note" "rocket" %}} 
 
{{% /notice %}}

## Check Your Understanding

{{% notice green  "Question" "rocket" %}} 

**True/False:** You should take note of the port number the server is using to run your application.

<!-- ans: True! It may not run at 5001 -->

{{% /notice %}}