---
title: "Registrations and Logins"
date: 2022-12-15T09:16:07-06:00
draft: false
weight: 4
originalAuthor: John Woolbright # to be set by page creator
originalAuthorGitHub: jwoolbright23 # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: 12/15/22 # UPDATE ANY TIME CHANGES ARE MADE
---

In order for users to successfully navigate through the application, Identity will handle a number of functions related to both authentication and authorization. For the purposes of this book, we will focus on just two: registering for a new account and logging in.

{{% notice blue "Note" "rocket" %}}
Razor Class Libraries do not have separate controllers like in the traditional MVC design pattern. The logic that we might be inclined to put in a controller for each of the actions that we look at is actually contained within a Razor page. Our goal is to locate the correct page and understand what is going on.

The pages we are looking at end with the file extension `.cshtml.cs`. Some Mac users may have to click on a small arrow on to expand the `.cshtml` pages to find the `cshtml.cs` files.
{{% /notice %}}

## Registration

Open up `Register.cshtml.cs` in `Areas/Identity/Pages/Account` and inspect it. Here are some things to note:

1. The return type of the action to register a new user is `Task<IActionResult>`. We have encountered `IActionResult` before.
`Task<IActionResult>` is an asynchronous return type. The action of adding a new user to a database is asynchronous so our function must return an asynchronous action.
1. We can still use `ModelState.IsValid` to make sure that the user's input matches our validation requirements.
1. `UserManager` comes back into play here for the addition of the new user to the database.
The method used for that action is called `CreateAsync()`. The new user's password is hashed as part of this method, so there aren't any additional method calls here.
1. If the new user row in the database is successfully created, then we want to direct the user to a page to start working. If not, the user registration form is reloaded, just as when the validation requirements are not met.

{{% notice blue "Note" "rocket" %}}
If you are interested in learning more about asynchronous return types in C#, check out the [documentation](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/async/async-return-types).
{{% /notice %}}

## Login

Open up `Login.cshtml.cs` in `Areas/Identity/Pages/Account`.
Here are some things to note:

1. `Task<IActionResult>` is back meaning the action of signing in is asynchronous.
1. If the form input is valid, then we want to try and sign in the user.
1. `SignInManager` has a method called `PasswordSignInAsync()` which takes in parameters like the inputted email and password and compares those values to the values stored in the database.
1. If the action of signing in is successful, the user is directed on to a new page. If the action is not successful, then the user is redirected back to the login form with an error message explaining that they could not log in.

## Logout

There are two main things to note about `Logout.cshtml.cs` in `Areas/Identity/Pages/Account`:

1. `Task<IActionResult>` is the return type.
1. `SignInManager` has a method called `SignOutAsync()` which ends the session. Once that action is completed, the user is redirected to an unrestricted page.

These are the three main actions we want to focus on when it comes to authentication with user accounts. We could additional elements to these three actions such as 2FA or two factor authentication on log in as the authentication requirements of our project grow.

