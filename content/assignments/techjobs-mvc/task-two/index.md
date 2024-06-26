---
title: "Task 2: Complete ListController"
date: 2023-01-05T13:58:39-06:00
draft: false
weight: 2
originalAuthor: Sally Steuterman # to be set by page creator
originalAuthorGitHub: gildedgardenia # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

Complete the `Jobs()` action method in `ListController`. Right now, it returns a view, but we need to send some details about jobs to that view.

1. The view relies on `ViewBag.jobs`, so to start create a list in the action method called `jobs`.
1. If the user selects "View All", you should use `JobData.FindAll()` to populate `jobs` with all the jobs and update `ViewBag.title`. If the user selects something specific, you should use `JobData.FindByColumnAndValue()` to populate `jobs` with jobs that only match that criteria and update `ViewBag.title` to include the criteria the user chose.
1. Make sure to set `ViewBag.jobs` equal to `jobs` and run the program to see how it is working now!

If everything looks good to you, run the tests in `TestTaskTwo` in `AutogradingTests` to make sure you are on the right track before proceeding to task three.