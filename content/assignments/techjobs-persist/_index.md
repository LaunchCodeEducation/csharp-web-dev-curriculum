---
title: "Assignment 4: Tech Jobs Persistent"
date: 2023-04-04T09:57:32-06:00
draft: false
weight: 5
originalAuthor: Courtney Frey # to be set by page creator
originalAuthorGitHub: speudusa # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

## Your Task
You will once again work with the TechJobs application. This time around you’ll add ORM functionality by using Entity Framework. You will be responsible for completing the code to allow users to create new job data.
Your final application will have the same list and search capabilities as your [Tech Jobs (MVC Edition)](../techjobs-mvc/) but you’ll need to do the work to connect the project to a database for storing user-submitted job data.
Each of the three sections of this assignment will also ask you to demonstrate your SQL skills under an item labeled **SQL TASK**.
As you work through each part, refer to our [demo app](https://techjobs-persistent.launchcodelearning.org/) to clarify questions about intended application behavior.

{{% notice blue Note "rocket" %}}
The List and Search functions in the demo app are not part of this current Assignment's codebase at this time.
{{% /notice %}}

## Getting Started
Set up a local copy of the project:

1. Fork and clone the [starter code repository](https://github.com/LaunchCodeEducation/CSharp6-TechJobs-Persistent).
1. You will need to complete Task 1 before you see a working MVC application.

## Checkout and Review the Starter Code
You will be able to run your application without any build errors. However, you’ll likely see a host of errors relating to the Entity Framework annotations and classes when you attempt to add any data or load different pages. Some of these have already been added but the connection to the database has not been set up yet. That will be one of your tasks. You’ll need to complete Task 1 before you can thoroughly check out the project running in the browser.

That said, it’s a good idea to scan the classes and templates even before you’re able to run the application. Take a gander at the `Job` class. It will look somewhat similar to the model in [Tech Jobs (MVC Edition)](../techjobs-mvc/), with a few key differences.

You’re no longer using a CSV file to load job data, instead, we’ll be creating new `Job` objects via a user form. The job data will be stored in a MySQL database that you’ll set up in Task 1 of this assignment.

As you explore the starter code, you’ll notice that the `JobField` class is missing. You will focus on just two aspects of a job listing: the employer and the skills required. Your task for Task 2 is to add code to let a user create an employer object.

The `Job` class will also look different from how you have last seen it. In Task 3, you will use the many-to-many relationship between skills and jobs to make it easier for users to add skills to new jobs. In your ASP.NET project, you’ll see an empty file in the solution called `queries.sql`. After completing the C# updates for task 1, 2, and 3, we ask you to test your application updates with SQL statements.

Since you are entering your own data, the queries we ask you to write will return unique result sets. For example, if you haven’t entered any data yet, there may be an empty result set. However, as the architect of the database, you have the knowledge to write the appropriate queries nonetheless.

Move on to [Task 1]({{< relref "../techjobs-persist/task-1/" >}}).
