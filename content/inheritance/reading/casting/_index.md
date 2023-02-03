---
title: "Casting"
date: 2023-01-31T15:39:38-06:00
draft: false
weight: 5
originalAuthor: Courtney Frey # to be set by page creator
originalAuthorGitHub: speudusa # to be set by page creator
reviewer: # to be set by the page reviewer
reviewerGitHub: # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

When one class extends another, as `HouseCat` extends `Cat`, a field or local variable of the type of the base class may hold an object that is of the type of the child class.

In other words, this is allowed:

```csharp
Cat suki = new HouseCat("Suki", 8);
```

This is acceptable because a `HouseCat` is a `Cat`. Furthermore, when we call methods on such an object, the compiler is smart enough to determine which method it should call. For example, the following call to `Noise()` will call the version defined in `HouseCat`:

```csharp
// Calls HouseCat's Noise() method
suki.Noise(); // Hello, my name is Suki!
```

This only works for methods that are declared in the base class, however. If we have a `HouseCat` object stored in a `Cat` variable or field, then it is not allowed to call methods that are only part `HouseCat`.

```csharp
// Results in a compiler error, since Cat
// doesn't have such a method
suki.IsSatisfied();
```

Here, `IsSatistfied()` is defined in `HouseCat`, and there is not a corresponding overridden method in `Cat`. If we were *really, really* sure that we had a `Cat` that was actually a `HouseCat`, we could call such a method by first casting:

```csharp
// As long as suki really is a HouseCat, this works
(suki as HouseCat).IsSatisfied();
```

The danger here is that if `suki` is in fact not a `HouseCat` (it was declared only as a `Cat`, after all) then we’ll experience a **runtime exception**. A runtime exception is an error that occurs upon running the program, and is not found by the compiler beforehand. These are dangerous, and situations where these exeptions might come up should be avoided. So you should only cast an object to another type when you are very sure that it’s safe to do so.

Storing objects of one type (e.g. `HouseCat`) in a variable or field of another compatible type (e.g. `Cat`) is an example of **polymorphism**. Polymorphism is another one of the pillars of OOP and we’ll have more to say about it in the next lesson.

## Check Your Understanding

{{% notice green  "Question" "rocket" %}} 
 
For this question, refer to the code block below.

```csharp{linenos=table,hl_lines=[],linenostart=1}
public class Message
{
   public bool Friendly { get; } = true;
   public string Language { get; }
   public string Text { get; }

   public Message(string language, string text)
   {
      Language = language;
      Text = text;
   }
}

public class Greeting : Message
{
   public bool Waving { get; set;};

   public Greeting(string language, string text) : base(language, text)
   {
   }

   public void Wave()
   {
      Waving = true;
   }
}
```

Which of the following does not contain an error:

   1. ```csharp{linenos=table,hl_lines=[],linenostart=1}
      Message hello = new Greeting("English", "Hello Coder!");
      (hello as Greeting).Wave();

      ```   
   1. ```csharp{linenos=table,hl_lines=[],linenostart=1}
      Message hello = new Greeting("English", "Hello Coder!");
      hello.Wave();

      ```  
   1. ```csharp{linenos=table,hl_lines=[],linenostart=1}
         Greeting hello = new Message("English", "Hello Coder!");
         hello.Wave();
      ```  
   1. ```csharp{linenos=table,hl_lines=[],linenostart=1}
      Greeting hello = new Greeting("English", "Hello Coder!");
      (hello as Message).Wave();
      ```  
<!-- ans: Message hello = new Greeting("English", "Hello Coder!");
         ((Greeting) hello).wave(); -->
{{% /notice %}}


{{% notice green  "Question" "rocket" %}} 
 
Polymorphism refers to:

   1. One object inheriting another
   1. An abstract class with many classes extending from it
   1. The practice of storing an object of one type in a variable of another type
   1. Shapeshifting

<!-- ans: The practice of storing an object of one type in a variable of another type -->
{{% /notice %}}