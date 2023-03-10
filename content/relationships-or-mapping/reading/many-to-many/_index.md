---
title: "Creating a Many-to-Many Relationship"
date: 2022-12-15T09:16:07-06:00
draft: false
weight: 5
originalAuthor: John Woolbright # to be set by page creator
originalAuthorGitHub: jwoolbright23 # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: 12/15/22 # UPDATE ANY TIME CHANGES ARE MADE
---
Let's set up a many-to-many relationship between `Event` and `Tag`.

{{% notice blue "Note" "rocket" %}}
The following walkthrough is a continuation of the `Some Setup` chapter. If you have not completed the steps in the `Some Setup` walkthrough you will need to revisit them before continuing.
{{% /notice %}}

## Join Tables

To relate data in a many-to-many fashion in a relational database requires a new type of SQL table.

One-to-many relationships are established at the database level by the use of a foreign key column on one side of the relationship. Our `Events` table has a foreign key column: `CategoryId`. 

For each `Events` row, the column `CategoryId` contains the `Id` of a `Categories` row. This is the primary key of the row in `Categories` that the `Events` row is related to. The `Event`/`EventCategory` relationship is many-to-one, so *many* event rows may have the same `CategoryId` value. 

Using foreign and primary keys to create many-to-many relationships is a bit trickier. In order to relate rows in `Events` to rows in `Tag`, we need need a third table, known as a **join table**. A join table consists of two columns, each of which is a foreign key column to another table. Each row in a join table represents a relationship between one row in each of the two tables being joined. This technique enables many-to-many relationships.

Consider some example data in our `Events` and `Tags` tables.

### Sample Events Data

| Id | Name | CategoryId |
|-----|-----|-----|
| 13 | WWDC  | 2 |
| 15 | SpringOne Platform | 2 |
| 17 | Java Meetup | 3 |

### Sample Categories Data

| Id | Name |
|-----|-----|
| 2 | Conference |
| 3 | Meetup |

### Sample Tags Data

| Id | Name |
|-----|-----|
| 4 | ios |
| 5 | spring |
| 6 | java |

A join table for these two tables would be called `EventTags`, and would have two columns, `EventsId` and `TagsId`. Each of these columns are foreign key columns into their respective tables. 

If we want to relate the `ios` tag to the `WWDC` event, we create a new row in `EventTags`:

### Join table with a single relationship

| EventId | TagId |
|-----|-----|
| 13 | 4 |

We can do this again and again to generate more relationships. Let's revisit the many-to-many diagram from earlier in the chapter. 

![Three Event objects on the left, with various relationships to three Tag objects on the right](pictures/many-to-many.png?classes=border)

The join table representing these relationships looks like this:

| EventsId | TagsId |
|-----|-----|
| 13 | 4 |
| 15 | 5 |
| 15 | 6 |
| 17 | 7 |

Notice that join table doesn't have an explicit primary key column. Values in both `EventsId` and `TagsId` may be duplicated in each column. Indeed, this is the exact property of a join table that allows many-to-many relationships. A join table makes use of a new type of primary key, called a **composite primary key**. A composite primary key is a combination of columns that is unique and functions as a primary key. So, for example, the primary key of the first row of the example just above is the pair (13, 4). This combination is unique, because the objects with the two IDs can be related to each other in only one way. 

In order to enable many-to-many relationships with EF, we need a class to model a join table.

## Many to Many Relationship

To model a join table for `Event` and `Tag` classes, we will provide a collection navigation property on both sides of the relationship. 

Within the `Event.cs` class we add the following collection property of type `Tags`:

```csharp {linenos=table}
public ICollection<Tag>? Tags { get; set; }
```

Within the `Tag.cs` class we add a collection property of type `Events` to the other side of the relationship:

```csharp {linenos=table}
public ICollection<Event>? Events { get; set; }
```

## Join Entity Type Configuration

Since our join table will make use of a composite primary key, we need to add some additional configuration to `EventDbContext`.

