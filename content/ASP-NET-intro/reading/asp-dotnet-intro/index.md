---
title: "Design Patterns, MVC, and ASP.NET, Oh My!"
date: 2023-02-06T14:44:12-06:00
draft: false
weight: 1
originalAuthor: Courtney Frey # to be set by page creator
originalAuthorGitHub: speudusa # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

So far, we have been designing our applications by diagramming classes, drawing connections, and abstracting via interfaces. This practice benefits us because we can start seeing issues before we start coding. Many software developers start their applications with this process. Before we start diagramming our `Cat` class and our `HouseCat` class, we decide on the template for our design that we want to use. These design templates that are abstract solutions to common software architecture problems are called **design patterns**. Design patterns provide a set of conventions that we follow to build an application.

**Model-View-Controller** (MVC) is a design pattern where the programming logic behind the application is broken down into 3 components: models, views, and controllers. A **model** handles the data and business logic of the application. A **view** handles the user interface elements. A **controller** passes information from the models to the views. Controllers are the traffic cops of the application, capable of passing data back and forth to the browser in MVC web applications. This process will be covered in depth later on in this chapter.

{{< rawhtml >}}
   <img src="pictures/mvcOverview.png" alt="MVC diagram" />
{{< /rawhtml >}}

Because MVC breaks down all of the programming logic of an application into three digestable components, we can use this particular design pattern to make extensible applications. We also use MVC because it separates the components of the programs that the user interacts with from the underlying business logic.

## ASP.NET

**ASP.NET Core** is an extension of .NET Core and is used to build web applications. **ASP.NET Core MVC** is the framework that allows us to build web applications in a way that uses the MVC design pattern. Visual Studio has an embedded server so it is easy for us to run our applications and get started. This server picks the port number to run the app. 

{{% notice orange "Warning" "rocket" %}} 

   In this book, the port number we use is 5001. If your port number is different from any of the walkthrough materials, that will not affect the output of your project. Visual Studio uses the first available port on your computer to run your project which is why your port number may vary.  

{{% /notice %}}

{{% notice blue "Note" "rocket" %}} 

   Throughout this book, we will refer to ASP.NET Core MVC as ASP.NET or ASP.NET MVC. This is purely for the sake of brevity. When you see “ASP.NET” or “ASP.NET MVC”, we are talking about ASP.NET Core MVC.

{{% /notice %}}

## How We Teach ASP.NET

The following video is the first in a series designed to help you code your first ASP.NET application. We will be building this app over the next several chapters, finishing in [Views chapter]({{% relref "../../../razor-views" %}}). The video below provides an overview of simple application routing via the use of controllers along with a walkthrough of what the finished app will look like. In subsequent videos in this series, we ask you to code along for maximum absorption of the topics introduced. A summary of the content introduced will follow each of these videos.

## Intro to ASP.NET - Video

{{< youtube geoobGtBJmQ >}}

{{% notice blue "Note" "rocket" %}}
This video is demonstrating the final output of the `HelloASPDotNET` project.
Use the instructions on the next page to initialize your own `HelloASPDotNET` MVC project.  As you work through the next few chapters, you will create the routes seen in the video.
{{% /notice %}}