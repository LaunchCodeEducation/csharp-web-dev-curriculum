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
features. Before you start working, create a new branch so you can revisit where you ended the reading at.

Modify your `HelloController` class to display a form on a `GET`
request that asks the user for both their name and the language they
would like to be greeted in. It should look something like this:

![Greeting Form](pictures/form.png)

The resulting form submission should return and display the message,
“Bonjour Chris”.

{{% notice blue "Note" "rocket" %}}

   The language is presented in a dropdown, more formally known as a `select` element. 
   For more information about the `select` element and how it works, read the 
   [MDN documentation](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select).

{{% /notice %}}

{{% expand "Check your solution" %}}

```csharp {linenos=table}
   [HttpGet]
        public IActionResult Index()
        {
            string html = "<form method='post'>" +
                "<input type='text' name='name' />" +
                "<select name='language'><option value='english' selected>English</option>" +
                "<option value='spanish'>Spanish</spanish>" +
                "<option value='bosnian'>Bosnian</option>" +
                "<option value='vietnamese'>Vietnamese</option>" +
                "<option value='french'>French</option></select>" +
                "<input type='submit' value='Greet Me!'/>" +
                "</form>";

            return Content(html, "text/html");

        }

```

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

   ```csharp {linenos=table}
      public static string CreateMessage(string name, string language)
        {
            string helloTranslation = "";
            switch (language)
            {
                case "french":
                    helloTranslation = "Bonjour ";
                    break;
                case "spanish":
                    helloTranslation = "Hola ";
                    break;
                case "bosnian":
                    helloTranslation = "Zdravo ";
                    break;
                case "vietnamese":
                    helloTranslation = "Xin Chao ";
                    break;
                case "english":
                    helloTranslation = "Hello ";
                    break;
            }
            return helloTranslation + name;

        }
   ```

   {{% /expand %}}

## Bonus Mission

1. Add some more HTML and inline styles to your returned greeting
   response string so that the displayed message looks a bit nicer.