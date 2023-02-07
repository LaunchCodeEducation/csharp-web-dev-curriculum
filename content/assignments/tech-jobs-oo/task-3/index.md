---
title: "Task 3: Complete the Job Class"
date: 2023-01-11T13:15:59-06:00
draft: false
weight: 4
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

Now open the Job file and follow the TODO prompts to remove the comment markers. 

OOF! There are a lot of fields and properties declared and not much else.

1. Code a constructor to initialize the `id` field with a unique value. This constructor should take no parameters.
1. Code a second constructor that takes 5 parameters and assigns values to `name`, `employerName`, `employerLocation`, `jobType`, and `jobCoreCompetency`. Also, this constructor should call the first in order to initialize the `id` field.
1. Generate the `Equals()` and `GetHashCode()` methods. Consider two `Job` objects equal when their id fields match.

### Run TestTask3 tests

Uncomment the tests inside the `TestTask3`class.  Look for the `TODO`s to help you find the multi-line comments marks.

Run your `TestTask3` unit tests. 

Refactor your code as needed. 

Do not start Task 4 until you have passed all of Task 3’s auto-grading unit tests.

{{% notice green "Tip" "rocket" %}}
Now would be a good time to save, `commit`, and `push` your work up to GitHub.
{{% /notice %}}

On to [Task 4]({{< relref "../tech-jobs-oo/task-4.md" >}}).