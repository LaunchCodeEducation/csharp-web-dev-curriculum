---
title: "Task Three"
date: 2023-01-03T10:42:56-06:00
draft: false
weight: 4
originalAuthor: Sally Steuterman # to be set by page creator
originalAuthorGitHub: gildedgardenia # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

## Make Search Methods Case-Insensitive

You've completed your first two tasks!

Let's assume you demonstrated the updated application for the Company Team, and
they noticed a feature that could be improved. When searching for jobs with
the skill `"JavaScript"` some results were missing (e.g. the Watchtower
Security job on line 31 of the CSV file). The search methods turn out to be
case-sensitive, so they treat `"JavaScript"` and `"Javascript"` as different
strings.

The Company Team strongly requested that this needs to be fixed, and of course
you told them that you are up to the task.

Here are some questions to ask yourself as you get started:

1. Which methods are called when searching?
1. How is the user's search string compared against the values of fields of the job `Dictionary` objects?
1. How can you make this comparison in a way that effectively ignores the case of the strings?
1. How can you do this *without* altering the capitalization of the items in `AllJobs` so that the data gets printed out the same way that it appears in `job_data.csv`?

You might find it useful to review the [String methods]({{< relref "../../../data-types-and-variables/reading/strings-chars-and-arrays/#string-manipulation" >}}) listed in the
chapter.

When this task is completed, you're ready to submit your assignment.