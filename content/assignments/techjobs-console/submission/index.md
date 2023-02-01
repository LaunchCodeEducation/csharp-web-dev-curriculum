---
title: "Submission and Bonus Missions"
date: 2023-01-03T10:42:56-06:00
draft: false
weight: 5
originalAuthor: Sally Steuterman # to be set by page creator
originalAuthorGitHub: gildedgardenia # to be set by page creator
reviewer: # to be set by the page reviewer
reviewerGitHub: # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

## Sanity Check

Before submitting, make sure that your application:

1. Prints each field of a job when using search functionality, and when listing all columns. If there are no search results, a descriptive message is displayed.
1. Allows the user to search for a string across all columns.
1. Returns case-insensitive results.
1. Run the autograding tests to ensure that the tests pass.

## How to Submit

<!-- TODO: Add link back to Assignment 0 -->

To turn in your assignment and get credit, follow the submission instructions.

## Bonus Missions

If you want to take your learning a few steps further, here are some
additional features the company team thinks would be nice to have in our app. We're not providing you much
guidance here, but we have confidence that you can figure how to implement these enhanced features!

1. **Sorting list results**: When a user asks for a list of employers, locations, position types, etc., it would be nice if results were sorted alphabetically. Make this happen.
1. **Returning a copy of AllJobs**: Look at `JobData.FindAll()`. Notice that it's returning the `AllJobs` property, which is a static property of the `JobData` class. In general, this is not a great thing to do, since the person calling our `FindAll()` method could then mess with the data that `AllJobs` contains. Fix this by creating a copy of `AllJobs`. *Hint:* Look at the methods of the `List` class listed in the Microsoft documentation.