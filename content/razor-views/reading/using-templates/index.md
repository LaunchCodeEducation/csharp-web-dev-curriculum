---
title: "Using a Template"
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

Now that we know a little bit about views, we can start talking about how to pass data between MVC elements. Models are a key component of this, but for now, we will focus on how to pass data between the view and the controller.

## Passing Data to a Template
The controller class contains methods that send data to different templates. These methods have a structure similar to:

{{% notice blue "Example" "rocket" %}}
```csharp{linenos=table,hl_lines=[5],linenostart=1}
  public IActionResult ActionMethod()
  {
     // method code here

     ViewBag.property = Data;
     return View();
  }
```
{{% /notice %}}

**ViewBag** is an object that passes data into a template. `Data` can be a variable of any type, a number, a collection of some sort, or an object. A `ViewBag` property is created and given a value as simply as is done on line 5 above. In fact, we can just as easily create a second property on `ViewBag` as follows:

{{% notice blue "Example" "rocket" %}}
```csharp
ViewBag.anotherNewProperty = someOtherData;
```
{{% /notice %}}

You can think of `ViewBag` as like an empty container object who exists for the purpose of carrying variables from the controller into the view.

### Accessing Data in a Template
The data assigned to properties on `ViewBag` is available inside of Razor templates. It can be accessed with the syntax `@ViewBag.propertyName`.

{{% notice blue "Example" "rocket" %}}

For example, if the controller stores a vegetable name as string in `ViewBag.vegetable`, then the template can display that value like so:


```csharp
<p>@ViewBag.vegetable</p>
```


Let’s say that `@ViewBag.vegetable` stores the string “Rutabaga”. When the program runs, the application interprets `<p>@ViewBag.vegetable</p>` as:


```csharp
<p>Rutabaga</p>
```


By using `@ViewBag.vegetable`, we make our webpage dynamically display data within the `p` element. Changing the value of `vegetable` leads to a corresponding change in the text in the view after refreshing.
{{% /notice %}}

## Try It Out in `HelloASPDotNET`

We started refactoring the `Welcome` method in the [previous section]({{<relref "../creating-templates/index.md">}}), but we did not update the return statement.  Currently, `Welcome` is still returning `Content`. 

Update the `Welcome` method by doing the following:

1. Change the return statement of `Welcome` to return a `View` instead of `Content`.
1. Create a `ViewBag` variable to store the `name` value.  
  {{% notice blue "Check your code" "rocket" %}}
  ```csharp{linenos=table,linenostart=19}
  public IActionResult Welcome(string name)
  {
    ViewBag.person = name;
    return View();
  }
  ```
  {{% /notice %}}

1. Make sure to add HTML to the `Welcome` View that will greet a user with the name they provided. 
  {{% notice blue "Check your code" "rocket" %}}
  ```csharp{linenos=table,linenostart=8}
  <h1>Welcome, @ViewBag.person!</h1>
  ```  
  {{% /notice %}}

    Your `Welcome` method will now pass the value of `ViewBag` to the view.

1. Run `HelloASPDotNET` to see your new views.








## Check Your Understanding

{{% notice green  "Question" "rocket" %}} 
Given the code:

```csharp
<p>Name: @ViewBag.name</p>
```

What will be displayed on the screen if the controller sends in a name variable with a value of “Blake”?

1. Name: name
1. Blake
1. Blake: Blake
1. Name: Blake
 
<!-- ans: Name: Blake -->
{{% /notice %}}

{{% notice green  "Question" "rocket" %}} 

We want a list element to read, “Item name: ______, Price: ______”, where the blanks need to be filled in with `name` and `price` values sent from the controller.

Which of the following will produce the desired result?

1. `<li>Item name: @ViewBag.name, Price: @ViewBag.price</li>`
1. `<li>@ViewBag("Item name: name, Price: price")</li>`
1. `<li>@Item name: , @Price = </li>`
1. `<li>Item name: @name, Price = @price</li>`

<!-- ans: ``<li>Item name: @ViewBag.name, Price: @ViewBag.price</li>`` -->
{{% /notice %}}

