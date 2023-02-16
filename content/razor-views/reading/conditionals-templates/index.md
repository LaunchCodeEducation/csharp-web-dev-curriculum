---
title: "Conditionals in a Template"
date: 2023-02-09T12:48:24-06:00
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

In addition to iteration, Razor can also add or remove content on a webpage based on certain conditions. Going back to the coffee example, we could generate the ordered list ONLY IF coffeeOptions contains data. If the list of coffee types is empty, then there is no need to include the `<ol>` element. Instead, the template could include a `<p>` element with text stating that there are no options to select.

## Display Content `if/else`

To include conditional logic to display a Razor template element, we use a basic C# if clause.

The general syntax for including a conditional in Razor is:

```csharp
@if (condition)
{
   // HTML element(s) to add or additional template logic
}
```

Above, `condition` represents any expression that can be evaluated to `true` or `false` (ie, a boolean).

If `condition` evaluates to `true`, then Razor adds the HTML element to the webpage and the content is displayed in the view. If `condition` is `false`, then Razor does NOT generate the element, and the content stays off the page.

Let’s look at an example:

{{% notice blue "Example" "rocket" %}} 
Assume that `userSelection` represents a string property on `ViewBag`.

```csharp{linenos=table,hl_lines=[1, 3, 5, 11],linenostart=1}
@if (ViewBag.userSelection == "Instant")
{
   <p>Are you sure about that?</p>
}
else if (ViewBag.userSelection == "French Roast")
{
   <p>Oooh la la!</p>
}
else
{
   <p>Thanks for your order</p>
}
```
{{% /notice %}}

The `@if` statement in line 1 compares a user’s brew choice to the string `"Instant"`. If they match, then Razor adds the paragraph element to the view. If they do not match, then the `<p>` tag on line 3 is not created and the condition on line 5 is evaluated. If that `else if` statement is true, then a paragraph element with different internal text is added. Lastly, if neither of those conditions is met, then the paragraph element with text on line 11 is rendered.

{{% notice blue "Note" "rocket" %}} 

We don’t add an additional `@` symbols on lines 5 and 9 in the example above. `if`, `else if`, and `else` clauses are dependent and treated as one C# code block in Razor.
 
{{% /notice %}}

### Nesting Logic

Just as we can nest loops, we can nest any C# in Razor for advanced control flow.

