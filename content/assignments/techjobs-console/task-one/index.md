---
title: "Task One"
date: 2023-01-03T10:42:56-06:00
draft: false
weight: 2
originalAuthor: Sally Steuterman # to be set by page creator
originalAuthorGitHub: gildedgardenia # to be set by page creator
reviewer: # to be set by the page reviewer
reviewerGitHub: # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

## Implement `PrintJobs()`

When trying out the program, and later when reading the code, you
hopefully noticed that there's some work to do in the `PrintJobs()`
method. As it stands, it currently just prints a message:
`"PrintJobs is not implemented yet"`.

Complete this method. Print out jobs *matching the below format*:

```bash
   *****
   position type: Data Scientist / Business Intelligence
   name: Sr. IT Analyst (Data/BI)
   employer: Bull Moose Industries
   location: Saint Louis
   core competency: Statistical Analysis
   *****

   *****
   position type: Web - Back End
   name: Ruby specialist
   employer: LaunchCode
   location: Saint Louis
   core competency: Javascript
   *****
```

For the autograding script to correctly grade your code, you'll need to match this format *exactly*. In particular, note the number of asterisks surrounding each listing, and the blank line between listings.

If there are no results, it should print `No results`. Again, you should use this *exact* message.

{{% notice green "Tip" "rocket" %}}

   To do this, you'll need to iterate over a `List` of jobs. Each
   job is itself a `Dictionary`. While you can get each of the items out of
   the `Dictionary` using the known keys (`employer`, `location`, etc.),
   think instead about creating a nested loop to loop over each
   `Dictionary`. If a new field is added to the job records, this approach
   will print out the new field without any manual updates to `PrintJobs()`.

{{% /notice %}}

{{% notice orange "Warning" "rocket" %}}

   To create new lines for your output, use `Environment.NewLine`. Traditionally `\n` is a new line in Mac OS and `\r\n` is new line in Windows. `Environment.NewLine`  is the universal way to create a new line and works regardless of your operating system.  Allowing code written on a Mac to pass unit tests when the same code is run on Windows. 

{{% /notice %}}

Test this method manually before moving on to your next task:

1. Save your changes.
1. Run the project.
1. Select "1" to list the jobs, and then "0" to list them all.
1. Make sure the printout matches the styling above.
1. Test that it prints a descriptive message if no jobs are found by selecting
   "0" to search and then "3" to search for a location. Then enter a location
   that is not in the data (e.g. "Cancun"). Your message should be displayed.