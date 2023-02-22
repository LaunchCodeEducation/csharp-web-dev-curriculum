---
title: "Creating a Template"
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

Using templates is a useful way to reduce the effort required to create and maintain a web-based project. Before you can dive into using templates, however, you need to take care of a little groundwork first.

## Razor

**Razor** is a templating syntax included in the application framework for our MVC project. It allows us to write C# code directly into an HTML tree.

More information on Razor can be found in this [reference page](https://learn.microsoft.com/en-us/aspnet/core/mvc/views/razor?view=aspnetcore-6.0).

For the most part, Razor templates look and operate just like regular HTML code. Any C# logic we add to a template is preceded with the _at sign_, `@`. You can open any template in a browser and view it just like a static HTML file. Before we begin adding C# logic to Razor templates, we’ll first demonstrate creating a view using only HTML.

In this chapter, you will construct some small practice projects to help you learn how to implement Razor templates.

## Hello Views

Before you start coding, we need to refactor `HelloController`. Now `Index()` is responding to `GET` requests at `localhost:5001/hello` and `Welcome()` is only responding to `POST` requests at `localhost:5001/hello`. Check out the code block below to refactor your code.

Open up your `HelloASPDotNET` project in Visual Studio and make sure you have committed any recent changes. Make a new branch for creating views and code along with the reading.

```csharp{linenos=table,hl_lines=[2, 7,8,9],linenostart=13}

[HttpGet]
public IActionResult Index()

//...code continues

[HttpPost]
[Route("/hello")]
public IActionResult Welcome(string name)

//...code continues
```

### Controllers Return View Templates

So far, you’ve seen action methods in controller classes return `Content` objects to render some view. Now, we pivot to another option. We mention in the introduction to controller classes that action methods can return HTML templates. Indeed, the `HomeController` contains a few methods that do just that.

Out of the box, your MVC project contains several Razor templates within the `Views` directory. The sub-directory `Home`, found inside of `Views`, contains the Razor templates returned from the `HomeController` action methods. Just as an action method’s name will map to a route with the same name, an action method’s name can also correspond to a Razor template’s name. The `Index()` method inside of `HomeController` returns the `Index.cshtml` template found inside of `Views/Home`.

In order to return that template, the action method calls a **View() method**. The `View()` method finds a template that’s associated with the particular controller and action method that it is called from.

You can override the default behavior of the `View()` method, you can pass in a parameter which is the name of the template you want to render. For example, if we want an action method named `Form()` to return a Razor template named `WelcomeForm.cshtml`, we have `Form()` return `View("WelcomeForm");`.


### Add a Template

To create a template, we update `HelloController.Index()` to return a Razor template instead of a string of HTML. 

Start by creating a new subdirectory within the `Views` directory called `Hello`.

Within `Hello` create a new file of the _Razor View_ file template.

1. Right click on the `Views` directory or any subdirectory and select _Add_ -> _New File_ or _New Item_ depending on your OS.
1. Look in the _ASP.NET Core_ menu for the _Razor View_ or _Razor View - Empty_ option.
1. Once you have your _Razor View_ or _Razor View - Empty_ selected, name it `Index`.  We are going to name the `Views` after their corresponding action methods for the MVC projects in this course.

Add the HTML form from the `Index()` method to your new template. Make sure to remove any residual C# syntax, like `+` or `"` or `;`.  The form should only be in HTML.

```csharp{linenos=table,hl_lines=[],linenostart=6}
//inside the Views/Hello/Index.cshtml

<form method='post' action='/hello'>
    <input type='text' name='name' />
    <input type='submit' value='Greet Me!' />
</form>

```

Once you are done with that, update the `Index()` method to return `View()`. 

```csharp{linenos=table,hl_lines=[],linenostart=11}

   [HttpGet]
   public IActionResult Index()
   {
      return View();
   }
```


### `_Layout.cshtml`

When you re-render the app now, you’ll notice some additional features and different styling. There is a `_Layout.cshtml` file inside of the `Views/Shared` folder that provides some scaffolding for the application views. You can edit this file once and any other template will also render whatever elements you add to it. This can help give your application a polished, unified look and feel. If you do not want to use this file, adding `@{Layout = null;}` at the top of the template will cause this shared layout template to be ignored.

{{% notice blue "Try it!" "rocket" %}}

Try adding the following code to your `Hello/Index` View.  Run your project and see if anything looks different. 

```csharp{linenos=table,hl_lines=[],linenostart=3}
//inside the Views/Hello/Index.cshtml
@{
   Layout = null;
}

```

You can remove this after you see what it does.  If you leave this, your `Hello/Index` View may be different than the video walkthrough, but only in appearance.

{{% /notice %}}


## Check Your Understanding

{{% notice green  "Question" "rocket" %}} 

Which symbol is required to use C# code in a Razor template?

   1. `#`
   1. `@`
   1. `$`
   1. `!` 

<!-- ans: @    -->
{{% /notice %}}


{{% notice green  "Question" "rocket" %}} 
What is the file type for Razor templates?

1. `.razor`
1. `.rzr`
1. `.html`
1. `.cshtml`

<!-- ans: '.cshtml' -->
{{% /notice %}}
