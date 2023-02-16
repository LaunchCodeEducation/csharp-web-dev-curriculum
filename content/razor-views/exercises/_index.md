---
title: "Exercises: Razor Views"
date: 2023-02-09T12:48:24-06:00
draft: false
weight: 2
originalAuthor: Courtney Frey # to be set by page creator
originalAuthorGitHub: speudusa # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

In this chapter, we started working on an application for tracking various coding events around town.

## Getting Started
Open up your `CodingEvents` project in Visual Studio. Create and checkout a new branch to complete these exercises.

<!-- TODO: Link to branch -->
The code you start with should roughly resemble [this branch](LINK). If you have been coding along with the video lessons, you’re probably in good shape.

As always, give the branch a useful name, like `view-exercises`.

Now, let’s add descriptions to our events.

## Expanding our Events Schedule

1. In this lessons, we learned how to use templates to display the elements in a static list called `Events`. Let’s convert our `Events` list to a `Dictionary`. The structure of a dictionary enables us to add descriptions to our events. You’ll need to think about what data types the event name and description will be.

   {{% notice green "Tip" "rocket" %}}

   If you need to refresh your memory on dictionaries, refer to [this page](Link to Chapter3).

   {{% /notice %}}

1. Update the Events/Add.cshtml template with a new field for a user to submit an event description.

   {{% notice green "Tip" "rocket" %}}

   You’ll want to also add some `label` tags to your form to let the user know what data they are entering.

   {{% /notice %}}

   {{% expand "Check your solution" %}}
   ```csharp
   <h1>Add Event</h1>

   <form method="post">
      <label for="name">Name</label>
      <input name="name" type="text" />
      <label for="desc">Description</label>
      <input name="desc" />
      <input type="submit" value="Add Event" />
   </form>
   ```
   {{% /expand %}}

1. Back in `EventsController.cs`, add the description parameter to the `NewEvent` action method and within the method, add the new event key/value pair to the `Events` dictionary.   

   {{% notice green "Tip" "rocket" %}}

   Whatever value you provided in the `name` attribute of your new description field is the name of the parameter.

   {{% /notice %}}

   {{% expand "Check your solution" %}}
   ```csharp
   [HttpPost]
   [Route("Events/Add")]
   public IActionResult NewEvent(string name, string desc)
   {
      Events.Add(name, desc);

      return Redirect("/Events");
   }
   ```
   {{% /expand %}}

1. Now to Events/Index.cshtml. Replace the `ul` with a `table` to display event names and descriptions.
   {{% expand "Check your solution" %}}
   ```csharp{linenos=table,hl_lines=[],linenostart=1}
   // inside the "else" block
   <table>
      <tr>
         <th>
            Name
         </th>
         <th>
            Description
         </th>
      </tr>
      @foreach (KeyValuePair<string, string> evt in ViewBag.events)
      {
         <tr>
            <td>@evt.Key</td>
            <td>@evt.Value</td>
         </tr>
      }
   </table>
   ```
   {{% /expand %}}   


1. Lastly, modify `_Layout.cshtml` to display links for the Coding Events app (only `Events/Index` and `Events/Add` for now).

   {{% expand "Check your solution" %}}
   ```csharp{linenos=table,hl_lines=[],linenostart=1}
   <header>
   <!-- html code -->
      <div class="navbar-collapse collapse d-sm-inline-flex flex-sm-row-reverse">
         <ul class="navbar-nav flex-grow-1">
            <li class="nav-item">
               <a class="nav-link text-dark" asp-area="" asp-controller="Events" asp-action="Add">Add</a>
            </li>
         </ul>
      </div>
   <!-- more html -->
   </header>
   ```
   {{% /expand %}}
