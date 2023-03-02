---
title: "Introduction"
date: 2023-02-01T13:10:40-06:00
draft: false
weight: 1
originalAuthor: Sally Steuterman # to be set by page creator
originalAuthorGitHub: gildedgardenia # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

The final pillar of object-oriented programming that we’ll
explore is polymorphism.

## Polymorphism

**Polymorphism** is an object-oriented mechanism that allows for objects
of different types to be used in the same way.

We’ve already encountered polymorphism made possible by [inheritance]({{< relref "../../../inheritance/reading/casting/" >}}) when talking about 
casting with our `Cat` and `HouseCat` classes.
In that case, we stored an object of type `HouseCat` in its compatible type, `Cat`.

Let's take a closer look at how polymorphism might work in our cat-centric application.

{{% notice blue "Example" "rocket" %}}

   Suppose we had a `CatSitter` class like the one below:

   ```csharp {linenos=table}
      public class CatSitter
      {
         public Cat Pet { get; set; }

         public CatSitter(Cat pet) {
            Pet = pet;
         }

         public void FeedTheCat() {

            // ...code to prepare the cat's meal...

            Pet.Eat();
         }
      }
   ```

   The method `FeedTheCat` uses the property `Pet`, which is of type
   `Cat`. Since a `HouseCat` *is a* `Cat` via inheritance, it is
   perfectly acceptable to use an instance of `HouseCat` to fill the
   `Pet` property.

   ```csharp {linenos=table}
      HouseCat suki = new HouseCat("Suki", 12);
      CatSitter annie = new CatSitter(suki);

      annie.FeedTheCat();
   ```

   Similarly, `FeedTheCat` can accept `Tiger` instances as well. This
   is because the only thing that the method requires is that the input
   parameter has the methods defined within `Cat`. Via inheritance,
   both `HouseCat` and `Cat` satisfy this requirement.

In addition to using classes to code in a polymorphic way, we can use *interfaces*.