---
title: "Assignment 3: TechJobs MVC"
date: 2023-01-05T13:58:39-06:00
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

## Introduction

Your first two tasks as an apprentice went well! You, Blake, and Sally built
the TechJobs console prototype and then refactored the code to move it to an
object-oriented format.

After demonstrating the prototype for the Company Team at LaunchCode, it
received the green light to be fully built out as a web application.

The first step in this process will be to quickly develop a [minimum viable
product](https://en.wikipedia.org/wiki/Minimum_viable_product), or MVP. The
goal is to get a functioning web app up and running with as little work as
possible. That way, additional feedback and testing can be done early in the
development process. After that, additional behind-the-scenes work will be
carried out to fully develop the model and data side of the application.

For this next step in the project, you’ll be working with Carly.

{{< rawhtml >}}
   <img src="pictures/LC-Carly.png" alt="LaunchCode Mentor Carly" width=20% />
{{< /rawhtml >}}

Carly was once a LaunchCode apprentice as well, so she knows just what
it’s like to be in your shoes. She’s done some initial work on the
project and left you some `TODO` tasks that she knows you can handle.

## Learning Objectives

In this project, you’ll show that you can:

1. Read and understand code written by others.
1. Work within the controller and view portions of a ASP.NET MVC application.
1. Use Razor syntax to display data within a view.
1. Create new action methods to process form submission.

## TechJobs (MVC Edition)

You’ll start with some code that Carly has provided. The idea behind your
current assignment is to quickly deliver a functioning ASP.NET MVC application,
so you’ll focus on the controllers and views.

In order to do this, you’ll be reusing the `JobData` class and
`job_data.csv` file from the console app. You will eventually have to go back
and rewrite the data portion of the application to make a true, database-backed
model. However, using the existing `JobData` class to provide some basic data
functionality lets you focus on the views and controllers for now.

## Your Assignment

The list below provides a general overview of your assigned tasks. Specific
details for each part appear in the following sections, so be sure to read them
carefully as you solve each problem.

1. Review Carly’s code in the `JobData` file as well as in the existing
   controllers and views.
1. Carly needs your help completing the code to display only certain jobs. She has the code to display all of the values that users can select to filter the jobs.
1. Carly started working on the search feature, but only got as far as
   writing the code to display the search form. She’s handed the project to you
   to finish the rest. First, you'll create a controller method to retrieve search results.
1. Finally, you'll display search results in the view. 

Throughout your work, refer to our [demo app](https://csharp-mvc.launchcodetechnicaltraining.org/) as needed to clarify questions about intended application behavior.

## Getting Started

Set up a local copy of the project:

<!-- TODO: Add link back to assignment 2 -->

1. In Canvas, **Graded Assignment #3: TechJobs (MVC Edition)** contains a GitHub Classroom assignment invitation link, accept the assignment, and then set up the project in Visual Studio. Refer back to the [GitHub Classroom instructions]({{< relref "../hello-world/getting-started/" >}}) from Assignment 0 for details. 
1. Launch the application to make sure it starts up properly. Then shut it down.
1. Run the autograding tests. The tests for this assignment are set up the same way as for Assignment 2. There are four tasks for this assignment, but the first doesn't require any coding on your part. Therefore, there are 3 tests files (for tasks 2-4). As with [Assignment 2]({{< relref "../tech-jobs-oo/#getting-started" >}}), we recommend that you only run the tests for the task you are currently working on.

Here are the tasks you need to complete:

{{% children %}}

