---
title: "Cleaning Up Your Controllers"
date: 2023-02-06T14:09:15-06:00
draft: false
weight: 4
originalAuthor: Sally Steuterman # to be set by page creator
originalAuthorGitHub: gildedgardenia # to be set by page creator
reviewer: # to be set by the page reviewer
reviewerGitHub: # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

So far, we have been adding attributes to our methods as we go along for each specific use case.
However, now our controller is rather unorganized and full of commented out attributes.
We can use a couple tips and tricks from attribute routing to clean this controller up.


Once you have written several action methods within a class, you may notice some similar behavior.
You may also want to expand upon the behavior that different action methods can make use of.
So far, we have been adding multiple different `[Route("path")]` attributes to each method to get every method to respond to a path that starts with `localhost:5001/helloworld`.
We also want to use the `Welcome()` method to respond to `GET` requests and `POST` requests, not just one or the other.
Time to DRY our code!

## Class-Level Attributes

In addition to adding attributes above action methods, we can also add attributes for routing above the class.
When we do so, we are designating class-wide behavior.
In `HelloController`, we want every action method to respond to requests at paths that start with `localhost:5001/helloworld`.
We can use `[Route("path")]` once above the class to designate that every path for each action method needs to start with `/helloworld`.

```csharp {linenos = table}
   [Route("/helloworld")]
    public class HelloController : Controller
    {
        // action methods here
    }
```

Now that we have added that `[Route("/helloworld")]` above the class, we can start to modify the attributes we placed above the `Index()` method.

```csharp {linenos = table}
   [HttpGet]
   public IActionResult Index()
   {
      string html = "<form method='post' action='/helloworld/welcome'>" +
            "<input type='text' name='name' />" +
            "<input type='submit' value='Greet Me!' />" +
            "</form>";

      return Content(html, "text/html");
   }
```

Since we want to map `Index()` to the path `localhost:5001/helloworld`, we removed the `[Route("/helloworld")]` attribute above the method.
If we hadn't, we would have inadvertently mapped the `Index()` method to the path, `localhost:5001/helloworld/helloworld`.
We want to leave the `[HttpGet]` attribute above the `Index()` method so we can still specify that `Index()` responds to `GET` requests.

Now that just leaves us the `Welcome()` method!

## One Method, Two Request Types

When we modified the `Welcome()` method to respond to a `POST` request, we commented out the attributes that we added when we were working with route parameters.
With attributes, we can DRY our code and create one method that can respond to two different request types at two different routes.
Before we begin, we should note that we can add route info directly to `[HttpGet]` and `[HttpPost]`.

```csharp {linenos = table}
   [HttpPost("welcome")]
   public IActionResult Welcome(string name = "World")
   {
      return Content("<h1>Welcome to my app, " + name + "!</h1>", "text/html");
   }
```

On line 1, we modified the `[HttpPost]` attribute to include the end of our path.
Now `Welcome()` still responds to `POST` requests at `localhost:5001/helloworld/welcome`.
However, this is just the beginning of us DRYing our code.

We also want `Welcome()` to respond to `GET` requests.
We can modify an `[HttpGet]` attribute to do so.

```csharp {linenos = table}
   [HttpGet("welcome/{name?}")]
   [HttpPost("welcome")]
   public IActionResult Welcome(string name = "World")
   {
      return Content("<h1>Welcome to my app, " + name + "!</h1>", "text/html");
   }
```

We added a different path to the `[HttpGet]` attribute on line 1.
Now `Welcome()` can respond to `GET` requests at `localhost:5001/helloworld/welcome`, `localhost:5001/helloworld/welcome?name=Tillie`, and `localhost:5001/helloworld/welcome/Tille`.
`Welcome()` can also still respond to the `POST` request at `localhost:5001/helloworld/welcome` upon submission of the form.

Now when we run our code, our app will still have the same functionalities, but now we have a more refined and organized code base!

## Check Your Understanding

{{% notice green "Question" "rocket" %}}

   True/False: Routing attributes go below the class definition, but above the method signature.

{{% /notice %}}

<!-- False, attributes go above both the class definition and the method signature -->