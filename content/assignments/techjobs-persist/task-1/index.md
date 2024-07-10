---
title: "Task 1: Connect a Database to an ASP.NET App"
date: 2023-01-05T13:58:39-06:00
draft: false
weight: 1
originalAuthor: Courtney Frey # to be set by page creator
originalAuthorGitHub: speudusa # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

In the `Program.cs` file

1. Start MySQL Workbench and create a new schema named `techjobs`.
   1. In the administration tab, create a new user, `TechJobs` with the same settings described in the `CodingEvents` tutorial and set the password to `TechJobs`.
1. Make sure that the `TechJobs6Persistent` project has all of its necessary dependencies.
   1. `Pomelo.EntityFrameworkCore.MySql`
   1. `Microsoft.EntityFrameworkCore.Design`
   1. `Microsoft.EntityFrameworkCore.Relational`
1. Read through the code that is currently in `JobDbContext` to get an idea of what the database will look like in terms of tables.
1. You will need to add the services required to create your database connection in `Program.cs`, including both the `connectionString` and the `serverVersion`.
1. Run a new migration and update the database.

{{% notice green Tip "rocket" %}}
You can double-check your setup against what you’ve already done for your `CodingEvents` repo. You can copy these property assignments from your `CodingEvents` repo, only needing to change the database address and username/password values.
{{% /notice %}}

## Test It with SQL
If you correctly connect to your database, you should have tables for `Jobs`, `Employers`, and `Skills`.

1. In your MySQL workbench, open a new query tab to check your database connection.
   1. Do you see tables?
   1. Do your tables have columns?

### SQL TASK: 
In `queries.sql` under “Task 1”, list the columns and their data types in the `Jobs` table.  Write this answer as a comment. 

{{% notice blue "Progress Check" "rocket" %}}

**Project Check:** You should be able to connect to your MySQL database and perform an initial migration. Your project should open a localhost browser window with a header that reads: “Tech Jobs & Persistent Data” with a message below that there are no jobs yet.

If you click through the application, you will see that not every page is functional.  You will be addressing this as you work through the next tasks below.

**Database check:** You should have empty tables.

{{% /notice %}}

You are ready for [Task 2]({{< relref "../task-2/" >}}).