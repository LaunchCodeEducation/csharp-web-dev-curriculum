---
title: "Classes for C#"
date: 2023-01-23T13:36:52-06:00
draft: false
weight: 1
originalAuthor: Sally Steuterman # to be set by page creator
originalAuthorGitHub: gildedgardenia # to be set by page creator
reviewer: # to be set by the page reviewer
reviewerGitHub: # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

In previous programming studies, we have come across **classes** and
**objects**. Classes and objects in C# are similar to classes and objects in
other languages.

## A Minimal Class and Object

Classes may contain **fields** and **methods**. Fields contain the data of a
class and methods define actions a class can take. We say that fields and
methods are **members** of a class.

{{% notice blue "Example" "rocket" %}}

   Let's create a class called `HelloWorld` with one field, `message`, and one method, `SayHello()`.
   `message` will be a string and have a value of `"Hello World"`.
   `SayHello()` will not return a specific value and instead print out the value of `message`.

   ```csharp {linenos=table}
      public class HelloWorld 
      {

         public string message = "Hello World";

         public void SayHello() 
         {
            Console.WriteLine(message);
         }

      }
   ```

{{% /notice %}}

The only field in the `HelloWorld` class is the string `message`, while the
only method is `SayHello()`, which prints the value of the `message` field
and doesn’t return anything.

{{% notice blue "Note" "rocket" %}}
   There is no `main` method, which is required to run a C# program.
   Without it, we have to do some additional work to get our program to run!
{{% /notice %}}

To execute `SayHello()`, we’ll need to create an **instance** of the
class `HelloWorld`. We refer to an object created from a particular class as
an instance of that class.

Here’s how this might look with our `HelloWorld` class:

{{% notice blue "Example" "rocket" %}}

   ```csharp {linenos=table}
      HelloWorld hello = new HelloWorld();
      hello.SayHello();
   ```

{{% /notice %}}

In order to call the `SayHello()` method of `HelloWorld`, we must
first have an instance of `HelloWorld`, which we create using the
syntax `new HelloWorld()`. As with built-in classes, classes that we
create define their own types. So the object `hello` is a variable of
type `HelloWorld`.

We introduced this `HelloWorld` class as a means of illustrating the simplest
representation of some basic concepts in C#. The goal of the next few
lessons is to build up the machinery to create a wide variety of
interesting classes that can be used to create complex programs and
elegantly solve difficult problems.

## The `this` Keyword

In `HelloWorld` above, we could have written `SayHello` this way,
with the same net effect:

```csharp {linenos=table, linenostart=6}
   public void SayHello() 
   {
      Console.WriteLine(this.message);
   }
```

In this context, inside of the class, we can refer to fields (and
methods) that belong to the class using the special object, `this`.
Whenever you use `this`, it *always* refers to the object that the
given code is currently within. In other words, `this` will always be
an instance of the given class. Since it is not legal to create code
outside of a class in C#, `this` nearly always makes sense to use
(there’s one exception, that we’ll encounter soon).

You are allowed to create local variables (variables declared
within a method) with the same name as a field of the given class. In
this case, in order to refer to the field, we *must* use `this`.

{{% notice blue "Example" "rocket" %}}

   Let's look at how this works with our ``HelloWorld`` class:

   ```csharp {linenos=table}
      public class HelloWorld 
      {

         public string message = "Hello World";

         public void SayHello() 
         {

            string message = "Goodbye World";

            // The line below prints "Goodbye World"
            Console.WriteLine(message);

            // The line below prints "Hello World"
            Console.WriteLine(this.message);
         }
      }
   ```

{{% /notice %}}

{{% notice orange "Warning" "rocket" %}}

   When a local variable has the same name as a field, we say that the
   local variable **shadows** the field. Errors caused by shadowing can be
   tricky to spot, so it’s best to avoid doing this in your code.

{{% /notice %}}

{{% notice blue "Note" "rocket" %}}

   If you want to learn more about this subject, check out the documentation on [using the this keyword]( https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/this).

{{% /notice %}}

## Check Your Understanding

{{% notice green "Question" "rocket" %}}

   The following code block contains several bugs. Mark all of the lines that contain a bug in the code.

   ```csharp {linenos=table}
      public class Greeting 
      {

         public String name = "Jess"

         public void SayHello() 
         {
            Console.WriteLine("Hello " + here.name + "!");

      }
   ```

   1. line 9
   1. line 4
   1. line 8
   1. line 1

<!-- lines 4, 8 and 9 all have bugs. -->