---
title: "Validation and Views"
date: 2023-02-24T08:57:18-06:00
draft: false
weight: 5
originalAuthor: Courtney Frey # to be set by page creator
originalAuthorGitHub: speudusa # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

While our application is properly handing errors, we need to _display_ the error messages so that the users know what information they should be adding. Client-side validation like this can prevent faulty data submissions.

## Displaying Error Messages in our View

Create a separate span element in the form. In the `<span>` tag, we can add `asp-validation-for` to specify which property’s validation error messages should be displayed if the conditions are not met.

{{% notice blue "Note" "rocket" %}} 

We don’t have to add anything else to display error messages, because that validation is already built in!

{{% /notice %}}

Now when we run our application and enter a bad event name or forget our description, we get the error message displaying what we should be entering!

If we pass our validation, we should be redirected to the `/Events` view and see the new event added to the list!

## Changing the Color of Error Messages

Making error messages a different color, such as red, is a common technique to catch the attention of the user.  We can do that by using **unobtrusive validation** methods, such as using a third-party library.

The [jQuery Unobtrusive Validation](https://github.com/aspnet/jquery-validation-unobtrusive) library. contains scripts that will perform validation tasks, such as updating the color of error messages. To utilize this library, we need to point to it in our `_Layout.cshtml` page and then add more attributes to our Views.

### `_Layout.cshtml` Updates

To utilize the library, we need to add the following references to it within the `<main>` area.

```html{linenos=table}
<main>
   @RenderBody()
   <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.6.0/jquery.js"></script>
   <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery-validate/1.19.3/jquery.validate.js"></script>
   <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery-validation-unobtrusive/3.2.12/jquery.validate.unobtrusive.js"></script>
</main>
```
In the `Add` View, you will need to create more class attributes for the library to target.

```html{linenos=table,hl_lines=[3,4],linenostart=8}
 <div asp-controller="Events" asp-action="Add" class="form-group">
     <label asp-for="Name"></label>
     <input asp-for="Name" class="form-control"/>
     <span asp-validation-for="Name" class="text-danger"></span>
 </div>
```

Note in line 10 the addition of `class="form-control"` and in line 11 `class="text-danger"`. These attributes will be noted by the jQuery Unobtrusive Validation library and print our red if the client does not meet the requirements.

You can read more about client-side validation and the jQuery Unobtrusive Validation library check out the [documentation](https://learn.microsoft.com/en-us/aspnet/core/mvc/models/validation?view=aspnetcore-6.0#client-side-validation). 

## Check Your Understanding

{{% notice green  "Question" "rocket" %}} 
**True or False**: In order to implement validation, all three elements of MVC applications are involved.

<!-- ans: true! -->
{{% /notice %}}