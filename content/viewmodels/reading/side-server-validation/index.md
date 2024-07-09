---
title: "Server-Side Validation"
date: 2023-02-24T08:57:18-06:00
draft: false
weight: 2
originalAuthor: Courtney Frey # to be set by page creator
originalAuthorGitHub: speudusa # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

Web applications work under the client-server model. We have been focusing on the server portion, using ASP.NET Core MVC and C# to create server-side application code. A critical component of any well-made web application is **validation**, which is the process of checking that data conforms to certain criteria. Validation ensures that the application only stores meaningful data.

{{% notice blue "Example" "rocket" %}} 
Consider a user registration form on a web site. Effective validation rules might require that:

- The username is between 3 and 12 characters long, and
- The password is between 6 and 20 characters long.

{{% /notice %}}

Web applications should validate all data submitted by users. This ensures that data remains well-structured and unexpected errors don’t occur. Validation that occurs in the browser—using JavaScript or HTML attributes—is **client-side** validation. Validation that occurs on the web server is **server-side** validation.

Even if client-side validation is done, it is still critical to validate data on the server. This is because client-side validation can often be bypassed by a savvy user. For example, such a user might modify HTML using a browser’s developer tools, or disable JavaScript.

Server-side validation involves both the model and controller. 
- The model is responsible for _defining_ validation rules. 
- The controller is responsible for _checking_ validation rules when data is submitted to the server.



## Check Your Understanding

{{% notice green  "Question" "rocket" %}} 
The best practice for validating data in a web app is to:

1. Use client-side validation
1. Use server-side validation
1. Use both client-side and server-side validation
1. Don’t validate incoming data 

<!-- ans:  Use both client-side and server-side validation -->
{{% /notice %}}