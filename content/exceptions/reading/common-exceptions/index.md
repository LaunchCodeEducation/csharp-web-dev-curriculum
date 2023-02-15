---
title: "Common Exception Objects"
date: 2023-02-08T10:27:25-06:00
draft: false
weight: 3
originalAuthor: Courtney Frey # to be set by page creator
originalAuthorGitHub: speudusa # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

Below is a summary of some of the more commonly used exception types in C#. As we mention before, all exceptions extend the `System.Exception` class.

{{% notice blue "Note" "rocket" %}} 

It is also possible to write your own exception type that inherits from System.Exception. You may find that your particular cause of error elicits a custom exception type. We won’t cover how to write custom exception objects in this book, but you can read about how to define your own exception [here](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/exceptions/creating-and-throwing-exceptions#defining-exception-classes).

{{% /notice %}}

The examples in this table are excerpted from [this page](https://learn.microsoft.com/en-us/dotnet/api/system.exception?view=net-6.0#choosing-standard-exceptions), where you can find several other commonly used exception types.

## Common Exception Types in C#

{{% expand "ArgumentOutOfRangeException" %}}

Thrown by methods that verify that arguments are in a given range.

*Example:* 
   ```csharp   
   String s = "string";   
   s.Substring(s.Length+1);
   ```
{{% /expand %}}

{{% expand "ArgumentNullException" %}}

Thrown by methods that do not allow an argument to be `null`.

*Example:* 
   ```csharp
   String s = null;
   "Calculate".IndexOf(s);
   ```
{{% /expand %}}

{{% expand "IndexOutOfRangeException" %}}

Thrown when an array is indexed improperly.

*Example:*
   ```csharp
   //Indexing an array outside its valid range:
   arr[arr.Length+1]
   ```
{{% /expand %}}

{{% expand "InvalidOperationException" %}}

Thrown by methods when in an invalid state.

*Example:*
   ```csharp
   //Calling an Enumerable method on an empty collection: 
   Enumerator.MoveNext()
   ```
{{% /expand %}}

{{% expand "NullReferenceException" %}}

Thrown when a `null` object is referenced.

*Example:*
   ```csharp
   object o = null;
   o.ToString();
   ```   
{{% /expand %}}

As with catching, be specific with which types of exceptions you throw. Never throw an instance of the base `Exception` class. If a built-in exception type works well based on it’s documented intended use, then use it! If there isn’t a built-in exception that matches your needs, then you can use a custom exception type.

## Check Your Understanding

{{% notice green  "Question" "rocket" %}} 

When should you write your own exception class?

   1. The error the your code encounters is very specific and targeted.
   1. You know your code will produce an error, but you’re not sure which exception is the best fit.
   1. Writing custom exception classes is done by .NET developers only.
   1. Never, don’t do it. 

<!-- ans: The error the your code encounters is very specific and targeted. -->

{{% /notice %}}

{{% notice green  "Question" "rocket" %}} 

Suppose you have created an empty array of Temperature objects :

```csharp
Temperature[] temps = new Temperature[] { };
```
What, if any, exception would you expect to encounter when the following line executes:

```csharp
double firstTemp = temps[0].Fahrenheit;
```

1. No exception will be thrown — `temps[0].Fahrenheit` will return `null`.
1. `NullReferenceException` — the object at `temps[0]` is null.
1. `InvalidOperationException` — cannot access the object’s property.
1. `IndexOutOfRangeException` — the array is empty.

<!-- ans: ``IndexOutOfRangeException`` --- the array is empty. -->

{{% /notice %}}

