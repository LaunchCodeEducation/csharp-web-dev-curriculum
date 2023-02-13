---
title: "Modifiers in C#"
date: 2023-01-23T13:36:52-06:00
draft: false
weight: 2
originalAuthor: Sally Steuterman # to be set by page creator
originalAuthorGitHub: gildedgardenia # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

## Access Modifiers

For fields in classes, the **access level** determines who can get or set
the value of the field. For methods, the **access level** determines who can
call the method. The access level of a class member is determined by an
**access modifier**.

We’ve encountered access modifiers so far in our code. In our examples, you
frequently see the keyword, **public**. `public` makes the field or method to
be accessible by anyone working with our code. Another common access modifier
is **private**, which restricts access to fields or methods so they can only be
used within the class. Two additional access modifiers are available in C#,
though they are used much less often than `public` and `private`.

{{% notice blue "Example" "rocket" %}}

   Let's take another look at our `HelloWorld` class from the last section,
   but with one small change.

   ```csharp {linenos=table}
      public class HelloWorld 
      {

         string message = "Hello World";

         void SayHello() 
         {
            Console.WriteLine(message);
         }

      }
   ```

   In this `HelloWorld` class, we omit the `public` access modifier in lines
   4 and 6. Doing this implicitly gives the message field and the `SayHello()`
   method **default access**.

{{% /notice %}}

We should avoid giving everything default access when creating classes in C#
and instead think carefully about what level of access each field and method
should have.

The table below details whether or not information can be accessed at different
levels based on the access modifier. For example, a field with the `private`
access modifier can be accessed within the class, but cannot be accessed
outside the class at the assembly or world-level. In C#, an **assembly** refers
to a grouping of classes and other resources that form a particular unit of an application.
**World-level** is the level of the whole application and contains all of the packages and 
classes. While we will discuss later how to decide which access modifier to use for different
scenarios, you should save this table now as reference for those conversations.

| Modifier | Class | Assembly | World |
|----------|-------|----------|-------|
| `public` | Yes | Yes | Yes |
| `protected` | Yes | No | No |
| `internal` (default for classes) | Yes | Yes | No |
| `protected internal` | Yes | Yes | No |
| `private` (default for class members) | Yes | No | No |

{{% notice blue "Note" "rocket" %}}

   If you would like to learn more about access modifiers, you should check out the [documentation](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/access-modifiers) on the subject.

{{% /notice %}}

Let's take a look at our `HelloWorld` class again and add some access
modifiers.

{{% notice blue "Example" "rocket" %}}

   ```csharp {linenos=table}
      public class HelloWorld 
      {

         private string message = "Hello World";

         public void SayHello() 
         {
            Console.WriteLine(message);
         }

      }
   ```

{{% /notice %}}

Since `message` only needs to be used by `SayHello()`, we declare it to be
`private`. Since we want `SayHello()` to be usable by anybody else, we
declare it to be `public`.

{{% notice blue "Note" "rocket" %}}

   In C#, you should always use the most restrictive access modifier
   possible. Minimizing access to class members allows code to be
   refactored more easily in the future, and hides details of how you
   implement your classes from others.

   This makes your code more modular and modifiable. Each public member
   that you expose is another field or property that can be referenced
   directly elsewhere in any program using your class. Thus, changing any
   such field in your code could potentially break any code referencing
   such members. The fewer public members, the more you can change your
   code without breaking stuff elsewhere.

{{% /notice %}}


## Check Your Understanding

{{% notice green "Question" "rocket" %}}

   For this question, refer to the code block below.

   ```csharp {linenos = table}
      public class Greeting 
      {

         string name = "Jess";

         public void SayHello() 
         {
            Console.WriteLine("Hello " + this.name + "!");
         }
      }
   ```

   What access modifier would you give `name`?

   1. no access modifier
   1. `public`
   1. `private`
   1. `protected`

{{% /notice %}}

<!-- c, private. -->