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

The `@if` statement in line 1 compares a user’s brew choice to the string `"Instant"`. If they match, then Razor adds the paragraph element to the view. 

If they do not match, then the `<p>` tag on line 3 is not created and the condition on line 5 is evaluated. 

If that `else if` statement is true, then a paragraph element with different internal text is added. Lastly, if neither of those conditions is met, then the paragraph element with text on line 11 is rendered.

{{% notice blue "Note" "rocket" %}} 

We don’t add an additional `@` symbols on lines 5 and 9 in the example above. `if`, `else if`, and `else` clauses are dependent and treated as one C# code block in Razor.
 
{{% /notice %}}

### Nesting Logic

Just as we can nest loops, we can nest any C# in Razor for advanced control flow.

{{% notice blue "Note" "rocket" %}}

Assume that userSelection represents a string property on `ViewBag`.

``` csharp{linenos=table, hl_lines=[],linenostart=1}
@if (ViewBag.coffeeOptions.Count > 1)
{
   <ol>
      @foreach(string coffeeType in ViewBag.coffeeOptions)
      {
         <li>@coffeeType</li>
      }
   </ol>
}
```
{{% /notice %}}

The conditional in line 1 checks that coffeeOptions contains more than one item. If true, then the ordered list is rendered in the view using a @foreach loop.

### Adding vs. Displaying/Hiding

A conditional statement in a Razor template determines if content is added or not added to a page. This is different from deciding if content should be _displayed_ or _hidden_.

_Hidden_ content still occupies space on a page and requires some amount of memory. When `@if` evaluates to `false`, content remains absent from the page—requiring neither space on the page nor memory. This is an important consideration when including items like images or videos on your website.

## Try It Out in `HelloASPDotNET`

What happens if a user enters an empty string?  What would happen if `name` was `null`?  It's not pretty.

Use conditional logic to prevent empty strings or null values from making it to the view.  Could you provide a generic or default option in the view?

  {{% expand "Check your code" %}}
  ```csharp{linenos=table,linenostart=8}
  @if(ViewBag.person == null || ViewBag.person == "")
  {
      <h1>Welcome, World!</h1>
  }
  else
  {
      <h1>Welcome, @ViewBag.person!</h1>
  }
  ```
  {{% /expand %}}

## Check Your Understanding

Assume you have a list of integers called `numbers`, and you display the values in an unordered list.

```csharp{linenos=table,hl_lines=[],linenostart=1}
<ul>
   @foreach(int number in ViewBag.numbers)
   {
      <li>@number</li>
   }
</ul>
```

{{% notice green "Question" "rocket" %}}
You want to display the list only if `ViewBag.numbers` contains data. Where is the best spot to put this conditional?

1. Above line 1
1. Above line 2
1. Above line 3
1. Above line 4

<!-- Answer =  Above line 1 -->
{{% /notice %}}

{{% notice green "Question" "rocket" %}}
You want to display the list only if `ViewBag.numbers` contains data. What is the best way to write this conditional statement?

1. `if (numbers.Count)`
1. `if (ViewBag.numbers != null)`
1. `@if ViewBag.numbers`
1. `@if (ViewBag.numbers.Count > 0)`

<!-- ans: @if (ViewBag.numbers.Count > 0) {} -->
{{% /notice %}}