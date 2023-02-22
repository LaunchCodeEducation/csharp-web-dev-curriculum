---
title: "Iterating in a Template"
date: 2023-02-09T12:48:24-06:00
draft: false
weight: 4
originalAuthor: Courtney Frey # to be set by page creator
originalAuthorGitHub: speudusa # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

Let’s revisit part of the non-efficient HTML from the introduction, where we hard-coded coffee options in a list.

```csharp{linenos=table,hl_lines=[],linenostart=1}
<ol>
   <li>French Roast</li>
   <li>Espresso</li>
   <li>Kopi Luwak</li>
   <li>Instant</li>
</ol>
```

If we want to add, remove, or edit the list items, we need to go in and change the individual tags, which is a poor use of our time. Fortunately, there is a way to streamline the process.

In C#, we use a [foreach Loop]({{<relref "../../../flow-collections/reading/loops/_index.md">}}) to iterate through the items in a data collection.

```csharp{linenos=table,hl_lines=[],linenostart=1}
foreach (type item in items)
{
   //...code here...
}
```

Razor templates allow us to use a `foreach` loop to display items in a collection.

```csharp{linenos=table,hl_lines=[],linenostart=1}
<ol>
   @foreach (type collectionItem in ViewBag.collectionProperty)
   {
      <li>@collectionItem</li>
   }
</ol>
```

Let's explore line 2 to better understand how we are using the `foreach` loop in the Razor View.

1. The `@` specifies the C# portion of the template.
1. The `@foreach` loop is initiated inside of a list element (either `<ol>` or `<ul>`).
1. `collectionItem` represents an individual item or element within the collection.
1. `ViewBag.collectionProperty` represents any collection that has been assigned as a property on `ViewBag`.

We can think of this syntax as saying, _“For each item within the `ViewBag` property, `collectionProperty`, repeat this HTML tag, but use the current value of `collectionItem`.”_

Let’s apply this new concept to the HTML coffee list example. Assume that we store each of the coffee names as strings in a `List` called `ViewBag.coffeeOptions`.

```csharp{linenos=table,hl_lines=[],linenostart=1}
<ol>
   @foreach (string coffeeType in ViewBag.coffeeOptions)
   {
      <li>@coffeeType</li>
   }
</ol>
```
Some points to note:
1. `coffeeOptions` is accessible to the template because it is a property of the `ViewBag` object.

1. In the first pass through the loop, `coffeeType` takes the value of the first coffee name in the `coffeeOptions` list.

1. `@coffeeType` displays the value of `coffeeType` in the view, so the `li` element will show the first coffee name.

1. Each successive iteration, `coffeeType` takes the next value in the list, and Razor adds a new `<li></li>` element to display that data.

{{% notice orange "Warning" "rocket" %}} 
 
`@foreach` creates one HTML tag for each item in a collection. BE CAREFUL where you place it.

Consider the following Razor code:

```csharp{linenos=table,hl_lines=[],linenostart=1}
<div>
   <h3>Coffee Types</h3>
   @foreach (string coffeeType in ViewBag.coffeeTypes)
   {
      <ol>
         <li>@coffeeType</li>
      </ol>
   }
</div>
```

The final HTML produced is one heading, 4 ordered lists, and 4 coffee names. When this view is rendered, each coffee type is labelled with “1”.

```csharp{linenos=table,hl_lines=[],linenostart=1}
<div>
   <h3>Coffee Types</h3>
   <ol>
      <li>French Roast</li>
   </ol>

   <ol>
      <li>Espresso</li>
   </ol>

   <ol>
      <li>Kopi Luwak</li>
   </ol>

   <ol>
      <li>Instant</li>
   </ol>
</div>
```
{{% /notice %}}


## Nested Loops
Assume you have a collection of different `CoffeeShop` objects. Each object contains a string field for `name` and a field that is a list of of the brews available, `coffeeOptions`.

Below, we nest loops to display a list of the shop names and their brew options.

Sample Razor template:

