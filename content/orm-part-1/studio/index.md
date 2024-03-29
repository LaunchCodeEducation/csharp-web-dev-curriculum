---
title: "Studio: OMG more ORM!"
date: 2023-03-10T09:32:46-06:00
draft: false
weight: 3
originalAuthor: Courtney Frey # to be set by page creator
originalAuthorGitHub: speudusa # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: Kimberly Horan # update any time edits are made after review
lastEditorGitHub: codinglikeagirl42 # update any time edits are made after review
lastMod: 2023-04-06 # UPDATE ANY TIME CHANGES ARE MADE
---

Today’s studio depends on completion of the [exercises]({{< relref "../exercises/_index.md" >}}). If you have not completed the exercises, go back and complete them before continuing with the studio. If you want to check out one possible solution to the exercises before you get started, look at the [orm1-studio](https://github.com/LaunchCodeEducation/CodingEvents/tree/orm1-studio) branch in `CodingEvents`.

## Adding a ViewModel

With the new table set up in our database and our application displaying event categories, we need to add a ViewModel so we can add validation for new event categories. Create a new ViewModel called `AddEventCategoryViewModel`. Add one property to your ViewModel for the name of the event category. Add validation attributes to the property so that it is required and that it has to be between 3 and 20 characters long.

## Updating `EventCategoryController`

We will be creating 2 new action methods in our controller:

1. `Create()`
1. `ProcessCreateEventCategoryForm()`

### `Create()` Action Method

`Create()` needs to do the following:

1. Responds to GET requests at `EventCategory/Create` and returns a view called `Create.cshtml`.
1. Pass a new instance of `AddEventCategoryViewModel` to `View()`.


### `ProcessCreateEventCategoryForm()` Action Method

`ProcessCreateEventCategoryForm()` needs to do the following:

1. Responds to POST requests at the route of your choosing.

1. Use error validation and `ModelState.IsValid` appropriately. If you want to review how to use `ModelState.IsValid`, check out the section on [error validation]({{< relref "../../../content/viewmodels/reading/controller-validation/index.md" >}}).

1. Create a new instance of `EventCategory` and add it to the database if the form input meets the validation conditions.

1. Either reload the form or add a new event category to the database and direct the user back to the `EventCategory/Index.cshtml` template.

## Razor Templates

To finish the studio, we need to make a new template, `EventCategory/Create.cshtml`, which will contain a form for adding new event categories.

We also need to add links to the pages for all of the events, all of the event categories, and the form to add a new event category to the navbar. To do so, open up `_Layout.cshtml` and scroll down to approximately line 22 where you find the code for the link to add an event:

```html{linenos=table,hl_lines=[],linenostart=22}
 <ul class="navbar-nav flex-grow-1">
   <a class="nav-link text-dark" asp-area="" asp-controller="Events" asp-action="Add">Add</a>
</ul>
```
Using this code as a template, add links to the following views:
1. `Events/Index.cshtml`
1. `EventCategory/Create.cshtml`
1. `EventCategory/Index.cshtml` 

Make sure to apply useful names for the links.

## The Final Application

Once you are done, launch your app and head to the `/EventCategory` route! If you added categories already, you will see any categories already stored in the database.

If you click on “Create Category”, you should be directed to the /`EventCategory/Create` route. Once you hit submit, you are redirected back to `/EventCategory`, and your table now contains the newest event category!




