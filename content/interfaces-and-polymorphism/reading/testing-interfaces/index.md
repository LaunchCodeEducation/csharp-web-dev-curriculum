---
title: "Unit Testing and Interfaces"
date: 2023-02-01T13:10:40-06:00
draft: false
weight: 5
originalAuthor: Sally Steuterman # to be set by page creator
originalAuthorGitHub: gildedgardenia # to be set by page creator
reviewer: # to be set by the page reviewer
reviewerGitHub: # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

After all that we have learned about interfaces, perhaps you are wondering, *how do I write my unit tests with interfaces?*

<!-- TODO: Add link back to testing inheritance -->

The best practices to testing interfaces are very similar to those of testing inheritance. You want to focus on testing the contract 
that the interface is supposed to be upholding as opposed to the interface itself.

{{% notice blue "Example" "rocket" %}}

   We have an `IFeedable` interface and a `HouseCat` class.

   ```csharp {linenos=table}
      public interface IFeedable
      {
         string Eat()
         {
            return "the feedable is eating";
         }
      }

      public class HouseCat : IFeedable
      {
         public string Name { get; set; }
         public HouseCat(string name)
         {
            Name = name;
         }
      }
   ```

   Based on the class above and the interface it implements, we should expect that a call to `.Eat()` on an instance of 
   a `HouseCat` will return the default implementation.

   ```csharp {linenos = table}
      [TestClass]
      public class CatTests
      {
         [TestMethod]
         public void TestHouseCatImplementsEatMethod()
         {
            IFeedable test_cat = new HouseCat("test");
            Assert.AreEqual("the feedable is eating", test_cat.Eat()); 
            // This test passes. Don't believe us? Try it yourself!
         }
      }
   ```

   In this situation, we test the contract that the interface is supposed to be upholding, but not the interface itself.
   While there are strategies to test interface code itself using *mock objects*, we won't approach those tactics in this course. 

{{% /notice %}}

## Check Your Understanding

{{% notice green "Question" "rocket" %}}

   A class ``PetDog`` also implements ``IFeedable`` and contains its own ``Eat()`` method. Should we test that method's results?

   1. No, the interface contract will not be tested in this scenario.
   1. Yes, testing the class's custom methods is always a worthy endeavor.

{{% /notice %}}
   
<!-- b, testing the class's custom methods is always a worthy endeavor. -->