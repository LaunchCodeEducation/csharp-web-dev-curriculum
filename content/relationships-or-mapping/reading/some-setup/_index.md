---
title: "Some Setup"
date: 2023-03-16T09:16:07-06:00
draft: false
weight: 4
originalAuthor: John Woolbright # to be set by page creator
originalAuthorGitHub: jwoolbright23 # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod:  # UPDATE ANY TIME CHANGES ARE MADE
---

Before introducing many-to-many relationships in EntityFrameworkCore, we need to add a new model and view to our app.

{{% notice blue "Note" "rocket" %}}
The starter code for this chapter is located within the [orm-one-to-many branch](https://github.com/LaunchCodeEducation/CodingEvents/tree/orm-one-to-many).
<!-- The following walkthrough is a continuation of the [Creating a One-to-Many Relationship](https://education.launchcode.org/csharp-web-dev-curriculum/relationships-or-mapping/reading/one-to-many/) chapter. In addition to the steps in the previous chapter we also added a new persistent model class `Tag`. This will allow us to set up a `many-to-many` relationship between the `Event` and `Tag` class. If you have not completed the steps in the **Creating a One-to-Many Relationship** walkthrough you can either revisit and complete the steps or start this walkthrough using the following branch of code: [orm-one-to-many](https://github.com/LaunchCodeEducation/CodingEvents/tree/orm-one-to-many). -->
{{% /notice %}}

In this section, we explore how we can work with many-to-many relationships in ASP.NET using EntityFrameworkCore. To do so, we need a class that we can relate to `Event` in a many-to-many fashion. This is the `Tag` class.

## The `Tag` Model Class

Between the last section and this one, we have added a new persistent model class to the code, `Tag`. This class represents a tag of the type used for blog or social media posts. For us, a tag will be a topical label that can be applied to any event. Thus, we'll eventually relate `Event` and `Tag` to each other in a many-to-many way.
<!-- TODO: add correct ref link below -->
The steps to add this code follow the exact same process that we used to add a [persistent EventCategory class](orm1-exercises), so we won't go through them in detail here. 

## The `Detail` View

Before working with tags, we will add a new view, along with the corresponding controller, ViewModel, and template. The new view will live at the route `/Events/Detail/X`, where `X` is the ID of a specific event. This view will display the details of a specific event on its own page.

Adding a `Detail` view for events is relatively straightforward, but it also involves a couple of new concepts. We'll start by creating a ViewModel to model the data we want to display in the view.

```csharp {linenos=table}
using System;
using System.Collections.Generic;
using CodingEventsDemo.Models;

namespace CodingEventsDemo.ViewModels
{
   public class EventDetailViewModel
   {
      public string Name { get; set; }
      public string Description { get; set; }
      public string ContactEmail { get; set; }
      public string CategoryName { get; set; }

      public EventDetailViewModel(Event theEvent)
      {
            Name = theEvent.Name;
            Description = theEvent.Description;
            ContactEmail = theEvent.ContactEmail;
            CategoryName = theEvent.Category.Name;
      }
   }
}
```

The model replicates the `Name`, `Description`, and `Email` properties of `Event` while storing `Category.Name` as a string. This is a minor variant of the `Event` class, but by the end of this section we'll add more behavior to `EventDetailViewModel` that will make the benefits of using a ViewModel in this case more clear.

Within `EventsController` we add a handler method to display the view.

```csharp {linenos=table}
public IActionResult Detail(int id)
{
   Event theEvent = context.Events
      .Include(e => e.Category)
      .Single(e => e.Id == id);

   EventDetailViewModel viewModel = new EventDetailViewModel(theEvent);
   return View(viewModel);
}
```

There are two new concepts to introduce here. First, our method takes a parameter named `id`. You have worked with such parameters in the past, as query parameters mapped to method parameters. For example, we could reach this handler with the request path `/Events/Detail?id=X`. What's new now is that we will use the same parameter mapping, but with a **path parameter**. A path parameter is a parameter that is part of the request path. In this case, we will be able to make requests to a path like `Events/Detail/X`.

{{% notice blue "Note" "rocket" %}}
This parameter mapping works seamlessly because the of default path template specified in the `Program.cs` file. 

```csharp {linenos=table}
app.MapControllerRoute(
    name: "default",
    pattern: "{controller=Home}/{action=Index}/{id?}");
```

This template is `"{controller=Home}/{action=Index}/{id?}"`. The last portion, `{id?}`, means that any path parameter following the action method will map to a method parameter named `id`. 

If we wanted to use a different URL structure, or a different method parameter name, we would need to include additional configuration. See [the documentation on routing](https://docs.microsoft.com/en-us/aspnet/core/mvc/controllers/routing?view=aspnetcore-6.0) for more details.
{{% /notice %}}

The other new concept here is the use of the EF method `Single`: 

```csharp {linenos=table}
Event theEvent = context.Events
   .Include(e => e.Category)
   .Single(e => e.Id == id);
```

This method takes a boolean lambda expression and filters the `Context.Events` collection down to the *one* event that satisfies `e.Id == id`. In other words, it finds the single event with `Id` matching the path parameter.

{{% notice blue "Note" "rocket" %}}
We use `Single` instead of `Find` here because we also need to call `Include` to eagerly fetch the `Category` property. `Include` can not be chained with `Find`.
{{% /notice %}}

The only remaining task is to create the view for the new event details. It should consist of a table displaying the properties of the `Event`. Create a new file within the `/Views/Events` folder named `Detail.cshtml` and add the following code:

```html {linenos=table}
@model CodingEvents.ViewModels.EventDetailViewModel

<h1>@Model.Name</h1>

<table class="table">
    <tr>
        <th>Description</th>
        <td>@Model.Description</td>
    </tr>
    <tr>
        <th>Contact Email</th>
        <td>@Model.ContactEmail</td>
    </tr>
    <tr>
        <th>Category</th>
        <td>@Model.CategoryName</td>
    </tr>
</table>
```

That wraps up this section. In the next chapter we will create the `many-to-many` relationship between the `Event` and `Tag` class.