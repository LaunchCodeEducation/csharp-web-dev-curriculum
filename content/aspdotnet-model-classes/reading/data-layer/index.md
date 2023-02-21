---
title: "Models and Data"
date: 2023-02-20T17:39:54-06:00
draft: false
weight: 3
originalAuthor: Sally Steuterman # to be set by page creator
originalAuthorGitHub: gildedgardenia # to be set by page creator
reviewer: # to be set by the page reviewer
reviewerGitHub: # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

To effectively work with data, we need to add another element to our MVC application. Say for example,
we want to remove an event from our list. If two events both have the same name, we can't yet identify which
of the events to delete. 

In `CodingEvents`, we add a unique identifier field to `Events` to better handle and track distinct 
`Event` instances. Next, we'll also create another model class called `EventData`. This allows us 
to encapsulate data storage and prepare ourselves for decoupling the `Event` model from the controller.

## Add a Unique Id

Identifying data by a user-defined string called `name` is not a sustainable or scalable method
of handling data in most situations. Consider the address book example. How can
we distinguish between two contact entries with the same name field? It is a frequent
practice to add a **unique identifier** field (sometimes called, or even labelled, **uid**) to a class 
responsible for modelling data. This ensures that our address book can contain two separate entries for 
our contacts who have the same name as one another. 

To accomplish the same data clarity with events, we'll add a few things to the event model class:

1. A readonly `id` field.
1. A static counter variable, `nextId`.
1. Additional constructor code that:
   
   1. Sets `id` to the `nextId` value.
   1. Increments `nextId`.

The result in `Models/Event.cs`:

```csharp {linenos = table}
   namespace CodingEvents.Models
   {
      public class Event
      {
         public string Name { get; set; }
         public string Description { get; set; }

         public int Id { get; }
         static private int nextId = 1;

         public Event(string name, string description)
         {
            Name = name;
            Description = description;
            Id = nextId;
            nextId++;
         }

         public override string ToString()
         {
            return Name;
         }
      }
   }
```

{{% notice blue "Note" "rocket" %}}

   Here's a closer look at what's going on in line 8.

   `Id` is created as a **get-only auto-implemented property**. You've seen this 
   syntax a few times before. The backing field, `id` is readonly because no setter 
   method has been written for the field. The only place `id`'s value 
   may be assigned is in a constructor (as it is on line 15).

{{% /notice %}}

With these additions, every time a new event object is created it is assigned a unique integer to its `id` field.

## Create a Data Layer

Now that we've begun building a model, it's a good time to remind ourselves that models are not designed to be 
data storage containers. Rather, models are meant to shape the data stored in another location. They shape data into 
objects that fit into the logic of our applications. As we work our way into learning about database usage and service 
calls, however, we'll use a C# class to store some data temporarily.

A **data layer** adds abstraction between models and the data we want to store. As we'll see, a data layer allows us to pass on responsibility of exactly *how* our data is stored.

To get started with a data layer, create a new directory called `Data` at the root of your project, on the same level as the rest of the MVC components. 
Inside of `Data/`, add a class `EventData`. Whereas `Event` is responsible for organizing
user-inputted information into a C# object, `EventData` is responsible for maintaining those objects once they 
are created. `EventData` is itself a C# class that stores events. It contains several methods for managing and 
maintaining the event data that simply extend System-provided collection methods.

The contents of `Data/EventData.cs`:

```csharp {linenos = table, linenostart = 6}
   namespace CodingEventsDemo.Data
   {
      public class EventData
      {
         static private Dictionary<int, Event> Events = new Dictionary<int, Event>();

         // GetAll
         public static IEnumerable<Event> GetAll()
         {
            return Events.Values;
         }

         // Add
         public static void Add(Event newEvent)
         {
            Events.Add(newEvent.Id, newEvent);
         }

         // Remove
         public static void Remove(int id)
         {
            Events.Remove(id);
         }

         // GetById
         public static Event GetById(int id)
         {
            return Events[id];
         }
      }
   }
```

With `EventData` now managing a collection of events, we must once again refactor `EventsController` to update the items stored in 
the dictionary. In keeping with the objective to remove data handling from the controller, we'll remove the list 
of events at the top of the class. Consequently, for the `Index()` action method, we'll now use events from 
`EventData` to populate a `ViewBag.events` property:

```csharp {linenos = table, linenostart = 17}
   ViewBag.events = EventData.GetAll();
```

And back to `NewEvent`, we'll make use of the `.add()` method from `EventData`:

```csharp {linenos = table, linenostart = 33}
   EventData.Add(new Event(name, desc));
```

## Delete an Event

Now that we've refined our events storage method, we are able to tackle the task of deleting an object. 
To delete an event object from storage, we'll grab the event's id and use that
information to call the `Remove()` method of `EventData`.
Since the delete event is user-initiated, a controller will be involved to pass
the information from the user-accessible view to the data layer. So our first step
with this task is to create an action method to return a view designed to delete events.

Onto the end of `EventsController`, add the following method:

```csharp {linenos = table, linenostart = 39}
   public IActionResult Delete()
   {
      ViewBag.events = EventData.GetAll();

      return View();
   }
```

We'll now need to create a new view for the path mapped in the method above. Add a new template, 
`Views/Events/Delete.cshtml`. This view will reference event id fields in order to distinguish which items the user 
will request to delete via checkbox inputs. 

```html {linenos = table}
   <h1>Delete Event</h1>

   <form method="post">
      @foreach (var evt in ViewBag.events)
      {
         <div class="form-group">
               <label>
                  <span>@evt.Name</span>
                  <input type="checkbox" name="eventIds" value="@evt.Id" class="form-control">
               </label>
         </div>
      }

      <input type="submit" value="Delete Selected Events" class="btn btn-danger">

   </form>
```

We also need a `POST` handler to take care of what to do when the delete event information
is submitted by the user. We'll have this post handler redirect the user back to the events home 
page once they have selected which event, or events, to remove from storage.

In `EventsController`, add another controller method:

```csharp {linenos = table, linenostart = 47}
   [HttpPost]
   public IActionResult Delete(int[] eventIds)
   {
      foreach (int eventId in eventIds)
      {
            EventData.Remove(eventId);
      }

      return Redirect("/Events");
   }
```

## Check Your Understanding

{{% notice green "Question" "rocket" %}}

   In `CodingEvents`, which method can we call to list every event object?

   1. `Events.Get()` 
   1. `EventData.GetEvery()` 
   1. `Event.GetAll()` 
   1. `EventData.GetAll()` 

{{% /notice %}}

<!-- d, EventData.GetAll() -->

{{% notice green "Question" "rocket" %}}

   In `CodingEvents`, breaking up the event storage from the `Event` model is an example of which 
   object-oriented concept?

   1. Inheritance
   1. Polymorphism
   1. Encapsulation 
   1. MVC design

{{% /notice %}}

<!-- c, encapsulation -->