```csharp {linenos=table}
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
   modelBuilder.Entity<Event>()
         .HasOne(p => p.Category)
         .WithMany(b => b.events);

   modelBuilder.Entity<Event>()
         .HasMany(p => p.Tags)
         .WithMany(p => p.Events)
         .UsingEntity(j => j.ToTable("EventTags"));
}
```

The method `OnModelCreating` can be overridden from the base class, `DbContext`, in order to provide additional configuration for the data store. In this case, we add code that configures `EventTag` to have a composite primary key consisting of the properties/columns `EventId` and `TagId`.

Before proceeding, create and apply a database migration. Be sure to use a unique and descriptive migration name. After running the migration, verify that there is a new join table, `EventTags`.

## Adding a `Tag` to an `Event`

Now that we have established a many-to-many relationship between `Event` and `Tag`, we can write controller and view code to allow users to add tags to events.

For a user to be able to add a tag to an event, they will need a view in which to do so. Our approach will be to create a view at the path `/Tag/AddEvent/X`, where `X` is a path parameter containing the ID of the event we want to add a tag to.

This new view will contain a form with a dropdown that will allow the user to select the tag to add to the event with ID ``X``. To model this form data, we need a new ViewModel.

### `ViewModels/AddEventTagViewModel`

```csharp {linenos=table}
using System;
using CodingEvents.Models;
using Microsoft.AspNetCore.Mvc.Rendering;

namespace CodingEvents.ViewModels
{
    public class AddEventTagViewModel
    {

        public int EventId { get; set; }
        public Event? Event { get; set; }

        public List<SelectListItem>? Tags { get; set; }

        public int TagId { get; set; }

        public AddEventTagViewModel(Event theEvent, List<Tag> possibleTags)
        {
            Tags = new List<SelectListItem>();

            foreach (var tag in possibleTags)
            {
                Tags.Add(new SelectListItem
                {
                    Value = tag.Id.ToString(),
                    Text = tag.Name
                });
            }

            Event = theEvent;
        }

        public AddEventTagViewModel()
        {
        }
    }

}
```

This class models the data that is needed to render and process our form. In order to add a tag to an event, our `POST` handler will need to know the IDs of the two objects in question. Therefore, our ViewModel has required `EventId` and `TagId` properties. It also contains an `Event` property, which we will use to display details (such as the event name) in the view.

Finally, the ViewModel has a property `List<SelectListItem> Tags`. As with previous forms containing a dropdown, this property will be used to populate the `select` element containing the all of the tag options. 

The constructor requires an `Event` object as well as a `List<Tag>` object. The list will contain a collection of all tags pulled from the database when we call the constructor from within our controller.

Now, let's create the view template.

### `Views/Tag/AddEvent.cshtml`

Our template needs a form with two inputs. The more obvious input will be the `select` element containing tag options. Since we also need to submit the event ID in our request, we'll add a hidden input that holds the value of `EventId` from our ViewModel.

```html {linenos=table}
@model CodingEvents.ViewModels.AddEventTagViewModel

<h1>Add Tag to Event: @Model.Event.Name</h1>

<form asp-controller="Tag" asp-action="AddEvent" method="post">
   <input type="hidden" value="@Model.Event.Id" name="EventId" />
   <div class="form-group">
      <label asp-for="TagId">Tag</label>
      <select asp-for="TagId" asp-items="Model.Tags"></select>
      <span asp-validation-for="TagId"></span>
   </div>
   <input type="submit" value="Add Tag" />
</form>
```

### `GET` and `POST` Handlers

We're now ready to add handler methods to `TagController`.

The `GET` method is simple since it just displays the form.

```csharp {linenos=table}
// responds to URLs like /Tag/AddEvent/5 (where 5 is an event ID)
public IActionResult AddEvent(int id)
   {
      Event theEvent = context.Events.Find(id);
      List<Tag> possibleTags = context.Tags.ToList();

      AddEventTagViewModel viewModel = new AddEventTagViewModel(theEvent, possibleTags);
      
      return View(viewModel);
   }
```

