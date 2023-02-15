---
title: "Interfaces"
date: 2023-02-01T13:10:40-06:00
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

An **interface** is similar to an abstract class, with some important differences. Interfaces allow us to 
create code organized by behavior, rather than static data. While some object-oriented languages encourage 
creating classes that behave like interfaces to improve software design, C# is a language that includes interfaces 
as a formal construction. Like abstract classes, interfaces cannot be instantiated and they have limitations on what 
kind of behavioral information they may contain. A C# interface may contain:

1. Constants
1. Method signatures
1. Static methods
1. Default methods

## Creating an Interface

### Method Signatures

One really useful aspect of using an interface is the ability to specify method signatures.
A **method signature** includes the name, parameters, and return
type of a method, but no body.

As part of our cat application, let's create a method signature, `Eat`, as part of an 
interface, `IFeedable`. "I" for interface, of course! More on this name below.

{{% notice blue "Example" "rocket" %}}

   ```csharp {linenos=table}
      public interface IFeedable
      {

         void Eat();

      }
   ```

{{% /notice %}}

In the code above, notice the following:

<!-- TODO: Add link back to access modifier table -->

1. We need to use the `interface` keyword to define our interface, `IFeedable`.
1. `Eat` only has a signature. We only provide a body for methods defined 
   in interfaces in special circumstances, defined below under *Default Methods*.
1. `Eat` also does not have an access modifier. Interface members are `public` by default and it's
   best practice to keep them public.
1. The `IFeedable` interface itself is declared `public`, which means any other class may 
   use it. We may also leave off `public`, making the interface `protected internal`, or 
   usable only within the same assembly. Recall this access modifier described in this
   table.
1. The name is indicative of the behavior that the interface is intended to describe. While this 
   is only a convention, most interfaces have names that are adjectives preceded with an "I". 
   While this is only a convention, you should follow it in the interest of code-readability.

### Static Methods

A static method in an interface can contain code in the body.
However, a static method cannot contain any references to instance properties in other classes.
This means that our static methods should only deal with universal behaviors that are NOT 
dependent on instance properties.


### Default Methods

A **default method** has a body and is a fully-formed method. It may be extended by classes 
implementing the interface.

```csharp {linenos=table}
   public interface IFeedable {

      void Eat();

      void Nap() {
         Console.WriteLine("snooooozzze");
      }

   }
```

The intended purpose of default methods is to allow
programmers to add a method to an interface that has already been
released, while not forcing those already using the interface to add new
code to their classes. *You should avoid using default methods in all situations other than the 
one described here.*

## Implementing an Interface

The purpose of an interface is to define a contract of behaviors that classes uphold. In 
doing so, we say that they “*implement* the interface”. The syntax for implementation is 
the same as that for inheritance --- so adhering to the interface naming convention comes in 
handy to identify a case of extension versus implementation. Here's how we can use the 
`IFeedable` interface in defining our `Cat` class.

{{% notice blue "Example" "rocket" %}}

   ```csharp {linenos=table}
      public class Cat : IFeedable
      {

         public void Eat()
         {
            Console.WriteLine("nom nom");
         }

         // ...rest of the class definition...

      }
   ```

{{% /notice %}}

Since we’ve declared that `Cat` implements `IFeedable`, we have to
provide an implementation for the `Eat` method, with the signature as
specified in the interface definition. 

<!-- TODO: Add link to method overriding in inheritance -->

Note the absence of the `virtual` and `override` keywords we used in inheritance. The class is 
*implementing* the interface, rather than extending it so different method rules apply. 

{{% notice blue "Note" "rocket" %}}

   You may both extend a class and implement an interface at the same time.
   Here's an example of how we might define `HouseCat` to extend the class `Cat`,
   as well as an interface `IPetable` that is not already inherited by `Cat`:

   ```csharp {linenos = table}
      public class HouseCat : Cat, IPetable
      {
         // ^^ Note that order matters here. The class being extended 
         // must come before any interfaces being implemented
      }
   ```

{{% /notice %}}

As with classes, interfaces define a type that can be used when
declaring fields and methods. This allows us to make our code more abstract, thus making it 
more extensible and adaptable. If an application is extensible, it is easier for programmers 
for new capabilities to be added later on. For example,
here’s how we might modify our `CatSitter` class:

