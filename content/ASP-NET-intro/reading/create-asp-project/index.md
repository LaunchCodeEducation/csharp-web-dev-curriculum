---
title: "Create a New ASP.NET Project"
date: 2023-02-06T14:44:12-06:00
draft: false
weight: 2
originalAuthor: Courtney Frey # to be set by page creator
originalAuthorGitHub: speudusa # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

ASP.NET is a framework in the .NET Core family that is used to build web applications. While [ASP.NET Core](https://learn.microsoft.com/en-us/aspnet/core/?view=aspnetcore-6.0) can be used to build a wide variety of web applications, we will be focusing on using it to build MVC web applications.

## Getting Started

To create a new ASP.NET Core MVC project, start a new project in Visual Studio.

{{% notice blue "Note" "rocket" %}}

You are creating the inital MVC template.  You will not have the routes seen in the video.  
You will add these to your project in the next chapter.

{{% /notice %}}


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

Mac users, the guide is working with `.NET 7.0`. Make you that you are using `.NET 6.0` as the process is identical.

{{% /notice %}}

### All Users

1. Now launch the application!

   1. **Mac Users:** Click *Run*.   

   1. **Windows Users:** Select `HelloAspDotNet` (or whatever you named your project) and try launching the application if it doesn't work initially.

1. Eventually, your browser will open and display your application. Take note of the port number in the address bar.  You should see `localhost:XXXX`. This means your computer is serving the web page.

{{% notice green "Tip" "rocket" %}} 

**Troubleshooting:**
Refer to the guides mentioned above

{{% /notice %}}

## Explore the Code
In the `Controllers` directory, check out `HomeController.cs`. Microsoft provided the code in `HomeController` and that is why our application ran immediately after we created it and was full of content.

## Check Your Understanding

{{% notice green  "Question" "rocket" %}} 

**True/False:** You should take note of the port number the server is using to run your application.

<!-- ans: True! It may not run at 5001 -->

{{% /notice %}}