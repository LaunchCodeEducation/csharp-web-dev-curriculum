---
title: "Templates"
date: 2023-02-09T12:48:24-06:00
draft: false
weight: 1
originalAuthor: Courtney Frey # to be set by page creator
originalAuthorGitHub: speudusa # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

Take a look at the homepage for [WebElements](https://www.webelements.com/). The content includes text, images, a navigation bar, a search box, linked menu options at the bottom of the page, and 118 carefully colored boxes with links—one for each element on the periodic table. All of this content is very deliberately arranged and styled.

Imagine your boss tasks you with creating this website. Setting up the HTML tags for the navigation bar would be straightforward, but what about the element boxes? You would need to make 118 similar structures, but with different text, links, and colors. Trying to make the table structure work would be tedious at best, and excruciatingly difficult at worst.

Also, what if a new element gets discovered, or some of the data for the elements changes? Updating the text, colors, layout, etc. means adjusting those items in the HTML. Also, if that information appears in other areas of the website, then you need to modify that code as well.

Whew! Changing the website rapidly becomes problematic, especially since it contains lots of data and consists of multiple pages. This is where templates come in to play. They help automate the tasks required to build and maintain a website.

## Templates are Frameworks

A **template** provides the general structure for a web page. Templates outline for us where different elements get placed on the page. Any page made with a template includes its elements and follows its rules. If we add content to the template or modify it in some way, all pages made from that template will reflect the changes.

Let’s see how using a template makes our lives easier.

### No Template Example

The code below displays a simple list. It defines the location for the heading and each `<li>` element, in addition to a couple of fun links. The CSS file (not shown) specifies the font, text size, colors, etc.

```csharp{linenos=table,hl_lines=[],linenostart=1}
  <body>
     <h1>Java Types</h1>
     <div class="coffeeList">
        <ol>
           <li>French Roast</li>
           <li>Espresso</li>
           <li>Kopi Luwak</li>
           <li>Instant</li>
        </ol>
     </div>
     <hr>
     <div class="links">
        <h2>Links</h2>
        <a href="https://www.launchcode.org/">LaunchCode</a> <br>
        <a href="https://en.wikipedia.org/wiki/Coffee">Coffee</a>
     </div>
  </body>
```

We could drastically improve the appearance and content of the page by playing around with the tags, classes, styles and text. However, any change we want to make needs to be coded directly into the HTML and CSS files, and this quickly becomes inefficient.

### A Better Way: Template Example

Recall that a template represents a view in the MVC world. It sets up a structure to display the data delivered by the controller, and the template guides where that information goes. This provides much more flexibility than hard-coding, since data can change based on a user’s actions.

```csharp{linenos=table,hl_lines=[],linenostart=1}
  <body>
     <h1>{templateInstructions}</h1>
     <div class="coffeeList">
        <ul>
           <li {templateInstructions}></li>
        </ul>
     </div>
     <hr>
     <div class="links">
        <h2>Links</h2>
        <a href={templateInstructions}></a>
     </div>
  </body>
  ```

This HTML looks similar to the previous example, but it replaces some of the code with _instructions_.

`{templateInstructions}` refers to instructions and data passed into the template by the controller. The curly brackets, `{}`, do not indicate real template syntax here. We will address how to write Razor template syntax in the following pages. Razor is the templating language used in this book. The brackets are used here to indicate that the instructions come from another source and are not plain HTML. Template instructions like these will automatically create HTML tags in order to display or update the information.

By using a template to build the website, changing the list or coffee types above involves altering something as simple as a C# `List` or object. After changing that data, the template does the tedious work of modifying the HTML.

### Templates Support Dynamic Content
Besides making it easier to organize and display content, templates also allow us to create a _dynamic_ page. This means that its appearance changes to fit new information. For example, we can define a grid for displaying photos in rows of 4 across the page. Whether the images are of giraffes, tractors, or balloons does not matter. The template sets the layout, and the code feeds in the data. If more photos are found, extra rows are produced on the page, but each row shows 4 images.

In the last lesson, you built a simple website that displayed a welcome message and responded to changing values for a user’s name. You did NOT apply a template for this page, and it is possible to create an interactive site without one. However, as your projects grow in size, templates make it MUCH easier to maintain your work.

## Templates Provide Structure, Not Content

Templates allow us to decide how to display data in the view, even if we do not know exactly what that data will be. Information pulled from forms, APIs, or user input will be formatted to fit within our design.

{{< rawhtml >}}
   <img src="../pictures/SampleTemplateDiagram.png" alt="Diagram of a template" />
{{< /rawhtml >}}

In the figure, the black outlines represent different areas defined by the template—spaces for lists, images, links, etc. As the controller feeds data into the template, the appearance of the page changes.

{{% notice blue "Note" "rocket" %}} 

If the template expects data for a list, but the controller does not provide the information, that part of the screen remains empty.
 
{{% /notice %}}

## Check Your Understanding

{{% notice green  "Question" "rocket" %}} 

**True/False:** Templates make your life easier as a programmer.

<!-- ans: True, Templates make programming webpages much easier by providing a dynamic way to display data -->
{{% /notice %}}

{{% notice green  "Question" "rocket" %}} 

What is the name of the templating syntax we will use in this book?

   1. HTML
   1. `templateInstructions`
   1. Razor
   1. Blazor

<!-- ans:  Razor -->
{{% /notice %}}