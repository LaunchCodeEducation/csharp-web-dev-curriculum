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


Since our data store, `EventDbContext`, extends `DbContext`, we have access to all of the methods defined by `DbContext`. There are quite a few such methods (see the [documentation](https://learn.microsoft.com/en-us/dotnet/api/microsoft.entityframeworkcore.dbcontext?view=efcore-6.0#methods) for details), but we will only use `SaveChanges`.

We will make more extensive use of the `Events` property of `EventDbContext`, which is of type `DbSet`. As mentioned in the previous section, this property allows us to query for objects directly from the database. It too has [quite a few methods](https://learn.microsoft.com/en-us/dotnet/api/microsoft.entityframeworkcore.dbset-1?view=efcore-6.0#methods), and we will demonstrate usage of `Add`, `Remove`, `ToList`, and `Find`.

### Adding the Data Store

To access data from the database in a controller, we’ll need an instance of EventDbContext. Adding the following code to the top of `EventsController` will make one available as an instance variable of the controller.

```csharp{linenos=table,hl_lines=[],linenostart=16}
private EventDbContext context;

public EventsController(EventDbContext dbContext)
{
  context = dbContext;
}
```

We can now reference `context` anywhere within our controller in order to query the database.

{{% notice blue "Note" "rocket" %}}

It may not be obvious how this code works, since we never explicitly call the constructor for `EventsController`. When we run our application, ASP.NET will call this constructor for us, and will pass in an instance of `EventDbContext`. This is an example of the concept of **dependency injection**, a topic which is fairly complex and beyond the scope of this course.

{{% /notice %}}

## Using Data Store Methods

Let’s refactor our controller to replace each usage of the in-memory store EventData with our instance of EventDbContext.

### `Index` Action Method

The first such usage is in the `Index` method, which displays a listing of all of the events. We are currently calling `EventData`.`GetAll()`. To carry out the equivalent action on context, we can use its Events property.

Instead we want to send the data as a list to `EventDbContext` through the `DbSet`.

{{% notice blue "Check Your Code" "rocket" %}}
```csharp{linenos=table,hl_lines=[3],linenostart=24}
public IActionResult Index()
{
  List<Event> events = context.Events.ToList();

  return View(events);
}
```
{{% /notice %}}

We use the `ToList` method of `context.Events` (recall that this property is a `DbSet`) to fetch a list of all `Event` objects stored in the database.

### Post `Add` Action Method
Our next usage of `EventData` that needs to be replaced is in the `Add` method that handles POST requests. That method is currently calling `EventData.Add(newEvent)` to store a newly created `Event` object. 

Replace `EventData.Add(newEvent)` with the following:

{{% notice blue "Check Your Code" "rocket" %}}
```csharp{linenos=table,hl_lines=[],linenostart=53}
context.Events.Add(newEvent);
context.SaveChanges();
```
{{% /notice %}}

Line 53 adds the object to `context.Events`, which only stores it within that `DbSet` object. For this change to be pushed to the database, we must also call `context.SaveChanges()`.

{{% notice blue "Note" "rocket" %}}
An instance of a persistent class, such as Event, that has not been stored in the database is called a **transient** object.
{{% /notice %}}

### GET `Delete` Action Method

The next usage of `EventData` is in the Delete method that handles GET requests. As in Index, this method is calling `EventData.GetAll()`, which we can replace with `context.Events.ToList()`.

{{% notice blue "Check Your Code" "rocket" %}}
```csharp{linenos=table,hl_lines=[],linenostart=64}
public IActionResult Delete()
{
  ViewBag.events = context.Events.ToList();

  return View();
}
```
{{% /notice %}}

### POST `Delete` Action Method

The final usage of EventData is in the `Delete` method that handles POST requests. That method currently looks like this:

{{% notice blue "Check Your Code" "rocket" %}}
```csharp{linenos=table,hl_lines=[],linenostart=69}
[HttpPost]
public IActionResult Delete(int[] eventIds)
{
  foreach (int eventId in eventIds)
  {
    EventData.Remove(eventId);
  }

  return Redirect("/Events");
}
```
{{% /notice %}}

The method takes in an array of IDs corresponding to objects that should be deleted. It then loops through the array and deletes the corresponding objects one-by-one.

Line 74 can be replaced with the following:

```csharp{linenos=table,hl_lines=[],linenostart=74}
Event? theEvent = context.Events.Find(eventId);
context.Events.Remove(theEvent);
```
The first line searches `context.Events` for an object with the given ID using its Find method. It returns the given object or `null` (if none is found). We can then delete the object by calling the `Remove` method of `context.Events` and passing in the object we want to delete.

Since we have changed the state of context, we must also call `context.SaveChanges()` to make sure these changes get reflected in the database. However, we need only do this after the loop. Since each call to `SaveChanges` results in a database query, this makes our code much more efficient than calling `SaveChanges` within the loop. Instead of several database queries, we have only one.

Our final refactored method looks like this:

```csharp{linenos=table,hl_lines=[],linenostart=69}
[HttpPost]
public IActionResult Delete(int[] eventIds)
{
  foreach (int eventId in eventIds)
  {
    Event? theEvent = context.Events.Find(eventId);
    context.Events.Remove(theEvent);
  }

  context.SaveChanges();

  return Redirect("/Events");
}
```
### File Tree Clean Up
Now that we are no longer using `EventData`, we can delete it from our application. And as always, be sure to start your app and test after refactoring.

{{% notice orange "Warning" "rocket" %}}
Remember that any time you update your database, you need to add a migration to your project and update your database.

If you do not, you will not see any of the changes you made.
{{% /notice %}}


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