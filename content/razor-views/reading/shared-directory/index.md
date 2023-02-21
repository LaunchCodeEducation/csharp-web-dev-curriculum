---
title: "The Shared Directory"
date: 2023-02-09T12:48:24-06:00
draft: false
weight: 8
originalAuthor: Courtney Frey # to be set by page creator
originalAuthorGitHub: speudusa # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

[Earlier in the lesson]({{<relref "../creating-templates/index.md">}}), we touched upon the role of `_Layout.cshtml`. When we set Layout to `null`, the header, footer, and Bootstrap disappear from our site and we are left with static HTML. `_Layout` is in the `Shared` directory of the `Views` directory. Files inside this `Shared` directory are used sitewide and can be accessed by the templates we create when we are working with our controllers. These files help us DRY our code.

## Layout pages

Whenever we create a new project, we get one layout page, `_Layout.cshtml`, and this file contains links to Bootstrap. Layout pages in ASP.NET MVC focus on the header and footer of the site. The header and footer of our site when we first create it contains links to important info like a privacy statement. As you work on your application, you may want your header and footer for each page to include your own privacy statement or a contact page. When you make updates to `_Layout`, every template in the application using `_Layout` reflects the updates you have made.

## Partial Views
If you want to create repeatable elements of your webpage that are contained within the main body of the page, you can use a **partial view**. Partial views are blocks of HTML elements that we want to use across multiple templates.

### Making a Partial View
Let’s assume that you want to add the same set of links to multiple pages within your web project.

```csharp {linenos=table}
<a href = "https://www.launchcode.org">LaunchCode</a> <br/>
<a href = "https://www.lego.com">Play Well</a> <br/>
<a href = "https://www.webelements.com">Other Building Blocks</a>
```

Instead of pasting this code into every template, we will store the HTML in a separate file.

1. Create a new view inside the Shared folder and give it a clear name, such as `_LinkListPartial.cshtml`.
   {{% notice tip "Tip" "rocket" %}}
   
   If the partial view you are creating is only going to be used for the views for one controller, you can put the partial view in the controller’s folder in the `Views` directory.

   {{% /notice %}}

1. Add the code to your file and save!

We can now pull our partial view into any template in our project.

### `<partial>`
This tag helper does just what the name implies—it replaces the tag that contains it with the selected partial view.

Now let’s see how to pull a partial view into a template:

```csharp {linenos=table}
<!-- template code -->

<partial name="/Views/Shared/_LinkListPartial.cshtml" />

<!-- more template code -->
```

When the code runs, the `name` attribute in the `<partial>` tag helper gives the path to the partial view. In the example above, the partial view is named `_LinkListPartial.cshtml` and is in the `Shared` folder in the `Views` directory. The code inside the partial view is then rendered as part of the HTML page.

## Check Your Understanding

{{% notice green "Question" "rocket" %}}
Given our code in _LinkListPartial.cshtml, which is stored in the Events directory:
```csharp {linenos=table}
<a href = "https://www.launchcode.org">LaunchCode</a> <br/>
<a href = "https://www.lego.com">Play Well</a> <br/>
<a href = "https://www.webelements.com">Other Building Blocks</a>
```
Which of the following would place the partial view inside a `<div>` element in the template?

1. `<div name="Views/Events/_LinkListPartial.cshtml"></div>`
1. `<div><partial>Views/Events/_LinkListPartial</div>`
1. `<div><partial name="/Views/Events/_LinkListPartial.cshtml" /></div>`
1. `<p><div partial="/Views/Events/_LinkListPartial.cshtml"></div></p>`

<!-- ans:  `<div><partial name="/Views/Events/_LinkListPartial.cshtml" /></div>` -->
{{% /notice %}}


 



