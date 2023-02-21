---
title: "Create a Model Class"
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

In this book section, we will continue to make incremental changes to `CodingEvents`. The next set of 
changes show model creation, how models relate to data, and the practice of model binding. First, we 
replace the dictionary in `EventsController` with a list of `Event` models. We’ll then update our 
action methods to take advantage of the new model and its properties. Lastly, we refactor the view template 
to reflect the changes in the controller.

## Setting Up a Model Class

Like controllers, model classes are conventionally located in a `Models`
folder. Model classes resemble the kinds of classes we practiced making at 
the start of this course. In other words, models are **plain old C# objects**, or **POCOs**.

To create a model, we’ll transform the information that we once stored in an `Events` dictionary into a class.
This new `Event` class will include a property for `Name`, a constructor, and a `ToString()` override.

In `Models/Event.cs`:

```csharp {linenos=table} 

   namespace CodingEvents.Models
   {
      public class Event
      {
         public string Name { get; set; }

         public Event(string name)
         {
            Name = name;
         }

         public override string ToString()
         {
            return Name;
         }
      }
   }

```

We now need to update the `POST` handler that creates new events. 

First, replace the `Events` dictionary with a list of `Event` objects.

```csharp {linenos=table,linenostart=15}
   static private List<Event> Events = new List<Event>();
```

Update the `Add()` method inside of 
`NewEvent()` to add a new `Event` instance to the list:

```csharp {linenos=table,linenostart=30}
   [HttpPost]
   [Route("Events/Add")]
   public IActionResult NewEvent(string name)
   {
      Events.Add(new Event(name));

      return Redirect("/Events");
   }
```

Back in `Events/Index.cshtml`, update the HTML to use the `Event` object’s fields, rather than strings.

```csharp {linenos=table, linenostart=22}
   @foreach (var evt in ViewBag.events)
   {
      <tr>
         <td>@evt.Name</td>
      </tr>
   }
```

{{% notice green "Tip" "rocket" %}}

   Here's a shorthand to create auto-implementing properties. In a class, type the word “prop” followed 
   by hitting the Tab key twice. This swiftly supplies the property’s scaffolding:

   ```csharp
      public object MyProperty { get; set; }
   ```

{{% /notice %}}

## Add a Model Property

To round out the `Event` class, we'll add a `Description` property to showcase what our events are all about.

Updates to `Models/Event.cs`:

```csharp {linenos = table}
   namespace CodingEventsDemo.Models
   {
      public class Event
      {
         public string Name { get; set; }
         public string Description { get; set; }

         public Event(string name, string description)
         {
            Name = name;
            Description = description;
         }

         public override string ToString()
         {
            return Name;
         }
      }
   }
```

Now that our data is object-oriented, it’s quick and easy to add a new property affiliated with an event. 
If we decide to add properties, such as `Date` or `Location`, we can follow the pattern established. 
Think about when we stored events as key-value pairs. At that stage, more significant changes were necessary 
to add fields.

In the `Views` folder, the `Events/Add.cshtml` template still uses a `desc` field so we don't need to update
this view. We do, however, need to go into `Events/Index.cshtml` to add the table data for an event's description.

`Events/Index.cshtml`:

```csharp {linenos=table, linenostart=26}
   <td>@evt.Description</td>
```

Lastly, add a parameter to the `NewEvent` action method. This parameter passes the description value into 
the creation of the `Event` object.

`EventController`:

```csharp {linenos=table, linenostart=30}
   [HttpPost]
   [Route("Events/Add")]
   public IActionResult NewEvent(string name, string desc)
   {
      Events.Add(new Event(name, desc));

      return Redirect("/Events");
   }
```

## Check Your Understanding

{{% notice green "Question" "rocket" %}}

   True/False: Model code is framework independent.

{{% /notice %}}

<!-- True, models are just C# objects -->

{{% notice green "Question" "rocket" %}}

   Say we do add a `Date` property to the `Event` class. Which line would we add to `Events/Index.cshtml` 
   to also display that value in our table of events?

   1. `<li>@evt.Date</li>`
   1. `<td>evt.Date</td>`
   1. `<td>@event.Date</td>`
   1. `<td>@evt.date</td>`

{{% /notice %}}

<!-- a, `<td>@evt.Date</td>` -->