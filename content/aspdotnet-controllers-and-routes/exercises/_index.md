---
title: "Exercises"
date: 2023-02-06T14:09:15-06:00
draft: false
weight: 2
originalAuthor: Sally Steuterman # to be set by page creator
originalAuthorGitHub: gildedgardenia # to be set by page creator
reviewer: # to be set by the page reviewer
reviewerGitHub: # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

## `GET` Request

While reading the chapter, you created a basic Hello, World application using ASP.NET
called `HelloASPDotNET`. Open that project up in Visual Studio, and get ready to add some 
features.

Modify your `HelloController` class to display a form on a `GET`
request that asks the user for both their name and the language they
would like to be greeted in. It should look something like this:

.. figure:: figures/form.png
   :alt: Greeting Form

   Greeting Form

The resulting form submission should return and display the message,
“Bonjour Chris”.

{{% notice blue "Note" "rocket" %}}

   The language is presented in a dropdown, more formally known as a `select` element. 
   For more information about the `select` element and how it works, read the 
   [MDN documentation](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select).

{{% expand "Check your solution" %}}

{{% /expand %}}

## `POST` Request

When the user submits the form (via a `POST` request), they should be
greeted in the selected language. Your new feature should: 

1. Include at least 5 languages, with English being the default. If you don’t speak 5 
   languages yourself, ask your friend 
   [the Internet](http://pocketcultures.com/2008/10/30/say-hello-in-20-languages/).
1. Include a new `public static` method, `CreateMessage`, in the `HelloController` 
   that takes a name as well as a language string. Based on the language string, you’ll 
   display the proper greeting.

   {{% expand "Check your solution" %}}

   {{% /expand %}}

## Bonus Mission

1. Add some more HTML and inline styles to your returned greeting
   response string so that the displayed message looks a bit nicer.