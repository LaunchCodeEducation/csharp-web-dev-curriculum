---
title: "Working with Data Stores"
date: 2023-03-10T09:32:46-06:00
draft: false
weight: 4
originalAuthor: Courtney Frey # to be set by page creator
originalAuthorGitHub: speudusa # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

With our data store and persistent class configured, we are ready to realize the full power of ORM.

## Data Stores in the Controller


Since our data store, `EventDbContext`, extends `DbContext`, we have access to all of the methods defined by `DbContext`. There are quite a few such methods (see the [documentatio](https://learn.microsoft.com/en-us/dotnet/api/microsoft.entityframeworkcore.dbcontext?view=efcore-6.0#methods) for details), but we will only use `SaveChanges`.

We will make more extensive use of the `Events` property of `EventDbContext`, which is of type `DbSet`. As mentioned in the previous section, this property allows us to query for objects directly from the database. It too has [quite a few methods](https://learn.microsoft.com/en-us/dotnet/api/microsoft.entityframeworkcore.dbset-1?view=efcore-6.0#methods), and we will demonstrate usage of `Add`, `Remove`, `ToList`, and `Find`.

### Adding the Data Store

To access data from the database in a controller, we’ll need an instance of EventDbContext. Adding the following code to the top of `EventsController` will make one available as an instance variable of the controller.

```csharp{linenos=table,hl_lines=[],linenostart=17}
  private EventDbContext context;

  public EventsController(EventDbContext dbContext)
  {
    context = dbContext;
  }
```

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