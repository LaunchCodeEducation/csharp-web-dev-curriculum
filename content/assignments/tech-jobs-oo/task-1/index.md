---
title: "Task 1: Explore the Employer Class"
date: 2023-01-11T13:15:59-06:00
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

Open the `Employer` file in Visual Studio and examine the code. In addition to the three members—`nextId`, `Id`, and `Value`—the class includes some methods like `ToString()` and `Equals()`.

You can refer to these examples as you fill in the missing pieces in the other classes, but for now let’s take a closer look at the constructors.

### Assign a Unique ID
One neat trick we can use is to automatically assign each new object a unique ID number.

Examine the two constructors in `Employer.cs`:

```csharp {linenos=true,hl_lines=[3, 6,7,8,9,10, 12,13,14,15],linenostart=1}
public class Employer {
   public int Id { get; }
   private static int nextId = 1;
   public string Value { get; set; }

   public Employer ()
   {
      Id = nextId;
      nextId++;
   }

   public Employer (string value) : this()
   {
      Value = value;
   }

   // Additional methods omitted from this code block
```

1. Line 3 declares the field `nextId`. Since it is static, its changing value is NOT stored within any `Employer` object.

1. The first constructor (lines 6 - 10) accepts no arguments and assigns the value of `nextId` to the id field. It then increments `nextId`. Thus, every new `Employer` object will get a different ID number.

1. The second constructor (lines 12 - 15) assigns the value field. It ALSO initializes id for the object by calling the first constructor statement with the `:this()` syntax. Including `:this()` in any `Employer` constructor makes initializing id a default behavior.

{{% notice green "Tip" "rocket" %}} 
By adding `: this()` to the signature of the second `Employer` constructor, we are using a new technique called constructor chaining. For more info on how this chaining technique works, check out this [blog post](https://www.codecompiled.com/csharp/constructor-chaining-c/)!
{{% /notice %}}

On to [Task 2]({{< relref "../task-2/index.md" >}}).