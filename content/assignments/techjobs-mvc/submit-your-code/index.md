---
title: "Task 5: Submit Your Code and Bonus Missions"
date: 2023-01-05T13:58:39-06:00
draft: false
weight: 5
originalAuthor: Sally Steuterman # to be set by page creator
originalAuthorGitHub: gildedgardenia # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

## Sanity Check

At this point, all autograding tests should be passing. To be sure, run all the tests at once and if any are failing, evaluate the error message and go back and fix your code.

## How to Submit

To turn in your assignment and get credit, follow the [submission instructions]({{< relref "../../hello-world/submit-your-code/" >}}).

## Bonus Missions

Here are some additional challenges, for those willing to take them on:

1. When we select a given field to search within and then submit, our choice is
   forgotten and returns to "All" by default. Modify the view template to keep
   the previous search field selected when displaying the results.
1. In the tables displaying the full job data, find a way to manipulate the
   font, style, capitalization, etc. to further distinguish the labels from the
   data (e.g. **Employer:** *LaunchCode*). (*Hint:* We capitalize the title
   string in multiple templates, so have a look around).
1. In the tables of the job results, make each value (except `name`)
   hyperlinked to a new listing of all jobs with that same value. For example,
   if we have a list of jobs with the `JavaScript` skill, clicking on a
   location value like `Saint Louis` will generate a new list with all the
   jobs available in that city.