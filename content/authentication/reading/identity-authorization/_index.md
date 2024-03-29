---
title: "Identity and Authorization"
date: 2022-12-15T09:16:07-06:00
draft: false
weight: 6
originalAuthor: John Woolbright # to be set by page creator
originalAuthorGitHub: jwoolbright23 # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: 12/15/22 # UPDATE ANY TIME CHANGES ARE MADE
---

While this chapter is focused on authentication, you may find yourself wanting to use Identity to limit pages to logged-in users Authorization allows us to restrict access to pages by allowing only logged in users to see them. While this can be a very complex process, `ASP.NET` has two simple attributes that allow us to restrict access to pages to only logged in users.

`[Authorize]` is an attribute that limits access to content to only logged in users.
`[Authorize]` can be used for a specific method or a whole controller.

`[AllowAnonymous]` is an attribute that allows *any* viewer to access content.
This is the default state, so `[AllowAnonymous]` is oftentimes used in conjunction with `[Authorize]`.

In `CodingEvents`, we may only want to allow logged-in users to add an event. We can add `[Authorize]` at the controller level to prevent any anonymous users from accessing those pages.

```csharp {linenos=table}
[Authorize]
public class EventsController : Controller
{
    // Controller code here!
}
```

Why do this? Because giving all users the ability to add, edit, or delete events can cause trouble.

However, we do want to give all users the ability to view the events. That is where `[AllowAnonymous]` comes in. We can update the controller so that the `Index` view is accessible to everyone like so:

```csharp {linenos=table}
[Authorize]
public class EventsController : Controller
{

    private EventDbContext context;

    public EventsController(EventDbContext dbContext)
    {
        context = dbContext;
    }

    [AllowAnonymous]
    // GET: /<controller>/
    public IActionResult Index()
    {
        List<Event> events = context.Events
            .Include(e => e.Category)
            .ToList();

        return View(events);
    }

    // Other action methods here!
}
```

Now every user can see available events, but only logged-in users can add, edit, or delete events!