This method creates an `AddEventTagViewModel` using the event specified by the `id` parameter and the list of all tags from the database. Then it renders the view.

The `POST` method is more complicated.

```csharp {linenos=table}
[HttpPost]
   public IActionResult AddEvent(AddEventTagViewModel viewModel)
   {
      if (ModelState.IsValid)
      {
            int eventId = viewModel.EventId;
            int tagId = viewModel.TagId;

            Event theEvent = context.Events.Include(p => p.Tags).Where(e => e.Id == eventId).First();
            Tag theTag = context.Tags.Where(t => t.Id == tagId).First();

            theEvent.Tags.Add(theTag);

            context.SaveChanges();

            return Redirect("/Events/Detail/" + eventId);
      }

      return View(viewModel);
   }
```

This action method takes in a `AddEventTagViewModel` object which will be created via model binding. Assuming validation passes (that is, both `EventId` and `TagId` are not `null`) we create a new `EventTag` object and save it to the database. Then we redirect to the detail view for the given event.

With this code, we can now add a tag to an event. Start up the application and test it out. In order to verify that everything worked, you'll need to look at the `EventTag` table in the database to verify a new row is created upon form submission. 

In the next section, we'll work to display tags in the view.

## Displaying Tags in the Detail View

Now that we have `EventTags` data in the database, let's display the tags for a given event in the view.

We want an event's tags to be displayed on its detail view, so let's start in `EventsController`. The `Detail` method needs to pass in tag data for the given event. To do this, we must use another `.Include()` statement with a lambda expression for `Tags`.

```csharp {linenos=table}
public IActionResult Detail(int id)
   {
   Event theEvent = context.Events
      .Include(e => e.Category)
      .Include(e => e.Tags)
      .Single(e => e.Id == id);

   EventDetailViewModel viewModel = new EventDetailViewModel(theEvent);
   return View(viewModel);
   }
```

Now let's move into `EventDetailsViewModel`. Here, we add data related to an event's tags to pass into the view.

First, add a new string property named `TagText`.

```csharp {linenos=table}
public string TagText { get; set; }
```

Then in the constructor, add a parameter to represent the list of all of `EventTag` objects associated with a given `Event`. Use this parameter to set the value of `TagText`.

```csharp {linenos=table}
public EventDetailViewModel(Event theEvent, List<EventTag> eventTags)
{
   EventId = theEvent.Id;
   Name = theEvent.Name;
   Description = theEvent.Description;
   ContactEmail = theEvent.ContactEmail;
   CategoryName = theEvent.Category.Name;

   TagText = "";
   for (var i = 0; i < eventTags.Count; i++)
   {
         TagText += ("#" + eventTags[i].Tag.Name);
         if (i < eventTags.Count - 1)
         {
            TagText += ", ";
         }
   }
}
```

We build up the contents of `TagText` by looping over `eventTags` and appending tag names, separated by commas. For example, if an event has tags with names `"java"`, `"csharp"`, and `"object-oriented"`, then the `TagList` will be `"#java, #csharp, #object-oriented"`. 

Displaying this data in the view is straightforward. In `Views/Events/Detail.cshtml`, add an additional row to the table.

```html {linenos=table}
<tr>
   <th>Tags</th>
   <td>@Model.TagText</td>
</tr>
```

Now, any tags associated with the given event will display nicely.

To make it easy for users to add a tag to an event, add the following link below the table.

```html {linenos=table}
<a asp-controller="Tag" asp-action="AddEvent" asp-route-id="@Model.EventId">Add Tag</a>
```

This creates a URL of the form `/Tag/AddEvent/X`, where `X` is the ID of the given event.

## Preventing Errors When Adding a Tag

With the current state of our code, attempting to add a tag to an event that already has that tag results in an error. This is because the `EventId`/`TagId` combination is the primary key for our join table, and primary keys must be unique. 

Let's address this scenario.

