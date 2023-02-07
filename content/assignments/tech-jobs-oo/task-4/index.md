---
title: "Task 4: Use Unit Testing to Verify Parts of the Job Class"
date: 2023-01-11T13:15:59-06:00
draft: false
weight: 5
originalAuthor: Courtney Frey # to be set by page creator
originalAuthorGitHub: speudusa # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: Courtney Frey # update any time edits are made after review
lastEditorGitHub: speudusa # update any time edits are made after review
lastMod: 2023-02-07  # UPDATE ANY TIME CHANGES ARE MADE
---

{{% notice orange "Warning" "rocket" %}}
Due to the fact that this code is being auto-graded as you work through it, make sure that you use any and all names for classes, variables, methods, etc provided to you in these directions.
{{% /notice %}}

The solution currently contains a testing project called `TechJobs.Tests`. If you open this project, you will find a class called `JobTests` You will need to add the appropriate dependency to `TechJobs.Tests` to test the classes in the `TechJobsOO` project. The `JobTests` file will hold all of the tests for the `Job

### Initial Setup

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

### Test the Empty Constructor

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

### Test the Full Constructor

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

### Test the `Equals()` Method
Two `Job` objects are considered equal if they have the same `id` value, even if one or more of the other fields differ. Similarly, the two objects are NOT equal if their `id` values differ, even if all the other fields are identical.
1. In `JobTest`, define a test called `TestJobsForEquality`.
1. Select any of the two `Job` objects. Test that `Equals()` returns `false`.

It might seem logical to follow up the false case by testing to make sure that `Equals()` returns true when two objects have the same ID. However, the positive test is irrelevant in this case.

The way you build your `Job` class, each `id` field gets assigned a unique value, and the class does not contain a setter for the `id` field. You also verified that each new object gets a different ID when you tested the constructors. Without modifying the constructors or adding a setter, there is no scenario in which two different jobs will have the same ID number. Thus, we can skip the test for this condition.

### Run TestTask4 tests

Uncomment the tests inside the `TestTask4`class.  Look for the `TODO`s to help you find the multi-line comments marks.

Run your `TestTask4` unit tests. 

Refactor your code as needed. 

Do not start Task 5 until you have passed all of Task 4’s auto-grading unit tests.

{{% notice green "Tip" "rocket" %}}
Now would be a good time to save, `commit`, and `push` your work up to GitHub.
{{% /notice %}}

On to [Task 5]({{< relref "../tech-jobs-oo/task-5.md" >}}).