```csharp{linenos=table,hl_lines=[1,3, 8],linenostart=1}
@foreach (var coffeeShop in ViewBag.coffeeShops)
{
   @*Each shop name*@
   <p>@coffeeShop.Name</p>
   <ul>
      @foreach(string coffeeType in coffeeShop.CoffeeOptions)
      {
         @*Each coffee type available*@
         <li>@coffeeType</li>
      }
   </ul>
}
```

Sample HTML output:

```csharp{linenos=table,hl_lines=[],linenostart=1}
<p>Central Perk</p>
<ul>
   <li>Espresso</li>
   <li>Instant</li>
</ul>

<p>Brews Brothers</p>
<ul>
   <li>French Roast</li>
   <li>Kopi Luwak</li>
</ul>
```

Apart from the nested loops displayed above, here are some other items you may find useful to note from the example above.

- Razor comments are seen on lines 3 and 8 in the first code block above. Comments in Razor are nested between `@*` and `*@`. You may have noticed the comment block present on the top of a new view file.

- `ViewBag.coffeeShops` is a list of `CoffeeShop` objects but we’ve used var on line 1 to type the coffeeShop item.

   In some limited circumstances, we can use the **var** keyword to implicitly type a variable. When this keyword is used, C# still assigns a type to `coffeeShop` through inference. It looks and sees that we are assigning `coffeeShop` to the value at the list index, which is a `CoffeeShop` object. Thus, `coffeeShop` is of type `CoffeeShop`.

   Alternatively, Razor does also allow us to import a custom class, such as CoffeeShop. If we wanted to do so, we could import the class or its namespace at the top of the template with a [using]({{<relref "../../../data-types-and-variables/reading/some-csharp-practice/index.md">}}) statement.

{{% notice orange "Warning" "rocket" %}} 

We use `var` above to simplify the example and focus on the loop action. In general, we recommend that you avoid using `var` while you are learning C#. Even after you become more experienced with the language, you will still only want to use it sparingly and in specific circumstances. Explicitly declaring the type of your variables makes for more readable code, to name only one benefit.
 
{{% /notice %}}

## Check Your Understanding

{{% notice green  "Question" "rocket" %}} 

What is the HTML outcome you expect from the Razor code below?

```csharp{linenos=table,hl_lines=[],linenostart=1}
<div>
   <h3>Coffee Types</h3>
   <ol>
      @foreach (string coffeeType in ViewBag.coffeeTypes)
      {
         <li>@coffeeType</li>
      }
   </ol>
</div>
```

1. One heading, 4 ordered lists, and 4 coffee names (each name labeled as “1”)?
1. One heading, one ordered list, and 4 coffee names (with the names labeled “1”, “2”, “3”…)?
1. 4 headings, 4 ordered lists, and 4 coffee names (each name labeled as “1”)?
1. 4 headings, 4 ordered lists, and 16 coffee names (with the names labeled “1”, “2”, “3”…)?

<!-- ans: One heading, 4 ordered lists, and 4 coffee names (each name labeled as “1”)? -->
{{% /notice %}}


{{% notice green  "Question" "rocket" %}} 

What is the HTML outcome you expect from the Razor code below?

```csharp{linenos=table,hl_lines=[],linenostart=1}
@foreach (string coffeeType in ViewBag.coffeeTypes)
{
   <div>
      <h3>Coffee Types</h3>
      <ol>
         <li>@coffeeType</li>
      </ol>
   </div>
}
```

1. One heading, 4 ordered lists, and 4 coffee names (each name labeled as “1”)?
1. One heading, one ordered list, and 4 coffee names (with the names labeled “1”, “2”, “3”…)?
1. 4 headings, 4 ordered lists, and 4 coffee names (each name labeled as “1”)?
1. 4 headings, 4 ordered lists, and 16 coffee names (with the names labeled “1”, “2”, “3”…)?

<!-- ans: 4 headings, 4 ordered lists, and 4 coffee names (each name labeled as “1”)? -->
{{% /notice %}}
