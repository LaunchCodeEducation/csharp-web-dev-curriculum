---
title: "Task 5: Use TDD to Build The ToString() Method"
date: 2023-01-11T13:15:59-06:00
draft: false
weight: 6
originalAuthor: Courtney Frey # to be set by page creator
originalAuthorGitHub: speudusa # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: Terri Penn # update any time edits are made after review
lastEditorGitHub: tpenn # update any time edits are made after review
lastMod: 2023-09-21T12:02:05-5:00 # UPDATE ANY TIME CHANGES ARE MADE
---

{{% notice orange "Warning" "rocket" %}}
Due to the fact that this code is being auto-graded as you work through it, make sure that you use any and all names for classes, variables, methods, etc provided to you in these directions.
{{% /notice %}}

To display the data for a particular `Job` object, you need to implement a custom `ToString()` method. Rather than creating this method and then testing it, you will flip that process using TDD.

### Create First Test for `ToString()`

Before writing your first test, consider how we want the method to behave:
1. When passed a `Job` object, it should return a string that contains a blank line before and after the job information.

The string should contain a label for each field, followed by the data stored in that field. Each field should be on its own line.  There should be a new line between each job listing. 

   ```C# {linenos=true}

   ID:  _______
   Name: _______
   Employer: _______
   Location: _______
   Position Type: _______
   Core Competency: _______


   ID:  _______
   //... more job objects to follow
   ```

1. If a field is empty, the method should add, `“Data not available”` after the label.

We will need three tests to test our `ToString` method.

### Test 1: `TestToStringStartsAndEndsWithNewLine`

In `JobTests`, add a new test called `TestToStringStartsAndEndsWithNewLine` to check the first requirement (item 1 in the above list), then run that test (it should fail).


{{% notice orange "Warning" "rocket" %}}
Only run the unit tests in the `JobTests` class as you work through this Task.


If you were to run the auto-graded tests right now, you will not pass them even if your own unit tests pass.  Once you have all 3 unit tests completed, we will ask you to run the auto-graded tests.  Please make sure you are running the correct tests.
{{% /notice %}}

### Code `ToString()` to Pass Test 1

In the `Job` class, create a `ToString()` method that passes the first test. Since the test only checks if the returned string starts and ends with a blank line, make that happen.

{{% notice green "Tip" "rocket" %}}
Do NOT add anything beyond what is needed to make the test pass. You will add the remaining behaviors for `ToString()` as you code each new test.
{{% /notice %}}

### Test 2: `TestToStringContainsCorrectLabelsAndData`

1. Code a new test for the second required behavior, then run the tests to make sure the new one fails. Call this test `TestToStringContainsCorrectLabelsAndData`.

1. Modify `ToString()` to make the new test pass. Also, make sure that your updates still pass all of the old tests.

1. Continue this test-refactor cycle until all of the behaviors we want for `ToString()` work. Remember to add only ONE new test at a time.

### Test 3: `TestToStringHandlesEmptyField`
1. Code your final test for the last required behavior, then run the tests to make sure the new one fails. Call this test `TestToStringHandlesEmptyField`.

1. Modify `ToString()` to make the new test pass. Also, make sure that your updates still pass all the old tests.

1. Cool! Your `Job` class is now complete and operates as desired.


### Run TestTask5 tests

Uncomment the tests inside the `TestTask5`class.  Look for the `TODO`s to help you find the multi-line comments marks.

Run your `TestTask5` unit tests. 

Refactor your code as needed. 

If the tests are failing, make sure you have uncommented the `TODO` in RunTechJobs.cs.

If you are getting a FileNotFound exception on the EmptyFieldTest.txt and StartsAndEndsWithNewLine.txt files:

>On Windows, right-click on the _EmptyFieldTest.txt_ file and choose _Properties_ from the context menu.  Under _Advanced_->_Copy to Output Directory_, change the setting to `Copy if newer`.  Repeat these steps for the _StartsAndEndsWithNewLine.txt_ file.
>
>{{< rawhtml >}}
><img src="pictures/copy-to-output-directory-win.png" alt="Copy to Output Directory" />
>{{< /rawhtml >}}
> 
>On Mac, you may select both of these files, right-click, choose _Quick Properties_, and then `Copy to Output Directory`.
>
>{{< rawhtml >}}
><img src="pictures/copy-to-output-directory-mac.png" alt="Copy to Output Directory" />
>{{< /rawhtml >}}

Do not start Task 6 until you have passed all of Task 5’s auto-grading unit tests.

{{% notice green "Tip" "rocket" %}}
Now would be a good time to save, `commit`, and `push` your work up to GitHub.
{{% /notice %}}

On to [Task 6]({{< relref "../task-6/index.md" >}}).