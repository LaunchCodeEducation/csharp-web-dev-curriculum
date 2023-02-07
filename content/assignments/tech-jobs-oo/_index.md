---
title: "Assignment 2: TechJobs (Object-Oriented Edition)"
date: 2023-01-11T13:15:59-06:00
draft: false
weight: 1
originalAuthor: Courtney Frey # to be set by page creator
originalAuthorGitHub: speudusa # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: Courtney Frey # update any time edits are made after review
lastEditorGitHub: speudusa # update any time edits are made after review
lastMod: 2023-02-07  # UPDATE ANY TIME CHANGES ARE MADE
---

## Introduction
Your apprenticeship at LaunchCode is going well! Only a few weeks in and you’re regularly making contributions to code that will eventually be used by all LaunchCode staff.

Your last task was to get the prototype Tech Jobs app in good shape. Now it’s time to advance the underlying structure of the program.

Your mentor on this project is Sally, one of the developers at LaunchCode. She regularly supports coders who are just getting started with their careers.

{{< rawhtml >}}
   <img src="pictures/LC-Sally.png" alt="LaunchCode Mentor Sally" width=20% />
{{< /rawhtml >}}

After seeing your strong work with your last project, Blake reported that you performed well and learned quickly. Because of your success, he and Sally feel comfortable assigning you to a set of tasks that are a notch up in difficulty.

Sally completed some initial work on the project and left you some `TODO`s.

### Learning Objectives

In this project, you’ll show that you can:
1. Read and understand code written by others.
1. Work with objects to encapsulate data and methods.
1. Use the generator in Visual Studio to automate routine tasks.
1. Use unit testing and Test-Driven-Development (TDD) to verify and create new methods.
1. Apply the concept of inheritance to streamline your classes (the DRY idea—Don’t Repeat Yourself).

### Getting Started

<!-- TODO: add links for Canvas and A0 -->

1. Get the Starter Code.  In *Canvas, Graded Assignment #2: TechJobs (Object-Oriented Edition)* contains a GitHub Classroom assignment invitation link, and then set up the project in Visual Studio. Refer back to the GitHub Classroom instructions from *Assignment #0: Hello, World!* for details.
1. Open Visual Studio.
1. If the app opens up to an existing project, close it.
1. From the Visual Studio dialog box, open your copy of the starter code.

### TechJobs (Object-Oriented Edition)

Sally has gotten the ball rolling by adding a `Job` class, along with classes to represent the individual properties of a job: `Employer`, `Location`, `PositionType`, and `CoreCompetency`. She completed the `Employer` class, and she left you the task of filling in the others.

As the team gets closer to deploying the app—and abandoning the test data they’ve been using—they’ll want an easy way to add and remove jobs via a user interface. Before that, however, you need to finish shifting the project to an object-oriented design.

## Why Change to Object-Oriented?

Working with data stored as strings in dictionaries and lists isn’t a good long-term solution, for reasons that we point out below.

The `Job` class introduces an object-oriented design to the application. It contains all of the properties you used in the console version of TechJobs: `Name`, `EmployerName`, `EmployerLocation`, `JobType`, `JobCoreCompetency`. There’s also an Id property which will be used to uniquely identify Job objects.

The main difference between the object representation of a job and the string-based representation is that the values of `EmployerName`, `EmployerLocation`, and the other non-ID properties are no longer strings. Instead, they are classes of their own.

### `Job` Members

Open the `Job` class file. 

{{% notice orange "Warning" "rocket" %}} 
The `Job` class is currently commented out.  Leave it in this state.  You can still explore the code. 
{{% /notice %}}

You’ll see the following properties (among other class members):


```csharp {linenos=true}
public string Name { get; set; }
public Employer EmployerName { get; set; }
public Location EmployerLocation { get; set; }
public PositionType JobType { get; set; }
public CoreCompetency JobCoreCompetency { get; set; }
```  

Of these, only `Name` is a string. Sally created classes to represent each of the other properties. These classes—`Employer`, `Location`, `CoreCompetency`, `PositionType`—have members to hold values and IDs.

So, for example, if you had a `Job` instance, you could get the name of the employer this way:

```csharp
// job is an instance of Job
string employerName = job.EmployerName.Value;
```

Additionally, the `ToString()` method of the `Employer` class is set up to return whatever the `value` field holds. Thus, using one of these objects in another string context like `Console.WriteLine` will print the data stored in `value`.

```csharp
// Prints the name of the employer
Console.WriteLine(job.EmployerName);
```

Why do we go through all of this trouble when we could store this job-related data as strings? 

There are a couple of reasons.

### Eliminate Duplication of Data
In our app, we have multiple jobs that have the same value in a given field. For example, there are multiple jobs with position type “Web - Full Stack”, and each employer may list several jobs. If we store the values of these fields as strings directly within each `Job` object, that data would be repeated in several places across the application.

