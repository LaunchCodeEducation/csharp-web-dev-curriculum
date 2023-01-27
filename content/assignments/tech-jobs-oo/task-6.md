---
title: "Task 6: Refactor to DRY the Support Classes"
date: 2023-01-11T13:15:59-06:00
draft: false
weight: 7
originalAuthor: Courtney Frey # to be set by page creator
originalAuthorGitHub: speudusa # to be set by page creator
reviewer: # to be set by the page reviewer
reviewerGitHub: # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

{{% notice orange "Warning" "rocket" %}}
Due to the fact that this code is being auto-graded as you work through it, make sure that you use any and all names for classes, variables, methods, etc provided to you in these directions.
{{% /notice %}}

Review the code in the `Employer`, `Location`, `CoreCompetency`, and `PositionType` classes. What similarities do you see?

There is a fair amount of repetition between the classes. As a good coder, anytime you find yourself adding identical code in multiple locations you should consider how to streamline the process.
DRY = “Don’t Repeat Yourself”.

### Create a Base Class
Let’s move all of the repeated code into a separate class. We will then have `Employer`, `Location`, `CoreCompetency`, and `PositionType` inherit this common code.
1. Create a new class called `JobField`.
1. Consider the following questions to help you decide what code to put in the `JobField` class:
   1. What fields do ALL FOUR of the classes have in common?
   1. Which constructors are the same in ALL FOUR classes?
   1. Which custom methods are identical in ALL of the classes?
1. In `JobField`, declare each of the common class members.
1. Code the constructors.
1. Add in any inherited method overrides.
1. Finally, to prevent the creation of a `JobField` object, make this class abstract.

### Extend JobField into Employer
Now that you have the common code located in the JobField file, we can modify the other classes to reference this shared code. Let’s begin with Employer.

1. Modify line 4 to extend the `JobField` class into `Employer`.
1. Next, remove any code in `Employer` that matches code from JobField (e.g. the `Id` and `Value` properties and the `nextId` field are shared).
1. Remove any of the methods that are identical.
1. The empty constructor is shared, but not the second. Replace the two constructors with the following:
   ```csharp {linenos=true,hl_lines=[1,3],linenostart=4}
   public class Employer : JobField
	{
        public Employer(string value) : base(value)
        {
        }
   }
   ```
1. Rerun your unit tests to verify your refactored code.

### Finish DRYing Your Code
Repeat the process above for the `Location`, `CoreCompetency`, and `PositionType` classes.

Rerun your unit tests to verify that your classes and methods still work.

### Run TestTas6 tests

Uncomment the tests inside the `TestTask6`class.  Look for the `TODO`s to help you find the multi-line comments marks.

Run your `TestTask6` unit tests. 

Refactor your code as needed. This is the last set of tests! Congrats! 

Submit your assignment once you have passed all of Task 6’s auto-graded unit tests.


{{% notice green "Tip" "rocket" %}}
Now would be a good time to save, `commit`, and `push` your work up to GitHub.
{{% /notice %}}

On to [your final steps]({{< relref "../tech-jobs-oo/final-steps.md" >}}).
