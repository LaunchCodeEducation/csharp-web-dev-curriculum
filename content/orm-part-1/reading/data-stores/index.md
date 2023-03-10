---
title: "Working with Data Stores"
date: 2023-01-30T09:32:46-06:00
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



## Check Your Understanding

{{% notice green "Question" "rocket" %}}
   **True/False:** The only methods available for querying objects within a `DbSet` are `Add`, `Remove`, `ToList`, and `Find`.

   <!-- ans: False. While these are the only methods introduced in this section, there are many more
 -->
{{% /notice %}}


{{% notice green "Question" "rocket" %}}
   Which `DbContext` method must be called in order to push changes to the database?

   1. `Save`
   1. `SaveAll`
   1. `PushChanges`
   1. `SaveChanges`

   <!-- ans: `SaveChanges` -->

   <!-- ans: False - we have to use a migration to create the table
 -->
{{% /notice %}}