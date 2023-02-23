---
title: "Razor Forms"
date: 2023-02-09T12:48:24-06:00
draft: false
weight: 7
originalAuthor: Courtney Frey # to be set by page creator
originalAuthorGitHub: speudusa # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

Already we have seen that templates allow us to build generic forms. Using templates, you can reuse the structure by rendering the same form, but with different labels and data. Thus, a single form can serve different purposes, saving you extra effort.

Whenever possible, reuse existing templates!

## Starting a New Project: Coding Events

You will build a new project so you can practice with templates and forms. If you have not done so, commit and push any unsaved work from your `HelloASPDotNET` project.

Your new project will keep track of some coding events, such as meetups and conferences. To get started, [follow the steps]({{<relref "../creating-templates/index.md">}}) you took to create `HelloASPDotNET`, but call the project `CodingEvents`.

### `CodingEvents` Setup

1. In the `Controllers` directory, create a new controller named `EventsController`.

1. In the new controller, create an `Index` action method for `GET` requests.

1. Within the action method, create an empty `List` and add a few event names to it.
   {{% notice blue "Example" "rocket" %}} 
   ```csharp{linenos=table,hl_lines=[],linenostart=13}

   [HttpGet]
   public IActionResult Index()
   {
      List<string> Events = new List<string>();
         //Add some events to the List

         //...code continues
   }
   ```
   {{% /notice %}}


1. Add the `List` to `ViewBag`. Then return the corresponding view.
   {{% notice blue "Example" "rocket" %}} 
   ```csharp{linenos=table,hl_lines=[],linenostart=13}

   [HttpGet]
   public IActionResult Index()
   {
      //...code continues
      ViewBag.events = Events;
      return View();
   }

   ```
  {{% /notice %}}

1. Within the `Views` directory, create a new directory named Events. Within this directory, create a new view named `Index.cshtml`.

1. Within the new template, loop over the `List` and display the name of each event. 
   {{% notice blue "Example" "rocket" %}} 
   ```csharp{linenos=table,hl_lines=[],linenostart=8}
   <ul>
      @foreach (string e in ViewBag.events)
      {
         <li>@e</li>
      }
   </ul>
   ```
   {{% /notice %}}

## Create and Render a Form
A Razor form can be made simply with a template that includes a `<form>` element. The method for the form should be of type `post`.

```html{linenos=table}
<!-- Other HTML -->

<form method="post">
   <input type="text" name="inputName">
   <input type="submit" value="submitButtonText">
</form>

<!-- Other HTML -->
```

You can include as many inputs as you need in the form, and these can be of different types (e.g. text, email, checkbox, etc.). However, each different piece of data you want to collect needs to have a unique `name` attribute.

To *render* the form in the view, add a method to the controller with an `[HttpGet]` annotation. 

   ```csharp{linenos=table,hl_lines=[],linenostart=1}}
  [HttpGet]
  public IActionResult Add()
  {
     // Any additional method code here

     return View();
  }

   ```

{{% notice blue "Note" "rocket" %}}

   If the `action` attribute in the `<form>` tag leads to the same route as the form is being rendered at, you do not have to include an `action` attribute.

{{% /notice %}}

### Create `Add` Method and View to `CodingEvents` 

1. Create a new View for the `EventsController` called `Add`.

1. Inside the `Add` view, create a form that takes one `input` of `type` text, and has a `name` of "name".  Create a second `input` of `type` "submit" and with a `value` "Add Event".
   {{% notice blue "Example" "rocket" %}} 
   ```csharp{linenos=table,hl_lines=[],linenostart=1}}
   <form method="post">
      <input name="name" type="text" />
      <input type="submit" value="Add Event" />
   </form>
   ```
   {{% /notice %}}

1. In the `EventsController`, create a new action method called `Add`.
   {{% notice blue "Example" "rocket" %}} 
   ```csharp{linenos=table,hl_lines=[],linenostart=1}
   [HttpGet]
   public IActionResult Add()
   {
      return View();
   }
   ```
   {{% /notice %}}

## Handling Form Submission

In this application, we are storing the name of events inside a list.  The `Add` view contains a form to capture events names, but the `Add` method only renders the form.  It does not process the data.

To _process_ a form after the user clicks the _Submit_ button, you need to add a method to the controller using the `[HttpPost]` annotation.  This method also needs a way to handle any data it captures.  

