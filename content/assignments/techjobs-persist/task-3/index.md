---
title: "Task 3: Creating a Many-To-Many Relationship"
date: 2023-01-05T13:58:39-06:00
draft: false
weight: 3
originalAuthor: Courtney Frey # to be set by page creator
originalAuthorGitHub: speudusa # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

Using a many-to-many relationship, we can apply jobs to multiple skills, and a skill to multiple jobs.  We want to create a table that will track the relationships between both Jobs and Skills.  To do this, we need to tell the `Modelbuilder` which properties to use.  

## Update the `JobDbContext`

1. In the `OnModelCreating` method, we want to create a table called `“JobSkills”`.  This table will use an `Entity` of type `Job`.  It has many `Skills` with many `Jobs`.  It will use `Entity` to create a table named `”JobSkills”`.
1. Run a new migration and update your database to see your new table.

## Test It with SQL
Run your application and make sure you can create a new job with an employer and several skills. You should now also have restored full list and search capabilities.

### SQL Task: 
In `queries.sql` under “Task 3”, write a query to return a list of the names and descriptions of all skills that are attached to jobs in alphabetical order. If a skill does not have a job listed, it should not be included in the results of this query.

{{% notice green Tip "rocket" %}}
 You will need to make use of “is not null”.
{{% /notice %}}


{{% notice blue "Progress Check" "rocket" %}}
**Testing:** Run the tests found in `Task.Tests`.  These should all pass unless your database connections have been set incorrectly.

**Build:** You should have a working website that allows you to make a job, employer, and skill and connect them.  You should be able to see the connections in an the `Job/Detail` view.

**Database:** and see data in MySQL database.  You should see data in your `JobSkills` table.  It should be a pairing of Job and Skill Ids.
{{% /notice %}}


## How to Submit

To turn in your assignment and get credit, follow the [submission instructions]({{< relref "../../hello-world/submit-your-code/" >}}).

## Congrats!
You have successfully completed Graded Assignment 4 in C#! 