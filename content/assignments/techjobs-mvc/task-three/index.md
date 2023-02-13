---
title: "Task 3: Complete SearchController"
date: 2023-01-05T13:58:39-06:00
draft: false
weight: 3
originalAuthor: Sally Steuterman # to be set by page creator
originalAuthorGitHub: gildedgardenia # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

Add a `Results()` action method to `SearchController`:

1. The `Results()` method should take in two parameters. Both parameters must be strings and the first one should be called "searchType" and the second one should be called "searchTerm".
1. First, you need to create a local variable called "jobs" that is of type `List<Job>`.
1. If the user enters "all" in the search box, or if they leave the box empty,
   call the `FindAll()` method from `JobData`. Otherwise, send the search
   information to `FindByColumnAndValue`. In either case, store
   the results in a `jobs` List.
1. Pass `jobs` into the `Index.cshtml` view.
1. Pass `ListController.ColumnChoices` into the view, as the existing `Index()` action method does.

Run the tests in `TestTaskThree` to see how you did!