### The `NewEvent` Action Method
In `CodingEvents` let's create a new action method called `NewEvent` which will handle the data provided by a user.  In this app, we are asking a user to provide a name of an event related to coding.  After a user submits the form, the ideal outcome would be to see and updated list containing that new item.  We need to return something other than a `View` for this.  

We can `Redirect` the path back to the `/Events` view to see the new list item.  

We could start creating our `NewEvent` method like this:

   ```csharp{linenos=table,hl_lines=[3,6],linenostart=31}
   [HttpPost]
   [Route("/Events/Add")]
   public IActionResult NewEvent (string name)
   {
      // Method code ...
      return Redirect("/Events");
   }
   ```
1. Line 33: For each piece of data that needs to be retrieved from the form, declare a parameter of the appropriate type.

1. The method code performs any data manipulation required after the information gets submitted.

1. Line 36: We may want to send the user to a different page after they successfully submit a form. Instead of re-rendering the form, we want to use `Redirect()` to _redirect_ the user to a different template.

### Anchor Tags and Form Submission
Now that we have a form and can handle the form submission, we want to create a link to the form to add an event in our `Index` template. This way, after reviewing the list of events, users can click on the link to the form and add an event. To do this, we use [anchor tag helpers](https://learn.microsoft.com/en-us/aspnet/core/mvc/views/tag-helpers/built-in/anchor-tag-helper?view=aspnetcore-6.0). The basic format is as follows:

```html
<a asp-controller="ControllerName" asp-action="ViewName">Text Here</a>
```

Then when we build our application, the generated HTML of the page will look like:

```html
<a href="/ControllerName/ViewName">Text Here</a>
```

### Try it in `CodingEvents`
 
1. In your `EventsController` create an action method called `NewEvent` that redirects users to the `"/Events"`.  This method should be a post request, and use the following route: `"/Events/Add"`.
   {{% notice blue "Example" "rocket" %}} 
   ```csharp{linenos=table,hl_lines=[],linenostart=31}
  [HttpPost]
  public IActionResult NewEvent(string name)
  {
     // Any additional method code here

     return Redirect("/Events");
  }
   ```
   {{% /notice %}}


1. The `NewEvent` needs to add the any provided arguments to the `Events` list.
   {{% notice blue "Example" "rocket" %}} 
   ```csharp{linenos=table,hl_lines=[],linenostart=31}
  [HttpPost]
  public IActionResult NewEvent(string name)
  {
     Events.Add(name);

     return Redirect("/Events");
  }
   ```
   {{% /notice %}}

1. You may have an error with the `Events.Add(name);` in the `NewEvent` action method.  It cannot reach the `Events` List contained in the `Index` method.  Remove the list from the `Index` method.  Instead declare the `Events` list above the `Index` method.  Make sure that it has the correct access modifiers that provide access to elements shared within the `EventsController`.  
   {{% notice blue "Example" "rocket" %}} 
   ```csharp{linenos=table,hl_lines=[],linenostart=13}
   static private List<string> Events = new List<string>();
   ```
   {{% /notice %}}


1. How can users add a New Event to the list?  In the `Events/Index` view, add an anchor tag where the `asp-controller` is set to the `Events` controller and the `asp-action` is set to the `Add` action method.  Make sure a user knows this anchor tag's functionality.
   {{% notice blue "Example" "rocket" %}} 
   ```csharp{linenos=table,hl_lines=[],linenostart=4}
   @* Inside Events/Index View *@
   <p>
      <a asp-controller="Events" asp-action="Add">Add Event</a>
   </p>        
   ```
   {{% /notice %}}

1. If there are no events in our list, how could we encourage users to add one or more?  Add a conditional to the `Index` view that creates a message only if the `Events` list is empty.
   {{% notice blue "Example" "rocket" %}} 
   ```csharp{linenos=table,hl_lines=[],linenostart=13}
   @if(ViewBag.events.Count == 0)
   {
         <p>No events yet!</p>
   }      
   ```
   {{% /notice %}}

Users can now click on the link on our page at `localhost:5001/Events` and are directed to the form to add an event. Once they hit the button to submit the form, the data is passed to the `NewEvent()` method, the user’s event is added to the `Events` list, and the application redirects back to `localhost:5001/Events` where an updated `Events` list is displayed.

{{% notice blue Note "rocket" %}}
You can compare your code to the chapter's [walkthrough]({{<relref "../view-form-walkthrough/index.md">}}).
{{% /notice %}}