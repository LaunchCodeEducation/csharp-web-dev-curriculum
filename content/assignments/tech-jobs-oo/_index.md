---
title: "Assignment 2: TechJobs (Object-Oriented Edition)"
date: 2023-01-11T13:15:59-06:00
draft: false
weight: 100
originalAuthor: Courtney Frey # to be set by page creator
originalAuthorGitHub: speudusa # to be set by page creator
reviewer: # to be set by the page reviewer
reviewerGitHub: # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

## Introduction
Your apprenticeship at LaunchCode is going well! Only a few weeks in and you’re regularly making contributions to code that will eventually be used by all LaunchCode staff.

Your last task was to get the prototype Tech Jobs app in good shape. Now it’s time to advance the underlying structure of the program.

Your mentor on this project is Sally, one of the developers at LaunchCode. She regularly supports coders who are just getting started with their careers.

<!-- TODO: Insert Image Here -->

After seeing your strong work with your last project, Blake reported that you performed well and learned quickly. Because of your success, he and Sally feel comfortable assigning you to a set of tasks that are a notch up in difficulty.

Sally completed some initial work on the project and left you some `TODO`s.

<!-- TODO: learn how to make this click able -->
## Table of Contents:
Learning Objectives
- Get the Starter Code
- TechJobs (Object-Oriented Edition)

Why Change to Object-Oriented?
- `Job` Members
- Eliminate Duplication of Data
- Enable Extension

Review the Solution and Auto-grading Tests
- Solution Explorer
- Test Explorer
- Running the Auto-grading Tests

Your Assignment
- Your Tasks
- Task 1: Explore the `Employer` Class
- Task 2: Complete the Support Classes
- Task 3: Complete the `Job` Class
- Task 4: Use Unit Testing to Verify Parts of the `Job` Class
- Task 5: Use TDD to Build The `ToString()` Method
- Task 6: Refactor to DRY the Support Classes

Sanity Check

How to Submit
<!-- TODO: learn how to make this click able -->





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
Use unit testing to verify the constructors and `Equals()` methods for the `Job` class.
Use TDD to design and code a custom `ToString()` method for the `Job` class.
Use inheritance to DRY the code within `Employer`, `Location`, `CoreCompetency`, and `PositionType`.

### Task 1: Explore the Employer Class

Open the `Employer` file in Visual Studio and examine the code. In addition to the three members—`nextId`, `Id`, and `Value`—the class includes some methods like `ToString()` and `Equals()`.

You can refer to these examples as you fill in the missing pieces in the other classes, but for now let’s take a closer look at the constructors.

#### Assign a Unique ID
One neat trick we can use is to automatically assign each new object a unique ID number.

Examine the two constructors in `Employer.cs`:

```csharp {linenos=true,hl_lines=[3, 6,7,8,9,10, 12,13,14,15],linenostart=1}
public class Employer {
   public int Id { get; }
   private static int nextId = 1;
   public string Value { get; set; }

   public Employer ()
   {
      Id = nextId;
      nextId++;
   }

   public Employer (string value) : this()
   {
      Value = value;
   }

   // Additional methods omitted from this code block
```

1. Line 3 declares the field `nextId`. Since it is static, its changing value is NOT stored within any `Employer` object.

1. The first constructor (lines 6 - 10) accepts no arguments and assigns the value of `nextId` to the id field. It then increments `nextId`. Thus, every new `Employer` object will get a different ID number.

1. The second constructor (lines 12 - 15) assigns the value field. It ALSO initializes id for the object by calling the first constructor statement with the `:this()` syntax. Including `:this()` in any `Employer` constructor makes initializing id a default behavior.

