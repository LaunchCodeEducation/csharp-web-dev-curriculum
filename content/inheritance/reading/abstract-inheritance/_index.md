---
title: "Inheriting from Abstraction"
date: 2023-01-31T15:39:38-06:00
draft: false
weight: 4
originalAuthor: Courtney Frey # to be set by page creator
originalAuthorGitHub: speudusa # to be set by page creator
reviewer: # to be set by the page reviewer
reviewerGitHub: # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

## `abstract` Classes

We noted in the introduction to this section that inheritance is a way to share behaviors among classes. You’ll sometimes find yourself creating a base class as a way to share behaviors among related classes. However, in such situations it is not always desirable for instances of the base class to be created.

For example, suppose we began coding two classes, `HouseCat` and `Tiger`. Upon writing the code, we realized that there was some common data and behaviors. For example, they both make a noise, come from the same biological family, and get hungry. In order to reduce code repetition, we combined those in `Cat`.

```csharp{linenos=table,hl_lines=[],linenostart=1}
public class Cat
{
   // Cat class definition
}

public class HouseCat : Cat
{
   // HouseCat class definition
}

public class Tiger : Cat
{
   // Tiger class definition
}
```

In reality, though, we might not want objects of type `Cat` to be created, since such a cat couldn’t actually exist (a real cat would have a specific genus and species, for example). We could prevent objects of type `Cat` from being created, while still enabling sharing of behavior among its subclasses, by making `Cat` an **abstract class**.

Change the signature on `Cat`:

```csharp{linenos=table,hl_lines=[],linenostart=4}
public abstract class Cat
{
   // Cat class definition
}
```

Now, in Program.cs, if you try creating a new Cat object,

```csharp
Cat salem = new Cat(8);
```

Visual Studio has your back with a handy error message that an abstract class cannot be instantiated.

In order to use the behavior of an abstract class, *we must extend it*.

## `abstract` Methods

We have another tool that we may use here, which is an **abstract method**. An abstract method is a method in an abstract class that does not have a body. In other words, it does not have any associated code, only a signature. It must also be marked `abstract`.

In our abstract `Cat` class, it would make sense to make an abstract `Noise` method since all types of cats make noise. By creating this abstract method, we force any class that extends `Cat` to provide its own implementation of that behavior.

```csharp
public abstract string Noise();
```

Now, classes such as `HouseCat` and `Tiger`, which both extend `Cat`, must provide their own version of `Noise`, with the exact same method signature, but without the `abstract` keyword.

## Check Your Understanding

{{% notice green  "Question" "rocket" %}} 

**True/False:** A class derived from an abstract class must implement all of the abstract methods it inherits.

<!-- ans: True -->
{{% /notice %}}


{{% notice green  "Question" "rocket" %}} 

When might a programmer want to make a class abstract?

   1. When a class has no real data or behavior
   1. When expressionism just won’t cut it
   1. When that class needs to be instantiated i   n more than one package
   1. When shared behavior is desired among a group of non-abstract classes

<!-- ans: When shared behavior is desired among a group of non-abstract classes  -->
{{% /notice %}}