There are multiple ways to address this issue. The approach we take is to allow the user to submit a form with a potentially duplicate `EventId`/`TagId` combination and add a check in the `POST` handler.

Within `Controller/TagController.cs` update the `AddEvent` (`POST` handler) code to look like this:

```csharp {linenos=table}
[HttpPost]
public IActionResult AddEvent(AddEventTagViewModel viewModel)
{
   if (ModelState.IsValid)
   {

         int eventId = viewModel.EventId;
         int tagId = viewModel.TagId;

         List<EventTag> existingItems = context.EventTags
            .Where(et => et.EventId == eventId)
            .Where(et => et.TagId == tagId)
            .ToList();

         if (existingItems.Count == 0)
         {
            EventTag eventTag = new EventTag {
               EventId = eventId,
               TagId = tagId
            };
            context.EventTags.Add(eventTag);
            context.SaveChanges();
         }

         return Redirect("/Events/Detail/" + eventId);
   }

   return View(viewModel);
}
```
<!-- TODO: double check that the below lines of code are correctly numbered -->
Lines 68-71 query for existing `EventTag` objects that have the some `EventId`/`TagId` pair. In other words, `existingItems` will be empty unless that given event already has the given tag. Before creating and saving a new `EventTag` object, we check the size of `existingItems`, skipping this step if the event already has the tag.

## Display Items With a Given Tag

In addition to seeing which tags are on an event, we would also like to see all events with a specific tag.

We start by creating a `Detail` action in `Controllers/TagController.cs`. This action method should retrieve all `EventTag` objects with a given `TagId`.

```csharp {linenos=table}
public IActionResult Detail(int id)
{
   List<EventTag> eventTags = context.EventTags
         .Where(et => et.TagId == id)
         .Include(et => et.Event)
         .Include(et => et.Tag)
         .ToList();

   return View(eventTags);
}
```

Here's a breakdown of this query:
<!-- TODO: double check the below lines are correctly numbered -->
1. **Line 92** - Filters the collection of all `EventTag` objects down to just those with the given `TagId`.
1. **Line 93** - Eager loads the `Event` child object.
1. **Line 94** - Eager loads the `Tag` child object.
1. **Line 95** - Converts the `DbSet` to a list.

This controller is accessible at the route `/Tag/Detail/X` where `X` is the ID of a specific tag.

The view is similar to other listings that we have created.

```html {linenos=table}
@model List<CodingEventsDemo.Models.EventTag>

@if (Model.Count == 0)
{
   <h1>No elements with the given tag</h1>
}
else
{
   <h1>Events Tagged: @Model[0].Tag.Name</h1>

   <ul>
      @foreach (var evtTag in Model)
      {
         <li>@evtTag.Event.Name</li>
      }
   </ul>

}
```

Finally, we add links to the name of each tag in our tag index.

`Views/Tag/Index.cshtml`:

```html {linenos=table}
<tr>
      <td>@tag.Id</td>
      <td><a asp-controller="Tag" asp-action="Detail" asp-route-id="@tag.Id">@tag.Name</a></td>
</tr>
```

Start the app up and test user behavior. Viewing the main tag listing should allow you to click on each tag name and view the events that have that tag.

## Check Your Understanding

{{% notice green "Question" "rocket" %}}
The use of join tables enables (select all that apply):

1. A database where you never need to run a `JOIN` query.
1. Many-to-many relationships between tables.
1. Many-to-many relationships between classes without creating a join class.
1. Rainbows and butterflies to be stored in your database.
{{% /notice %}}

{{% notice green "Question" "rocket" %}}
**True/False:** A join table does not have a primary key.
{{% /notice %}}

{{% notice green "Question" "rocket" %}}
Which ``EventDbContext`` property allows you to access `Tag` objects that are related to an `Event` object?

1. `DbSet<Event> Events`
1. `DbSet<Tag> Tags`
1. `DbSet<EventTag> EventTags`
1. All of the above
{{% /notice %}}