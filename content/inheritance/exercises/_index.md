---
title: "Exercises: Inheritance"
date: 2023-01-31T15:39:38-06:00
draft: false
weight: 8
originalAuthor: Courtney Frey # to be set by page creator
originalAuthorGitHub: speudusa # to be set by page creator
reviewer: # to be set by the page reviewer
reviewerGitHub: # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

Work on these exercises in a new Visual Studio .NET Core console app. Name your solution `Technology` and make a project inside of it with the same name.

## Class Design

Create three classes inside your solution: `Computer`, `Laptop`, and `SmartPhone`

Before you start coding anything inside these classes, diagram how the three classes are going to be related to each other.  You can start with the diagram below.  Be sure to show how the base class extends each subclass.

{{< mermaid >}}
classDiagram
  Computer -- Smartphone
  Computer -- Laptop
{{< /mermaid >}}

{{% expand "Check your solution" %}}

The Computer class extends Laptop and Smartphone.  

Arrows should point towards Computer class

{{% /expand %}}

Remember to add properties and methods to your diagram.

   1. For a **parent** class: add 3 fields, 2 methods, and a constructor.

   {{% expand "Check your solution" %}}

   The fields and methods selected for these examples can differ from your fields and methods.  

   ```csharp
      public class Computer
      {
         public double Ram { get; set; }
         public double Storage { get; set; }
         public readonly bool hasKeyboard;

         public Computer(double ram, double storage, bool hasKeyboard)
         {
            Ram = ram;
            Storage = storage;
            this.hasKeyboard = hasKeyboard;
         }

         public double IncreaseRam(double extraRam)
         {
            return Ram += extraRam;
         }

         public double IncreaseStorage(double extraStorage)
         {
         return Storage += extraStorage;
         }
      }
   ```

   {{% /expand %}}



   1. For a **child** class: add at least 1 additional field and 1 additional method.

<!-- TODO: show code for Laptop -->

   1. At least one of your fields should be either `static`, `readonly`, or a `const`.

<!-- TODO: show code for Smartphone (or which ever one of the two has any of the reqs above) -->






## Class implementation
Implement your design and add unit tests to a new TechnologyTests MSTest project.

Add a new MSTest project to your solution.
{{% expand "Check your solution" %}}
```csharp
   // one Computer class tests in the Computer Class
   [TestMethod]
   public void TestIncreasingRam()
   {
      Computer testingComputer = new Computer(2, 3, true);
      Assert.AreEqual(2, testingComputer.Ram);
      testingComputer.IncreaseRam(3);
      Assert.AreEqual(5, testingComputer.Ram);
   }
```

{{% /expand %}}


Try to add three MSTests tests per class.
 
{{% expand "Check your solution" %}}

- Testing the `Smartphone` class

```csharp
   //Smartphone Class
   [TestMethod]
   public void TestTakingSelfies()
   {
      SmartPhone testingSmartphone = new SmartPhone(2, 3, true, 800);
      testingSmartphone.TakeSelfie();
      Assert.AreEqual(801, testingSmartphone.NumberOfSelfies);
   }   //Smartphone Class
```

{{% /expand %}}

1. Test
 1. Test



