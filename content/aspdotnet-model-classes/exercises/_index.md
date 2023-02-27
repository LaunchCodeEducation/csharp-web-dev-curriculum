---
title: "Exercises: Edit Model Classes"
date: 2023-02-20T17:39:54-06:00
draft: false
weight: 2
originalAuthor: Sally Steuterman # to be set by page creator
originalAuthorGitHub: gildedgardenia # to be set by page creator
reviewer: # to be set by the page reviewer
reviewerGitHub: # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

Add functionality to edit event objects in your `CodingEvents` application. 
These exercises assume that you have added all of the code from this section of the book and your 
application resembles the [models branch](https://github.com/LaunchCodeEducation/CodingEvents/tree/models).

The edit form will resemble the form used to create an event.

{{% notice green "Tip" "rocket" %}} 

   As you work through these steps, test your code along the way! 
   With each change you apply to your code, ask yourself what you expect to see when the application
   is run. You may not find that all of the steps result in observable changes, though.
   Use Visual Studio’s debugging tools and read your error messages if you run into issues after applying any of
   the changes.

{{% /notice %}}

1. Create the two action methods listed below in `EventsController`. We’ll add code
   to these in a moment, so just put the outline in place for
   now.

   1. Create an action method to display an edit form with this signature:

      ```csharp {linenos = table}
         public IActionResult Edit(int eventId) {
            // controller code will go here
         }
      ```

   1. Create an action method to process the form with this signature:

      ```csharp {linenos = table}
         [HttpPost]
         public IActionResult SubmitEditEventForm(int eventId, string name, string description) {
            // controller code will go here
         }
      ```

1. Add the necessary annotations to the `SubmitEditEventForm()` method for it to live at the path `/Events/Edit`.

   {{% expand "Check your solution" %}}

   ```csharp {linenos=table}
   [HttpPost]
   [Route("Events/Edit")]
   public IActionResult SubmitEditEventForm(int eventId, string name, string description)
   {
      // controller code will go here
   }
   ```

   {{% /expand %}}

1. You’ll need to configure the route for `Edit()` to include the path variable `eventId`, 
   so that paths like `/Events/Edit/3` will work.

   {{% expand "Check your solution" %}}

   ```csharp {linenos=table}
   [HttpPost]
   [Route("Events/Edit/{eventId}")]
   public IActionResult Edit(int eventId)
   {
      // controller code will go here
   }
   ```

   {{% /expand %}}

1. Create an `Edit.cshtml` view in `Views/Events`.

1. Copy the code from `Add.cshtml` into `Edit.cshtml`. 

   1. You'll want to update the text of the submit button and the heading to reflect the edit functionality.

   {{% expand "Check your solution" %}}

   ```html {linenos = table}
   <h1>Edit Event</h1>

   <form method="post">
      <div class="form-group">
         <label for="name">Name</label>
         <input name="name" type="text" />
      </div>
      <div class="form-group">
         <label for="description">Description</label>
         <input name="description" />
      </div>
      <input type="submit" value="Edit Event" />
   </form>
   ```

   {{% /expand %}}

1. Back in `EventsController`, round out the `Edit()` method.

   1. Use an `EventData` method to find the event object with the given `eventId`.
   
   1. Put the event object in `ViewBag`.

   1. Return the appropriate view.

   {{% expand "Check your solution" %}}

   ```csharp {linenos = table}
   [HttpGet]
   [Route("Events/Edit/{eventId}")]
   public IActionResult Edit(int eventId)
   {
      Event editingEvent = EventData.GetById(eventId);
      ViewBag.eventToEdit = editingEvent;
      return View();
   }
   ```

   {{% /expand %}}

1. Within the form fields in `Edit.cshtml`, 

   1. Get the name and description from the event that was passed in via `ViewBag` and
      set them as the values of the form fields.
   
   1. Add `action="/events/edit"` to the `form` tag.

   {{% expand "Check your solution" %}}

   ```html {linenos = table}
   <h1>@ViewBag.title</h1>

   <form method="post" action="/events/edit">
      <div class="form-group">
         <label for="name">Name</label>
         <input name="name" type="text" value="@ViewBag.eventToEdit.Name"/>
      </div>
      <div class="form-group">
         <label for="description">Description</label>
         <input name="description" type="text" value="@ViewBag.eventToEdit.Description" />
      </div>
      <input type="submit" value="Edit Event" />

   </form>
   ```

   {{% /expand %}}

1. Add another input to hold the id of the event being edited. This
   should be hidden from the user:

   ```html
      <input type="hidden" value="@ViewBag.eventToEdit.Id" name="eventId" />
   ```

   {{% notice blue "Note" "rocket" %}}

   You may not have named your `ViewBag` property `eventToEdit`.
   Make sure you are using the name you gave your property!

   {{% /notice %}}

   {{% expand "Check your solution" %}}

   ```html {linenos = table}
   <!-- description div code here -->
      </div>
      <input type="hidden" value="@ViewBag.eventToEdit.Id" name="eventId">
      <input type="submit" value="Edit Event" />
   </form>
   ```

   {{% /expand %}}

1. Back in the `Edit()` action method, add a title to `ViewBag` that reads `“Edit Event
   NAME (id=ID)"` where `"NAME"` and `"ID"` are replaced by the values for the
   given event. 

   {{% expand "Check your solution" %}}

   ```csharp {linenos = table}
   [HttpGet]
   [Route("Events/Edit/{eventId}")]
   public IActionResult Edit(int eventId)
   {
      Event editingEvent = EventData.GetById(eventId);
      ViewBag.eventToEdit = editingEvent;
      ViewBag.title = "Edit Event " + editingEvent.Name + "(id = " + editingEvent.Id + ")";
      return View();
   }
   ```

   {{% /expand %}}

1. In `SubmitEditEventForm()`, 

   1. Query `EventData` for the event being edited with the given id parameter. 
   
   1. Update the name and description of the event.

   1. Redirect the user to `/Events` (the event listing page).

   {{% expand "Check your solution" %}}

   ```csharp {linenos = table}
   [HttpPost]
   [Route("Events/Edit")]
   public IActionResult SubmitEditEventForm(int eventId, string name, string description)
   {
      Event editingEvent = EventData.GetById(eventId);
      editingEvent.Name = name;
      editingEvent.Description = description;
      return Redirect("/Events");
   }
   ```

   {{% /expand %}}

1. To access event editing, the user will need an edit option in the list of event data.

   1. In `Index.cshtml`, add a link to edit the 
      event as a column in the event table:

      ```html
         <td><a asp-controller="Events" asp-action="Edit" asp-route-id="@evt.Id">Edit Event</a></td>
      ```

      `asp-route-id` is a new tag helper for us.
      Our routes normally go `/<controller>/<action>`.
      `asp-route-id` passes an `{id?}` parameter at the end of our route.
      When the site is built, we can inspect it and see that for the first item in the table this line of HTML will look like:

      ```html
         <td><a href="/Events/Edit/1">Edit Event</a></td>
      ```

   {{% expand "Check your solution" %}}

   ```html {linenos = table}
    @foreach (var evt in ViewBag.events)
      {
         <tr>
            <td>@evt.Id</td>
            <td>@evt.Name</td>
            <td>@evt.Description</td>
            <td><a asp-controller="Events" asp-action="Edit" asp-route-id="@evt.Id">Edit Event</a></td>
         </tr>
      }
   </table>
   ```

   {{% /expand %}}