{{% notice green "Tip" "rocket" %}} 
By adding `: this()` to the signature of the second `Employer` constructor, we are using a new technique called constructor chaining. For more info on how this chaining technique works, check out this [blog post](https://www.codecompiled.com/csharp/constructor-chaining-c/)!
{{% /notice %}}

### Task 2: Complete the Support Classes

{{% notice orange "Warning" "rocket" %}}
Due to the fact that this code is being auto-graded as you work through it, make sure that you use any and all names for classes, variables, methods, etc provided to you in these directions.
{{% /notice %}}

Sally needs you to build up the remaining classes. In each case, refer to the Employer class for hints on how to structure your code.



#### The `Location` Class

Open the Location.cs file. Note that the methods for this class are done, as is the constructor for initializing the Id property.

Sally left you a `TODO` comment with instructions for coding a second constructor:
1. It should call the first constructor to initialize the id field.
1. It must also initialize the value field for a new Location object.

{{% notice blue "Note" "rocket" %}}
To locate all of the `TODO`s for Task 2, use the Task List feature in Visual Studio.

[Windows Users](https://learn.microsoft.com/en-us/visualstudio/ide/using-the-task-list?view=vs-2022): To open Task List, select **View** > **Task List**

[Mac Users](https://learn.microsoft.com/en-us/visualstudio/ide/reference/task-list-environment-options-dialog-box?view=vs-2022): To open Task List, select **View** > **Tasks**
{{% /notice %}}

#### The `CoreCompetency` Class

Open the class file. In this case, the constructors and custom methods are ready. Sally needs you to change the `id` and `value` fields to auto-implemented properties, but NOT `nextId`.

#### The `PositionType` Class

Open the class file. This time the constructors are done. Sally’s comments direct you to where you need to add the custom methods.

1. Code a ToString() method that just returns the `value` of a `PositionType` object.
1. Use the Generate option again to add the `Equals()` and `GetHashCode()` methods. Refer to the [final section](https://education.launchcode.org/csharp-web-development/chapters/classes-part2/equals-shortcut.html) of the “Classes and Objects, Part 2” chapter if you need a quick review.
1. Assume that two `PositionType` objects are equal when their `id` fields match.

#### Run TestTask2 tests

Uncomment the tests inside the `TestTask2`class.  Look for the `TODO`s to help you find the multi-line comments marks.

Run your `TestTask2` unit tests. 

Refactor your code as needed. 

Do not start Task 3 until you have passed all of Task 2’s auto-grading unit tests.

{{% notice green "Tip" "rocket" %}}
Now would be a good time to save, `commit`, and `push` your work up to GitHub.
{{% /notice %}}

### Task 3: Complete the `Job` Class

{{% notice orange "Warning" "rocket" %}}
Due to the fact that this code is being auto-graded as you work through it, make sure that you use any and all names for classes, variables, methods, etc provided to you in these directions.
{{% /notice %}}

Now open the Job file and follow the TODO prompts to remove the comment markers. 

OOF! There are a lot of fields and properties declared and not much else.

1. Code a constructor to initialize the `id` field with a unique value. This constructor should take no parameters.
1. Code a second constructor that takes 5 parameters and assigns values to `name`, `employerName`, `employerLocation`, `jobType`, and `jobCoreCompetency`. Also, this constructor should call the first in order to initialize the `id` field.
1. Generate the `Equals()` and `GetHashCode()` methods. Consider two `Job` objects equal when their id fields match.

#### Run TestTask3 tests

Uncomment the tests inside the `TestTask3`class.  Look for the `TODO`s to help you find the multi-line comments marks.

Run your `TestTask3` unit tests. 

Refactor your code as needed. 

Do not start Task 4 until you have passed all of Task 3’s auto-grading unit tests.

{{% notice green "Tip" "rocket" %}}
Now would be a good time to save, `commit`, and `push` your work up to GitHub.
{{% /notice %}}

### Task 4: Use Unit Testing to Verify Parts of the `Job` Class

{{% notice orange "Warning" "rocket" %}}
Due to the fact that this code is being auto-graded as you work through it, make sure that you use any and all names for classes, variables, methods, etc provided to you in these directions.
{{% /notice %}}

The solution currently contains a testing project called `TechJobs.Tests`. If you open this project, you will find a class called `JobTests` You will need to add the appropriate dependency to `TechJobs.Tests` to test the classes in the `TechJobsOO` project. The `JobTests` file will hold all of the tests for the `Job

#### Initial Setup

Inside JobTests, 
1. Delete the `TestMethod` test.
1. Initialize 4 job objects starting at line 7. This will save you a lot of time while creating your unit tests.

<!-- this is not a very pretty codeblock -->
```csharp {linenos=true,linenostart=7}
//Testing objects
Job job1 = new Job();
Job job2 = new Job();
Job job3 = new Job("Product tester", new Employer("ACME"), new Location("Desert"), new PositionType("Quality control"), new CoreCompetency("Persistence"));
Job job4 = new Job("Product tester", new Employer("ACME"), new Location("Desert"), new PositionType("Quality control"), new CoreCompetency("Persistence"));
```

You can now use these testing objects in your unit tests.

#### Test the Empty Constructor

Each `Job` object should contain a unique ID number, and these should also be sequential integers.

1. In `JobTests`, define a test called `TestSettingJobId`.
1. Using `job1` and `job2`, compare two empty constructor Job objects. Use `Assert.AreEqual`, `Assert.IsTrue`, or `Assert.IsFalse` to test that the ID values for the two objects are NOT the same and differ by 1.
   1. How could you compare `Id` numbers?
   1. How could you test the incrementing amount?
1. Run the test to verify that your `Job()` constructor correctly assigns ID numbers.
1. If the test doesn’t pass, what should be your first thought?
   1. “I need to fix the unit test.”
   1. “I need to fix my `Job()` constructor code.”

{{% notice orange "Warning" "rocket" %}}
Your test code might be incorrect, but that should not be your FIRST thought. TDD begins with writing tests for desired behaviors. If the tests fail, that indicates errors in the methods trying to produce the behavior rather than in the tests that define that behavior.
{{% /notice %}}

#### Test the Full Constructor

Each `Job` object should contain six properties—`Id`, `Name`, `EmployerName`, `EmployerLocation`, `JobType`, and `JobCoreCompetency`.
1. In `JobTest`, define a test called `TestJobConstructorSetsAllFields`.
1. Select one of the `Job` objects with the full constructor to test that the object is assigned the correct properties.
1. Use `Assert` statements to test that the constructor correctly assigns the value of each field as follows:
   1. `"Product tester"` for `Name`
   1. `"ACME"` for `EmployerName`
   1. `"Desert"` for `JobLocation`
   1. `"Quality control"` for `JobType`
   1. `"Persistence"` for `JobCoreCompetency`

{{% notice blue "Note" "rocket" %}}
We are not testing `Id` at the moment.
{{% /notice %}}

#### Test the `Equals()` Method
Two `Job` objects are considered equal if they have the same `id` value, even if one or more of the other fields differ. Similarly, the two objects are NOT equal if their `id` values differ, even if all the other fields are identical.
1. In `JobTest`, define a test called `TestJobsForEquality`.
1. Select any of the two `Job` objects. Test that `Equals()` returns `false`.

It might seem logical to follow up the false case by testing to make sure that `Equals()` returns true when two objects have the same ID. However, the positive test is irrelevant in this case.

The way you build your `Job` class, each `id` field gets assigned a unique value, and the class does not contain a setter for the `id` field. You also verified that each new object gets a different ID when you tested the constructors. Without modifying the constructors or adding a setter, there is no scenario in which two different jobs will have the same ID number. Thus, we can skip the test for this condition.

#### Run TestTask4 tests

Uncomment the tests inside the `TestTask4`class.  Look for the `TODO`s to help you find the multi-line comments marks.

Run your `TestTask4` unit tests. 

Refactor your code as needed. 

Do not start Task 5 until you have passed all of Task 4’s auto-grading unit tests.

{{% notice green "Tip" "rocket" %}}
Now would be a good time to save, `commit`, and `push` your work up to GitHub.
{{% /notice %}}


