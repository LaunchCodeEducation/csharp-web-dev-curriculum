---
title: "Model Binding"
date: 2023-02-20T17:39:54-06:00
draft: false
weight: 4
originalAuthor: Sally Steuterman # to be set by page creator
originalAuthorGitHub: gildedgardenia # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

We now introduce a useful technique to auto-create model instances, 
called **model binding**. Model binding takes place when a whole 
model object is created by the ASP.NET framework on form submission. This saves us the effort, 
and the code, needed to pass in each form field to a controller. 

Model binding reduces the amount of code we need to 
write to create an object and helps with validation (which we’ll explore further in the next
section). With a few modifications to our project, ASP.NET creates an `Event` object for us when 
the *New Event* form is posted.

## How to Use Model Binding

When submitting new event information, rather than passing in each field used to 
instantiate a model, we can instead pass in `Event newEvent` as a parameter 
of the controller method. 

First, we need to add a parameterless constructor to `Event`:

```csharp {linenos=table}
   public Event()
   {
      Id = nextId;
      nextId++;
   }
```

Then, we can revise the `NewEvent()` method in `EventsController`:

```csharp {linenos = table, linenostart = 29}
   [HttpPost]
   [Route("Events/Add")]
   public IActionResult NewEvent(Event newEvent)
   {
      EventData.Add(newEvent);

      return Redirect("/Events");
   }
```

This is the essence of model binding. The model instance is created
on form submission. With only two fields needed to create an event, the value of this data binding may not be
particularly apparent right now. You can imagine, though, with a larger form and class, that the practice of 
model binding is pretty potent.

For binding to take place, we must use the model field names as the form field names. So back in 
the create form HTML, we update the form fields to match the event fields. 

`Views/Events/Add.cshtml`:

```html {linenos = table, linenostart = 4}
   <div class="form-group">
      <label>
         Name
         <input type="text" name="name" class="form-control">
      </label>
      <label>
         Description
         <input type="text" name="description" class="form-control">
      </label>
   </div>  
```

If a form field name does NOT match up with a model field, then binding will fail for that piece of data. 
It is critically important to ensure these names match up. 

{{% notice green "Tip" "rocket" %}}

   The basics of model binding require that model property names match form field names. If they don't, 
   you still have the option to bind the model with attributes. We could have left the description
   field in the *Add Event* form with `name="desc"`. Then back in the `Event` class, we could modify the 
   description property as such:

   ```csharp {linenos = table, linenostart = 10}
      [FromForm(Name="desc")]	
      public string Description { get; set; }
   ```

{{% /notice %}}

The changes above only scratch the surface of what can be done with model binding.
We address more aspects and advantages of this technique in the coming pages If you'd 
like to read more on the topic now, take a look at the [documentation](https://learn.microsoft.com/en-us/aspnet/core/mvc/models/model-binding?view=aspnetcore-6.0).

## Check Your Understanding

{{% notice green "Question" "rocket" %}}

   Complete this sentence (*Check all that apply*): Model binding ...

   1. requires the use of attributes.
   1. helps with form validation.
   1. reduces controller code.
   1. makes your code more rigid and vulnerable to errors.

{{% /notice %}}

<!-- b + c, helps with form validation, reduces controller code. -->

{{% notice green "Question" "rocket" %}}

   In `CodingEvents`, we add an additional property, `NumberOfAttendees`, to the `Event` class. What other change must we make to ensure the user of our 
   application can determine this value? (Assume we are using model binding to process form submission.) 

   1. Pass in a `numberOfAttendees` parameter to the form submission handler.
   1. Add another input element to the create event form with a `name="numberOfAttendees"` attribute.
   1. Add a `getAttendees` method to `EventData`.
   1. All of the above. 

{{% /notice %}}

<!-- b, Add another input element to the create event form with a ``name="numberOfAttendees"`` attribute. -->