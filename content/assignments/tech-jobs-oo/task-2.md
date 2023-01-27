---
title: "Task 2: Complete the Support Classes"
date: 2023-01-11T13:15:59-06:00
draft: false
weight: 3
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

Sally needs you to build up the remaining classes. In each case, refer to the Employer class for hints on how to structure your code.



### The `Location` Class

Open the Location.cs file. Note that the methods for this class are done, as is the constructor for initializing the Id property.

Sally left you a `TODO` comment with instructions for coding a second constructor:
1. It should call the first constructor to initialize the id field.
1. It must also initialize the value field for a new Location object.

{{% notice blue "Note" "rocket" %}}
To locate all of the `TODO`s for Task 2, use the Task List feature in Visual Studio.

[Windows Users](https://learn.microsoft.com/en-us/visualstudio/ide/using-the-task-list?view=vs-2022): To open Task List, select **View** > **Task List**

[Mac Users](https://learn.microsoft.com/en-us/visualstudio/ide/reference/task-list-environment-options-dialog-box?view=vs-2022): To open Task List, select **View** > **Tasks**
{{% /notice %}}

### The `CoreCompetency` Class

Open the class file. In this case, the constructors and custom methods are ready. Sally needs you to change the `id` and `value` fields to auto-implemented properties, but NOT `nextId`.

### The `PositionType` Class

Open the class file. This time the constructors are done. Sally’s comments direct you to where you need to add the custom methods.

1. Code a ToString() method that just returns the `value` of a `PositionType` object.
1. Use the Generate option again to add the `Equals()` and `GetHashCode()` methods. Refer to the [final section](https://education.launchcode.org/csharp-web-development/chapters/classes-part2/equals-shortcut.html) of the “Classes and Objects, Part 2” chapter if you need a quick review.
1. Assume that two `PositionType` objects are equal when their `id` fields match.

### Run TestTask2 tests

Uncomment the tests inside the `TestTask2`class.  Look for the `TODO`s to help you find the multi-line comments marks.

Run your `TestTask2` unit tests. 

Refactor your code as needed. 

Do not start Task 3 until you have passed all of Task 2’s auto-grading unit tests.

{{% notice green "Tip" "rocket" %}}
Now would be a good time to save, `commit`, and `push` your work up to GitHub.
{{% /notice %}}

On to [Task 3]({{< relref "../tech-jobs-oo/task-3.md" >}}).