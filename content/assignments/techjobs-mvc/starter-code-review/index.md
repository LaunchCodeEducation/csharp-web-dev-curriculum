---
title: "Task 1: Review the Starter Code"
date: 2023-01-05T13:58:39-06:00
draft: false
weight: 1
originalAuthor: Sally Steuterman # to be set by page creator
originalAuthorGitHub: gildedgardenia # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

{{% notice green "Tip" "rocket" %}}

   One essential programming skill that you will develop is the ability to read
   and understand someone else's code. This assignment begins with you
   practicing exactly that. Make sure you carefully examine the provided code
   BEFORE you start changing things.

   Trying to "fix" a code sample before understanding how it works leads to
   confusion, frustration, and a broken program. DO NOT SKIP the code review!

{{% /notice %}}

Carly created a ASP.NET MVC application and filled in some features. She
refactored `JobData` to generate a List of `Job` objects based on
your TechJobs-OO work, and she added controllers and views for a "Home",
"List", and "Search" page. `JobData` now also builds Lists for the
`Employer`, `Location`, `PositionType`, and `CoreCompetency` objects.

## The Data and Model

The "model" is contained in the `JobData` class, which is in the `Data`
folder. We put "model" in quotes, since this class isn’t a model in the
typical, MVC/object-oriented sense (maybe a better name for this assignment
would be *TechJobs VC*).

The `JobData` class serves the same purpose as before---it reads data from
the `job_data.csv` file and stores it in a format we can use. In this case,
that format is a `List` of `Job` objects, which is stored in the `Models` folder. Note that Carly changed the
path to the `job_data.csv` file to store it in the `Data` folder too.

You’ll use some of the static methods provided by `JobData` in your
controller code. Since you’re already familiar with these, we’ll leave it to
you to review their functionality as you go.

## The Controllers

Expand the `Controllers` folder, and you’ll see that you have three
controllers already in place. Let’s look at these one at a time.

### The `HomeController`

This class has only one action method, `Index()`, which displays the home page
for the app. The controller renders the `Index.cshtml` template (in
`Views/Home`) and provides a fairly simple view.

{{< rawhtml >}}
   <img src="../pictures/techJobsMvcHome.png" alt="TechJobs MVC home screen" />
{{< /rawhtml >}}

### The `ListController`

This controller provides functionality for users to see either a table showing
all the options for the different `Job` fields (`Employer`, `Location`,
`CoreCompetency`, and `PositionType`) or a list of details for a selected
set of jobs.

If you look at the corresponding page at `/list`, you’ll see an "All" column
in the table. However, this option doesn’t work yet, and you will fully
implement the constructor as you work on this project.

At the top of `ListController` is a constructor that populates
`ColumnChoices` and `TableChoices` with values. These Dictionaries play the
same role as in the console app, which is to provide a centralized collection
of the different *List* and *Search* options presented throughout the user
interface.

`ListController` also has `Index()` and `Jobs()` action
methods. The first method
renders a view that displays a table of clickable links for the different job
categories. The second method needs to render a different view that displays
information for the jobs that relate to a selected category. Both of the
action methods can obtain data by implementing the `JobData` class methods.

`Jobs()` will work similarly to the search functionality, in
that we are "searching" for a particular value within a particular field and
then displaying jobs that match. However, this is slightly different from the
other way of searching in that the user will arrive at this handler method as a
result of clicking on a link within the `Index.cshtml` view, rather than via
submitting a form.

### The `SearchController`

Currently, the search controller contains only a single method, `Index`.
It simply renders the form defined in the `Index.cshtml` template.

Later in this assignment, you will receive instructions for adding a second
handler to deal with user input and display the search results.

## The Views

Let’s turn our attention to the views.

### Bootstrap Classes

The application uses a few Bootstrap classes to style the view content and job tables. You won’t have to explicitly add any Bootstrap classes to your views in this assignment, but it’s a great way to make your sites look good with minimal work.

### The List Views

Turn your attention to `List/Index.cshtml`. This page displays a table of links
broken down into several categories. Data from `ColumnChoices` is used to
fill in the header row, and information stored in `TableChoices` generates
the link text.

The most interesting part of this template is how we generate the links:

```html {linenos=true,hl_lines=[1,5,8],linenostart=17}
   @foreach (var category in ViewBag.tableChoices)
   {
      <td>
         <ul>
         @foreach (var item in category.Value)
         {
            <li>
                  <a asp-controller="List" asp-action="Jobs" asp-route-column="@category.Key" asp-route-value="@item">@item</a>
            </li>
         }
          </ul>
      </td>
   }
```

1. `TableChoices` is a Dictionary from `ListController`, and it contains the names of
   the `Job` fields as keys (`Employer`, etc.). The value for each key is
   a List of `Employer`, `Location`, `CoreCompetency`, or
   `PositionType` objects.
1. In line 17, `category` represents one key/value pair from
   `TableChoices`, and in line 21, `item` represents one entry from the
   stored `List`.
1. We’ve seen some of the syntax to generate a link within a Razor
   template, but we don't have as much experience with `asp-route-column` and `asp-route-value`.This syntax causes Razor
   to dynamically generate query parameters for our URL.

In line 24, we set these parameters by using `asp-route-column=` and `asp-route-value=`. The
values of these parameters are determined dynamically based on
`@category.key` and `@item`. Since these values come from
`TableChoices`, the *keys* will be `employer`, `location`, etc. The
*values* will be the individual elements from the related `List`. When the
user clicks on these links, they will be routed to the
`Jobs()` action method in `ListController`, which looks for
these parameters.

By the end of your work on this project, clicking on one of the links display a list of jobs that relate to the
choice, via the `Jobs()` action method.

For now, click one of the *Location* links. This sends a request as we
outlined above, but doing so only leads to an error.

Once you have completed the project, the page you will see at `/list/values?column=location&value=...` is generated by
the `Jobs.cshtml` template. It has a similar structure as `Index.cshtml`,
but the table consists of only one column.

{{% notice blue "Note" "rocket" %}}
   Select "Kansas City" from the list of locations, and then check the address
   bar of your browser:

   ```console
      /list/jobs?column=location&value=Kansas%20City
   ```

   Razor inserts `%20` for us, to represent a space, but this may
   actually be hidden in your browser’s address bar.
{{% /notice %}}

### The Search View

Finally, click on *Search* from the home page, or the navigation bar, and open
up `Search/Index.cshtml` in Visual Studio. You’ll see a search form (in both the browser
and template file) that gives the user the option of searching by a given
`Job` field, or across all fields. This is an exact visual analog of our
console application.

This template will be used to display search results, in addition to rendering
the form. This will give the nice user experience of easily searching multiple
times in a row.

## Wrap Up the Code Review

Once you understand the controllers and views that are already in place, you’re
ready to begin your work.

In Visual Studio, select *View > Tasks* to pop open a small pane at
the bottom of the window. This list is populated by any code comments that
start with `TODO`. You’ll see your tasks listed, and clicking on any one will
open the relevant file.

{{% notice blue "Note" "rocket" %}}
   You may not see a `TODO #4`. This is because TODO comments in views do not always show up in the Task List.
   If it is not there, check out the `Search/Index.cshtml` view to locate it!
{{% /notice %}}