---
title: "ViewModels and Passing Data Between Views"
date: 2023-02-24T08:57:18-06:00
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

Now that we have an understanding for what a model is, we can focus on how to effectively pass information between the three elements of MVC applications. With our current MVC application, we can add new events and remove events. However, our application is also susceptible to run-time errors. Our view can accept any type of input and if we mistype something in our view, we can run into issues later down the line.

A `ViewModel` is a model class designed specifically to be used in a view. By utilizing ViewModels in our application, we can make our views strongly-typed and add validation to forms to prevent bad user input. Also, if we have information we want to collect as part of a form, but not save as part of a model, we can store that data as a property of a ViewModel. An example of this would be if we have a form for users to create an account on our site. The form includes two fields: one for the password and one for confirming the new user’s password. While we only want to save the password and may only have a `Password` property in our model, we can add a `ConfirmPassword` property to the `ViewModel` so we can check that the two match before saving the user’s info. These benefits of `ViewModels` will help reduce potential errors in our application.

## Refactoring the View and Controller to Use a Model in a View

To start with understanding why we may want to use a ViewModel, let’s refactor our code to use a model directly in our view.

First, in `EventsController`, we want to convert the collection of Events we have been holding into a list.

```csharp{linenos=table,hl_lines=[],linenostart=19}
List<Event> events = new List<Event>(EventData.GetAll());
```

Now that we are storing our items in a `List`, we need to import the model into our `Events/Index.cshtml` view so we can use the new events collection. We can add a small statement up on line 1 to do so:

```csharp{linenos=table,hl_lines=[],linenostart=1}
@model List<CodingEvents.Models.Event>
```
<!-- TODO: Need to consolidate or remove this.  Adjust "in the video" references -->
Or, as we write in the video: <-- FIX THIS

```csharp{linenos=table,hl_lines=[],linenostart=1}
   @using CodingEvents.Models

   @model List<Event>
```

Wherever we used our `ViewBag` property, we can now use `Model` syntax. Once the view has been updated, run the application!

This was merely a refactor so the functionality of the app hasn’t changed, but we have eliminated some of the possibility of bugs in our code being discovered at runtime! Using a model in a view like this makes our view _strongly-typed_. Before if we misspelled a property of `Event` or `ViewBag`, those errors would have been caught at run-time and possibly interfered with users’ experience. With a strongly-typed view, the same errors would be caught at compile-time before users see the application. Strongly-typed views also support intellisense, so as we work with properties of a model, we can make sure we have the correct property name.

## Adding a ViewModel

Now that we have refactored our `Events/Index.cshtml` view and `EventsController` to use a model, let’s investigate how to create a ViewModel. We can do so by following these steps:

1. Add a `ViewModels` directory at the top level of the project.

1. Add a new class to the `ViewModels` directory and name it `AddEventViewModel`.

1. Add `Name` and `Description` properties to the new class.


   {{% notice blue "Note" "rocket" %}} 
   For now, your ViewModel does not need a constructor!
   {{% /notice %}}

1. In the `Add()` action method responsible for retrieving the form to add events, in `EventsController`, create a new instance of `AddEventViewModel` called `addEventViewModel` and add it to the `View()`.

1. Import the ViewModel to the `Add.cshtml` view with the `@model` syntax.

1. Add `asp-controller = Events` and `asp-action = NewEvent` to the `<form>` tag to designate which method the form data should be sent to.

1. Add `asp-for` to `<label>` and `<input>` tags. This allows us to specify which form field corresponds to which property in our ViewModel.

1. Refactor the `NewEvent()` action method to be named `Add()`. Have it also now use the ViewModel as its parameter. Set values of a new `Event` object using the values of the properties stored in the instance of the `AddEventViewModel`.

1. Add the new `Event` object to `EventData` and make sure that the method still returns a `Redirect` to `/Events`.

1. Run your application.

Following these steps, we effectively refactored our application to use a ViewModel. While the functionality of the application remains the same, we are now in a position to easily add validation to our application.


## Check Your Understanding
{{% notice green  "Question" "rocket" %}} 
**True or False**: ViewModels are views designed to specifically be used in models.

<!-- ans: False, ViewModels are models designed to be used in views! -->
{{% /notice %}}
