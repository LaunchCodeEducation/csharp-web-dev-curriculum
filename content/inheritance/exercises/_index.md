---
title: "Exercises: Inheritance"
date: 2023-01-31T15:39:38-06:00
draft: false
weight: 8
originalAuthor: Courtney Frey # to be set by page creator
originalAuthorGitHub: speudusa # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
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

The `Computer` class extends `Laptop` and `Smartphone`.  

Arrows should point towards `Computer` class.

Remember to add properties and methods to your diagram.

{{% /expand %}}

   
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

   {{% expand "Check your solution" %}}

   Here is a possible `Laptop` class.


   ```csharp
   public class Laptop : Computer
   {
      public double Weight { get; set; }

      public Laptop(double ram, double storage, bool hasKeyboard, double weight) : base(ram, storage, hasKeyboard)
      {
      Weight = weight;
      }

      public bool IsClunky()
      {
         if (Weight > 5.0)
         {
            return true;
         }
         else
         {
            return false;
         }
      }
   }
   ```
   {{% /expand %}}


   {{% expand "Check your solution" %}}

   Here is a possible `Smartphone` class.

   ```csharp
   public class SmartPhone : Computer
   {
      public int NumberOfSelfies { get; set; }
      public SmartPhone(int ram, int storage, bool hasKeyboard, int numberOfSelfies) : base(ram, storage, hasKeyboard)
      {
         NumberOfSelfies = numberOfSelfies;
      }
      
      public void TakeSelfie()
      {
         NumberOfSelfies++;
      }
   }
   ```
   {{% /expand %}}


1. At least one of your fields should be either `static`, `readonly`, or a `const`.

   {{% expand "Check your solution" %}}

   ```csharp{linenos=table,hl_lines=[5],linenostart=1} 
   public class Computer
   {
      public double Ram { get; set; }
      public double Storage { get; set; }
      public readonly bool hasKeyboard;

   // code continues
   ```
   {{% /expand %}}

## Class implementation
Implement your design and add unit tests to a new TechnologyTests MSTest project.

1. Add a new MSTest project to your solution.

   {{% expand "Check your solution" %}}
   ```csharp
   // one Computer class tests in the Computer Class
   [TestMethod]
   public void TestIncreasingRam()
   {
      //Arrange
      Computer testingComputer = new Computer(2, 3, true);

      //Act
      testingComputer.IncreaseRam(3);

      //Assert
      Assert.AreEqual(2, testingComputer.Ram);
      Assert.AreEqual(5, testingComputer.Ram);
   }
   ```
   {{% /expand %}}


1. Try to add three MSTests tests per class.
 
   {{% expand "Check your solution" %}}

   - One of the `Smartphone` class tests.  For ideas, verify if your methods work.  Test your fields.  

   ```csharp
   //Smartphone Class
   [TestMethod]
   public void TestTakingSelfies()
   {
      //Arrange
      SmartPhone testingSmartphone = new SmartPhone(2, 3, true, 800);

      //Act
      testingSmartphone.TakeSelfie();

      //Assert
      Assert.AreEqual(801, testingSmartphone.NumberOfSelfies);

      //More tests for the Smartphone Class ...

   }   
   ```

   {{% /expand %}}

## Abstract Class Design

Consider the group of classes that you designed. Suppose you have a web program that uses these classes and you need to assign a unique ID to every object created from them. Each class should have an id field, and no two objects created from any of the classes may have the same value for id.

1. Create an abstract class, `AbstractEntity`, that contains the behavior for assigning and accessing such a unique ID for each class that extends it.
   {{% expand "Check your solution" %}}
   ```CSHARP
   // AbstractEntity Class
   public class AbstractEntity
   {
      public int Id { get; set; }
      private static int nextId = 1;

      public AbstractEntity()
      {
         Id = nextId;
         nextId++;
      }
   }
   ```
   {{% /expand %}}

1. Add this class to your `Technology` project above, and add `AbstractEntity` to the class hierarchy in the correct place.

   {{% expand "Check your solution" %}}
   ```CSHARP
   // AbstractEntity Class
   public class AbstractEntity
   {
      public int Id { get; set; }
      private static int nextId = 1;

      public AbstractEntity()
      {
         Id = nextId;
         nextId++;
      }
   }
   ```
   {{% /expand %}}

   {{% expand "Check your solution" %}}
   
   Update the Computer class. Remember Computer extends AbstractEntity.
   
   ```csharp
   public class Computer : AbstractEntity
   ```
   {{% /expand %}}


   {{% expand "Check your solution" %}}
      
   Testing `AbstractEntity` using MSTest:

   - Testing the `Computer` Class

   ```csharp
   //Computer Class
   [TestMethod]
   public void TestInheritsId()
   {
      //Arrange
      Computer testingComputer = new Computer(2, 3, true);
      Computer testingComputer2 = new Computer(4, 6, true);

      //Assert
      Assert.AreEqual(1, testingComputer.Id);
      Assert.AreEqual(2, testingComputer2.Id);
   }
   ```

   - Testing the `Smartphone` class

   ```csharp
   //Smartphone class
   [TestMethod]
   public void TestInheritingBaseConstructor()
   {
      //Arrange
      SmartPhone testingSmartphone = new SmartPhone(2, 3, true, 800);

      //Assert
      Assert.IsNotNull(testingSmartphone.Id);
      //...
   }
      ```
   {{% /expand %}}