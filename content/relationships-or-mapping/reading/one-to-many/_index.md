---
title: "Creating a One-to-Many Relationship"
date: 2022-12-15T09:16:07-06:00
draft: false
weight: 3
originalAuthor: John Woolbright # to be set by page creator
originalAuthorGitHub: jwoolbright23 # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod:  # UPDATE ANY TIME CHANGES ARE MADE
---

The first relationship we implement will be between the `Event` and `EventCategory` classes. We will allow multiple events to be in the same category, but each event will only have one category. Thus, this will be a one-to-many relationship. In this case, we will set up both sides of the relationship, so a many-to-one relationship will result as well.

We are now ready to create a relationship between `Event` and `EventCategory`.

{{% notice blue "Note" "rocket" %}}
The starter code for the following walkthroughs is found at the [orm-1 branch](https://github.com/LaunchCodeEducation/CodingEvents/tree/orm-1) of `CodingEvents`. The final code presented in the following walkthroughs will be found on the [orm2 branch](https://github.com/LaunchCodeEducation/CodingEvents/tree/orm2). As always, code along on your own `CodingEvents` project.
{{% /notice %}}

## Setting Up the Relationship

We want to relate `Event` objects to `EventCategory` objects, and vice versa. Currently, similar functionality is enabled via the `EventType` field of `Event`. However, `EventType` is an enum, which means that new values can not be added without changing the code and re-compiling. Using the persistent ``EventCategory`` class to organize events will be a much more flexible and user-friendly approach. 

### Replacing `EventType` With `EventCategory`

In the `Event` class, replace the `Type` property with a new property of type `EventCategory`. In order for EntityFrameworkCore to be able to persist relationships between `Event` objects and `EventCategory` objects, we must also have a property that stores the `Id` of the given `EventCategory`.

### `Models/Event.cs`

```csharp
public EventCategory Category { get; set; }

public int CategoryId { get; set; }
```
The `CategoryId` property functions as a [foreign key](https://education.launchcode.org/csharp-web-dev-curriculum/). EF will create a `CategoryId` column in the `Event` table. The value of this column for a given row will determine which row in the `Category` table is related to the given event. Our code is now set up so that each `Event` will know about its `EventCategory` object, and that relationship persists.

{{% notice blue "Note" "rocket" %}}
It is *very* important that the ID field corresponding to the `Category` property is named `CategoryId`. This naming convention lets EF know that it should set `Category` to be the object with the `Id` value the same as `CategoryId`. 
{{% /notice %}}

Now, let's remove all references to `EventType` in the project.

Open `AddEventViewModel`, which is in the `ViewModels` directory. Recall that this ViewModel represents the data that is needed to display and process the form used to create new `Event` instances. Replace its `Type` and `EventType` properties with similar properties that use `EventCategory`.

### `ViewModels/AddEventViewModel.cs`

```csharp
[Required(ErrorMessage = "Category is required")]
public int CategoryId { get; set; }

public List<SelectListItem>? Categories { get; set; }
```

The constructor for this class populates the `EventTypes` collection, which we have just removed. This collection stored a collection of `SelectListItem` objects, one for each possible value of `Type`. The corresponding code to work with categories should populate `Categories` with each possible value of `Category`. In other words, `Categories` should have one `SelectListItem` for each item in the `EventCategory` table. 

We'll rely on the controller to provide our constructor with a list of all `EventCategory` objects, so we can update the constructor to look like this:

```csharp {linenos=table}
public AddEventViewModel(List<EventCategory> categories)
{
   Categories = new List<SelectListItem>();

   foreach (var category in categories)
   {
         Categories.Add(new SelectListItem
         {
            Value = category.Id.ToString(),
            Text = category.Name
         });
   }
}
```

The `Value` of each `SelectListItem` will be the `Id` of the given category. The `Id` of a category is unique (in fact, it functions as a primary key) while the `Name` may not be. Therefore, we must use `Id` for the `value` attribute.

Since we no longer have a no-arg constructor, we must add one to allow model binding.

```csharp
public AddEventViewModel()
{
}
```

There are a couple references to `Type` and `EventType`, residing within our `Views/` directory. 

Within the `Views/Events/Add.cshtml` file, update the `select` input and its label to reference our new `Category` and `Categories` properties.

```html
<label asp-for="CategoryId">Category</label>
<select asp-for="CategoryId" asp-items="Model.Categories"></select>
```

Additionally, within the `Views/Events/Index.cshtml` file, update the `Event Type` to `Category` and the `Evt.Type` to `Evt.Category.Name`:

```html
<th>
   Category
</th>
```

```html
<td>@evt.Category.Name</td>
```

Finally, we have a reference to `EventType` in the `EventsController.Add` method that handles POST requests. This method creates a new `Event` object using data from the `AddEventViewModel` parameter.

### `Controllers/EventController.cs`

```csharp {linenos=table}
[HttpPost]
public IActionResult Add(AddEventViewModel addEventViewModel)
{
   if (ModelState.IsValid)
   {
         Event newEvent = new Event
         {
         Name = addEventViewModel.Name,
         Description = addEventViewModel.Description,
         ContactEmail = addEventViewModel.ContactEmail,
         Type = addEventViewModel.Type
         };

         context.Events.Add(newEvent);
         context.SaveChanges();

         return Redirect("/Events");
   }

   return View(addEventViewModel);
}
```

When this method runs, `addEventViewModel` contains form data. The data that specifies which `EventCategory` and `Event` should be assigned to is `CatgoryId` and NOT the `EventCategory` object. Therefore, we must first retrieve the category object, and then pass it into the `Event` constructor.

The code above can be refactored as follows:

```csharp {linenos=table}
[HttpPost]
public IActionResult Add(AddEventViewModel addEventViewModel)
{
   if (ModelState.IsValid)
   {
         EventCategory theCategory = context.Categories.Find(addEventViewModel.CategoryId);
         Event newEvent = new Event
         {
         Name = addEventViewModel.Name,
         Description = addEventViewModel.Description,
         ContactEmail = addEventViewModel.ContactEmail,
         Category = theCategory
         };

         context.Events.Add(newEvent);
         context.SaveChanges();

         return Redirect("/Events");
   }

   return View(addEventViewModel);
}
```

Our app is now free of all references to `EventType`, so we may delete this unused class. 

### Defining the Inverse Relationship

For categories to be aware of the events that they relate to, we must add an `Event` collection property to `EventCategory`.

### `Models/EventCategory.cs`

```csharp
public List<Event> Events { get; set; }
```

{{% notice blue "Note" "rocket" %}}
The new property on `Event` is a single `EventCategory` reference, while the new property on `EventCategory` is a *collection* of `Event` objects. This is due to the one-to-many nature of the relationship. Each `Event` can have only one `EventCategory`, but an ``EventCategory`` may be related to multiple `Event` objects.
{{% /notice %}}

## Refactoring the Controller and View

Our `EventsController` requires a few updates now that `Event` objects reference `EventCategory` objects.

The `Index` method passes the collection of all `Event` objects into the view for display:

### `Controllers/EventsController.cs`

```csharp
public IActionResult Index()
   {
      List<Event> events = context.Events.ToList();
      return View(events);
   }
```

When we reference `context.Events`, all `Event` objects will be queried from the database. By default, EF uses **lazy loading** to retrieve objects. Lazy loading results in *only* the data in the `Event` table being returned in the result set. Any data stored in other tables, such as data belonging to a referenced object, will NOT be loaded. In our case, this means that `Event` objects in `context.Events` will NOT have their `Category` properties set by EF. As-is, our code would display an empty category column in the main view.

{{% notice blue "Note" "rocket" %}}
While lazy loading is not what we want now, it can be a useful strategy in a lot of cases. Suppose your application wants to display a list of all users, where each `User` has a `UserDetails` property that stores info like profile image, email, etc. 

If all we need is a list of users, loading all of the additional data in `UserProfile` is unnecessary and will slow down the application. Lazy loading minimizes the data returned to optimize performance and reduce queries. 
{{% /notice %}}

The solution is to use **eager loading**. Eager loading is a technique that allows us to specify that data from other tables/objects be loaded when the querying a specific table/object. In our case, we want our `Event` objects to be returned with their corresponding `EventCategory` objects. We can tell EF to load the categories eagerly with the following code:

### `Controllers/EventsController.cs`

```csharp
public IActionResult Index()
   {
      List<Event> events = context.Events.Include(e => e.Category).ToList();

      return View(events);
   }
```

The `Include` method takes a lambda expression which specifies the property of each `Event` object that should be included in the query results. The effect of this additional method is that a `JOIN` query is performed between the `Event` and `EventCategory` tables, with `Event.CategoryId` being joined on `EventCategory.Id`.

Our next update is more straightforward. Recall that we modified the main controller in `AddEventViewModel` to take a list of all `EventCategory` objects. This constructor is called in the `Add` method of our controller. Let's update it to pass in a list of all `EventCategory` objects, as queried from the database.

### `Controllers/EventsController.cs`

```csharp
public IActionResult Add()
{
   List<EventCategory> categories = context.Categories.ToList();
   AddEventViewModel addEventViewModel = new AddEventViewModel(categories);

   return View(addEventViewModel);
}
```

## Database Migration and Testing

We are done updating our code for now, but before we can test we must update the database. Recall that we changed the structure of the model by relating `Event` and `EventCategory` classes, and by removing `EventType`. Any model change requires a database update.

Open a terminal and navigate to the `CodingEvents` project directory within the solution. Then run `dotnet ef migrations add RelateEventsAndCategories` to create a new migration.

To apply the migration, run `dotnet ef database update`.

If you look at the database, you'll see that the `Event` table no longer has a `Type` column. In addition, it now has a `CategoryId` column that is a foreign key to `EventCategory.Id`.

Now, start up the app and test!

## Check Your Understanding

{{% notice green "Question" "rocket" %}}
You are working on an ASP.NET application tracking elected officials. Your model class, ``Senator`` has a many-to-one relationship with another model class, ``State``. To properly configure this relationship in the EF context, what must be present?

1. In `Senator`, a `State` property and a `StateId` property
1. In `Senator`, only a `State` property
1. In `State`, a `Senator` property and a `SenatorId` property
1. In `State`, only a `Senator` property
{{% /notice %}}

{{% notice green "Question" "rocket" %}}
What is the default technique for loading child objects of persistent objects? 

1. Eager loading
1. Lazy loading
1. Explicit loading
1. There is no default, the technique must always be explicitly specified
{{% /notice %}}