```csharp {linenos = table}
   public class CatSitter
   {
      public IFeedable Pet { get; set; }

      public CatSitter(IFeedable pet) {
         Pet = pet;
      }

      public void FeedTheCat() {

         // ...code to prepare the cat's meal...

         Pet.Eat();
      }
   }
```

Note that we’ve declared the property `Pet` to be of type
`IFeedable`. This class assumes that the only behavior of `Pet` that
we’ll need within the class is the ability to `Eat`. But if that’s all
we need, then we should relax the requirements on the `Pet` property
as much as possible. In fact, there’s nothing specific about cats in
this class, so we might make our code a step more abstract and flexible
by doing the following:

```csharp {linenos = table}
   public class PetSitter
   {
      public IFeedable Pet { get; set; }

      public PetSitter(IFeedable pet) {
         Pet = pet;
      }

      public void FeedThePet() {

         // ...code to prepare the pet's meal...

         Pet.Eat();
      }
   }

   public class CatSitter : PetSitter
   {
      public CatSitter(IFeedable pet) : base(pet)
      {
         Pet = pet;
      }
      // other Cat-specific behavior
   }
```

We’ve created a `PetSitter` class that encapsulates the behavior for any pet (any 
``IFeedable``, actually), and have `CatSitter` extend `PetSitter`. This allows other 
classes to extend `PetSitter` to make, say, a `DogSitter` that knows how to play fetch
with their pet, or a `HorseSitter` that knows how to go for trail rides with their pet. It
also reduces the dependency of the `FeedThePet` method on the specific
type of pet, since the basic feeding behavior is the same for all types of pets.

Since the base class does not have a no-arg constructor, we must, at minimum, extend the `PetSitter`
constructor in any subclass. Of course, we can always add more constructors to the subclass.

To use this new class design, we can revise the sample code from above
as follows:

```csharp {linenos = table}
   HouseCat suki = new HouseCat("Suki", 12);
   CatSitter annie = new CatSitter(suki);

   annie.FeedThePet();
```

While the code usage here remains unchanged except for changing the
method name from `FeedTheCat` to the more generic `FeedThePet`, the
opportunities for using the classes we’ve built are much wider since the
defined classes are no longer dependent on the specific `Cat` class.
Also notice that we’ve used the object `suki` in a polymorphic way,
creating it as a `HouseCat`, but using it as an `IFeedable` to instantiate a
`CatSitter` object.

As is the case with classes inherited from others, interfaces also enable polymorphic usage of 
objects. We can create an object and then use it in different contexts based on the
interfaces that it implements.

Crucially, *interfaces may not be instantiated*.
You may implement an interface, or declare variables and parameters as
interface types. You cannot, however, create an instance of an
interface.

## Benefits of Using Interfaces

Once you get used to interfaces, you’ll begin to think more abstractly about which 
*behaviors* your code requires rather than which *classes* your code requires. This means
you will start to “code to interfaces” (an OOP principle) instead of
coding to classes, and your code will become more flexible and
extensible.

Here are a few benefits of using interfaces:

1. You can only extend one class, but you may implement many interfaces.
1. You can extend a class and implement an interface at the same time.
1. By declaring variables and parameters as interface types, you make
   your code useful for a much wider variety of situations.
1. When you declare properties and return types to be interface types,
   you decouple code using your classes from the actual class types you
   use. This means that you are free to change the specific
   implementation of your classes without affecting those using them.

You don’t need to start creating interfaces to use their
power! As we cover later in this chapter, there are several interface types provided by 
the C# language spec that you may find handy.

## Check Your Understanding

{{% notice green "Question" "rocket" %}}

   Choose the appropriate option to fill in the blanks.

   A class can extend _______ class(es) and implement ________ interface(s).

   1. one, one
   1. one, more than one
   1. more than one, one
   1. more than one, more than one

{{% /notice %}}

<!-- b, one, more than one -->

{{% notice green "Question" "rocket" %}}

   True or False: An interface in C# must begin with the letter "I".

{{% /notice %}}

<!-- false, while it is convention to name interfaces this way - and Visual Studio strongly encourages it, 
      it is not a breaking requirement. -->
