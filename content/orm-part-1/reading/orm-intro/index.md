---
title: "Introduction to Object-Relational Mapping"
date: 2023-01-30T09:32:46-06:00
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

We are now ready to connect our MVC application to a relational database and add persistent data storage to our apps. To do so, we need to use _object-relational mapping_.

**Object-Relational Mapping** or **ORM** is a technique for converting data between C# objects and relational databases. ORM converts data between two incompatible type systems (C# and MySQL), such that each model class becomes a table in our database and each instance a row of the table.

## Check Your Understanding

{{% notice green "Question" "rocket" %}}
   **True/False:** Writing usernames and passwords in plain text in a file is a GREAT idea!

   <!-- ans: False -->
{{% /notice %}}


{{% notice green "Question" "rocket" %}}
   **True/False:** An ORM converts data between C# objects and relational databases.

   <!-- ans: True -->
{{% /notice %}}


{{% notice green "Question" "rocket" %}}
   **True/False:** We need Entity Framework Core AND a MySQL provider to successfully use ORM in this project.

   <!-- ans: True -->
{{% /notice %}}