By using objects, we can have a single `PositionType` object with the value “Web - Full Stack”. Each job that wants to use that position type holds onto a reference to the given object. Similarly, we can have one `Employer` object for each employer.

Aside from reducing the amount of raw data/memory that the application uses, this will allow data to be updated more easily and properly. If we need to change the name of an employer (e.g. due to a typo or a name change at the company), we can change it in one place, the single `Employer` object that represents that company.

As you continue to work on the assignment, you will find further ways to streamline the application.

### Enable Extension
While the four `Job` properties represented by objects will primarily be used for their string values, it’s easy to imagine adding new properties to address future needs.

For example, it would be useful for an `Employer` object to have an address, a primary contact, and a list of jobs available at that employer.

For a `Location` object, useful information includes a list of zip codes associated with that location, in order to determine the city and state for an employer or job.

If we were to store these four new properties as strings within the `Job` class, extending and modifying this behavior would be much more complicated and difficult moving forward.

## Review the Solution and the Auto-grading Tests

Now that you have some understanding of why we want to use Object-Orientation principles in our code, let's explore the code.

### Projects in Solution Explorer

Inside the Solution Explorer, you should see the following three projects: 
- The `TechJobs.Tests` project is where you will write unit tests for Task 4.
- The `TechJobsOO.Tests` project contains auto-grading tests and 2 text files.
- The `TechJobsOOAupoGraded6` project contains the code you will write and test.

### Test Projects in Test Explorer

This assignment has many more tests than the previous assignments.  We have created a test class for each assigned task.  

Open the Test Explorer, you should see `TechJobsOOAutoGraded6`.  Expand this to see the following test projects:
- `TechJobs.Tests` project is where you will write your own unit tests in this assignment.  Right now, it contains an empty test method and will pass.
- `TechJobsOO.Tests` project contains the auto-graded tests for this assignment.

In Test Explore, expand `TechJobs.Tests` project > `TechJobs.Tests` namespace > `JobTests` class > `TestMethod`.  This is an empty method that you will expand on in Task 4.  For now, you can leave it alone. 

In Test Explorer, expand the `TechJobsOO.Tests` project.  Nothing will happen because the tests have been commented out.  As you start each task, you will need to uncomment the auto-graded assignments.  Many of these tests are dependent upon code that doesn’t exist right now. By the end of a task, you will have enough code written to run the task tests.  

Since we can’t see our tests in the Test Explorer, let’s look that them inside the Solution Explorer.  Expand `TechJobsOO.Tests` inside the Solution Explorer and open `TestTask2` tests class. You should see 8 tests listed by their names. These are all of the tests that will be run after you complete Task 2.  You can run all your tests after you complete Task 2 or run individual tests as you go through Task 2. 

{{% notice blue "Note" "rocket" %}} 
There is no `TestTask1` since Task 1 does not require any coding.
{{% /notice %}}

### Task List in Visual Studio

To help you keep track of your tasks, Sally added many `TODO` tasks.  Use the Task List to as you work through the project.  

[Windows Users](https://learn.microsoft.com/en-us/visualstudio/ide/using-the-task-list?view=vs-2022): To open Task List, select **View** > **Task List**

[Mac Users](https://learn.microsoft.com/en-us/visualstudio/ide/reference/task-list-environment-options-dialog-box?view=vs-2022): To open Task List, select **View** > **Tasks**

### Running the Auto-grading Tests
<!-- TODO: Add link for A0 -->
If you need a refresher on running auto-graded tests, review _Assignment #0: Hello, World!_ 

Each task of the assignment will prompt you to uncomment and run the auto-graded tests.  Once you have completed the task you can leave the tests active.  They should all continue to pass as you continue through this assignment.

As you work on the components of the given tasks, continually re-run the tests to see the failing tests gradually pass. When all tests within the file pass, you’re ready to move on to the next task. As you expand your codebase, none of your earlier tests should fail.

## Your Assignment

### Your Tasks
The list below provides a general overview of your assigned tasks. Specific details for each part appear in the following sections, so be sure to read them carefully as you solve each problem.

1. Review Sally’s code in the `Employer` class to learn how to assign a unique ID.
1. Add properties and custom methods as needed to the `Location`, `CoreCompetency`, and `PositionType` classes.
1. Complete the `Job` class using what you learned in steps 1 and 2.
1. Use unit testing to verify the constructors and `Equals()` methods for the `Job` class.
1. Use TDD to design and code a custom `ToString()` method for the `Job` class.
1. Use inheritance to DRY the code within `Employer`, `Location`, `CoreCompetency`, and `PositionType`.

On to [Task 1]({{< relref "../tech-jobs-oo/task-1.md" >}}).