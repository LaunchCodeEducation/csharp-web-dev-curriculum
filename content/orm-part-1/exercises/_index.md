---
title: "Exercises: OMG the ORM!"
date: 2023-03-10T09:32:46-06:00
draft: false
weight: 2
originalAuthor: <no value> # to be set by page creator
originalAuthorGitHub: <no value> # to be set by page creator
reviewer: # to be set by the page reviewer
reviewerGitHub: # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

## Exercises

For the exercises, we are going to continue building on our CodingEvents application. The exercise instructions assume that your code resembles the [orm1-with-db](https://github.com/LaunchCodeEducation/CodingEvents/tree/orm1-with-db) branch. Create a new branch in your own CodingEvents repo to get started on the exercises.

{{% notice blue "Note" "rocket" %}}

You will be making one model class and adding to DbContext. If you are not sure what these classes should look like, refer back to the [section]({{< relref "../reading/data-stores/#data-stores-in-the-controller" >}}) on data stores and DbContext.

{{% /notice %}}

## The `EventCategory` Class

First, create a new class called `EventCategory` in the Models directory.

`EventCategory` needs to have the following:

1. An `Id` property of type `int`.
1. A `Name` property of type `string`.
1. A no arg constructor.
1. A constructor that sets the value of `Name`.

`EventCategory` represents data that will be stored in our database.

{{% expand "Check your solution" %}}
```csharp{linenos=table,hl_lines=[],linenostart=6}
public int Id { get; set; }
public string? Name { get; set; }

public EventCategory()
{
}

public EventCategory(string name)
{
   Name = name;
}
```
{{% /expand %}}

## Adding to `DbContext`

Once you have created EventCategory, you need to add to EventDbContext to set up a table in the database for storing categories.

{{% expand "Check your solution" %}}
```csharp{linenos=table,hl_lines=[],linenostart=10}
public DbSet<EventCategory> Categories { get; set; }
```
{{% /expand %}}

## Adding a New Table to the Database

With the two steps completed above, you now need to add a new migration and update your database. You should see a new table in your database!

{{% notice green "Tip" "rocket" %}}
**Where is my table?**
f you are not able to see your new EventCategory table try the following:

1. **Drop tables**
   1. Start by dropping all of your tables in MySql Workbench
   1. Add a new migration in your terminal
   1. Update your database in the terminal
   1. Refresh your schema in MySql Workbench

If you still can’t see your table, then you will need to drop your schema and delete old migrations.

1. Drop schema

   1. Drop the schema in MySql Workbench. Don’t worry, we’ll get it back.
   1. ecreate your schema in MySql Workbench like you did earlier. You can use the same names and passwords if you like. If you change any of the names and passwords, make sure you update your MySql connections that you made in the `Program.cs`.
   1. Delete your old migrations from your C# project.
   1. Add a new migration in your terminal
   1. Update your database in the terminal
   1. Refresh your schema in MySql Workbench

You should see your new table in MySql Workbench now.
{{% /notice %}}

## The `EventCategoryController` Class

Create `EventCategoryController` in the `Controllers` directory. To get our action methods working, we also need a variable of type `EventDbContext`.

For now, we are just going to set up our `Index()` action method so that it displays all of the categories in our table.

### `Index` Action Method

`Index()` needs to do the following:

1. Responds to GET requests at `EventCategory/Index` and returns a view called `Index.cshtml`.  
1. Pass the `DbContext` category values as a list into the view template as a model.

{{% expand "Check your solution" %}}
```csharp{linenos=table,hl_lines=[],linenostart=15}
private EventDbContext context;

public EventCategoryController(EventDbContext dbContext)
{
   context = dbContext;
}

// GET: /<controller>/
public IActionResult Index()
{
   List<EventCategory> categories = context.Categories.ToList();
   return View(categories);

}
```
{{% /expand %}}

## Adding a View

Create an `EventCategory` directory inside of our `Views` directory. Add a new view called `Index.cshtml`.

`Index.cshtml` needs to have the following:

1. Use the list passed in from the action method in the controller as a model to populate the view.
1. An `h1` with an appropriate heading for the page.
1. A table that will display all of the category names of the event categories stored in our database.

{{% expand "Check your solution" %}}
```csharp{linenos=table,hl_lines=[],linenostart=1}
@model List<CodingEventsDemo.Models.EventCategory>

<h1>All Event Categories</h1>

<table>
   <tr>
   <th>Category Name</th>
   </tr>
   @foreach(EventCategory category in Model)
   {
      <tr>
            <td>@category.Name</td>
      </tr>
   }
</table>
```
{{% /expand %}}

## Test Your Application

If you navigate to the `/eventcategory` route, you will see an empty table on the page. That is what you should see! We haven’t added the ability to add a new category to our table yet. We will do so in the studio this chapter.