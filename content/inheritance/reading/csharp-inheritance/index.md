---
title: "Inheritance in C#"
date: 2023-01-31T15:39:38-06:00
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

Let’s examine an inheritance relationship between two classes: `Cat` and `HouseCat`. `HouseCat` is a class that inherits from Cat, so `HouseCat` receives the data and behaviors of Cat. These inherited traits are things like fields, properties, and methods. Any fields and non-constructor methods in Cat are available to each instance of `HouseCat`.

When we speak about an inheritance relationship, we say that a `HouseCat` is a `Cat`, or **extends** `Cat`. In order to define a class that inherits from another, we use the `:` syntax.

```csharp{linenos=table,hl_lines=[],linenostart=1}
public class Cat
{
   // ...code for the Cat class...
}

public class HouseCat : Cat
{
   // ...code for the HouseCat class...
}
```

We say that `HouseCat` is a **subclass**, **derived class**, or **child class** of `Cat`, and we say that `Cat` is the **superclass**, **base class**, or **parent class** of `HouseCat`.

In C#, a class may extend only one class. Classes may extend each other in turn, however. This creates hierarchies of classes. We often visualize these by drawing each class as a box, with an arrow pointing from the subclass to the base class. The image below show that `B` extends `A`.

   {{< rawhtml >}}
   <img src="../../pictures/inheritance-basic.png" alt="B extends A" width=60% />
   {{< /rawhtml >}}

   The shaded portion of these boxes can include additional information about each class. We’ll learn about what we might put here in a little bit.

Inheritance is an essential mechanism for sharing data and behavior between related classes. Using it effectively creates organized code with groups of classes that have increasingly specialized behavior.

When this happens, we can visualize the inheritance structure with a slightly more complex diagram.

   {{< rawhtml >}}
   <img src="../../pictures/inheritance-tree.png" alt="Inheritance tree with many nodes" width=80% />
   {{< /rawhtml >}}

You can see that classes `B`, `C`, and `D` all extend class `A`. And class `E` extends class `D` which itself extends class `A`. So class `E` involves an even greater specialization of behavior than class `D`.

Fields and non-constructor methods are directly available to instances of the subclass, subject to any access modifiers. In general, this means that `private` and `internal` members of a base class are not accessible to a subclass. However, if the subclass and base class are in the same assembly, `internal` allows access to a member.

{{% notice blue "Note" "rocket" %}} 

If anything in the last paragraph was fuzzy, this is a good time to review [access modifiers in C#]({{< relref "../../../classes/reading/modifiers/index.md" >}}).

{{% /notice %}}

## Check Your Understanding

{{% notice green  "Question" "rocket" %}} 

Which of the following is NOT a term for one class that extends another:

   1. subclass
   1. derived class
   1. extension class
   1. child class

   <!-- ans: extension class -->

{{% /notice %}}


{{% notice green  "Question" "rocket" %}} 

A class, `Greeting`, extends another class, `Message`. By convention, how would we represent the relationship between these classes in a diagram?

   1. two boxes with an arrow pointing from `Greeting` to `Message`
   1. two boxes with an arrow pointing from `Message` to `Greeting`
   1. two boxes with `Greeting` positioned inside of `Message`
   1. two boxes with `Greeting` positioned directly beneath `Message`

<!-- ans: two boxes with an arrow pointing from ``Greeting`` to ``Message`` -->

{{% /notice %}}