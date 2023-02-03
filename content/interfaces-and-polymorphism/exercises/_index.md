---
title: "Exercises"
date: 2023-02-01T13:10:40-06:00
draft: false
weight: 2
originalAuthor: Sally Steuterman # to be set by page creator
originalAuthorGitHub: gildedgardenia # to be set by page creator
reviewer: # to be set by the page reviewer
reviewerGitHub: # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

As a new C# coder, it might take you some time to recognize when to use interfaces.

To help overcome this, let's consider a common occurrence---sorting a
`List` of objects.

<!-- TODO: Add link to section on list sorting -->

1. If the list contains `string` or numerical entries, then sorting the list
   is trivial:

   ```csharp
      listName.Sort();
   ```

1. However, if the elements are custom objects (like `Cat`), then sorting the
   list becomes more complicated. This is because the objects may contain
   multiple fields, any of which could be used as a sorting option. For
   `Cat` objects, this could include `name`, `age`, or `mass`.

## Getting Started

Open up your exercises starter code repo in Visual Studio to get started!

You will practice implementing interfaces by playing around with a small ice
cream store. It consists of a refrigerated display `Case`, which contains
a collection of ice cream `Flavor` objects and a selection of `Cone`
objects.

{{% notice green "Tip" "rocket" %}}

   Did you notice the abstract `Ingredient` class? This gets extended by
   `Flavor` and `Cone` to help streamline the code.

{{% /notice %}}

## Sorting Flavors by Name

To display a menu for your customers, you need to sort the ice cream flavors
alphabetically by the `name` field. Fortunately, the `IComparer`
interface helps you solve the sorting-objects-by-field problem.

{{% notice green "Tip" "rocket" %}}

   Before proceeding, make sure you have read the section on the [IComparer interface]({{< relref "../reading/given-interfaces/#icomparert" >}})!

{{% /notice %}}

### Create a Sorting Class

1. Create a new class called `FlavorComparer` and have it implement the
   `IComparer` interface:

   ```csharp
      public class FlavorComparer : IComparer<Flavor>
   ```

1. To start sorting, we need a `Compare()` method. Add the following code to create one:

   ```csharp {linenos = table}
      public int Compare(Flavor x, Flavor y)
      {
         return string.Compare(x.Name, y.Name);
      }
   ```

   This returns an integer (-1, 1, or 0) depending on
   which `Flavor` object `x` or `y` comes first, alphabetically.

### Sorting the `Flavors` List

In `Program.cs`, we declare `menu` that contains everything in the `Case`
as well as specific `availableFlavors` and `availableCones` collections.

```csharp {linenos=table, linenostart=10}
   Case menu = new Case();
   List<Flavor> availableFlavors = menu.Flavors;
   List<Cone> availableCones = menu.Cones;
```

1. To sort the `availableFlavors` list, first create a new `FlavorComparer`
   object.

   ```csharp {linenos=table, linenostart = 13}
      FlavorComparer comparer = new FlavorComparer();
   ```

1. Next, call the `Sort` method on `availableFlavors` and pass the `comparer`
   object as the argument.

   ```csharp {linenos = table, linenostart = 15}
      availableFlavors.Sort(comparer);
   ```

1. Iterating through the `availableFlavors` list with a loop before and after the sort shows
   the results. (The output below displays just the `name` fields).

   ```console
      Before:                 After:

      Vanilla                 Chocolate
      Chocolate               Red Velvet
      Red Velvet              Rocky Road
      Rocky Road              Strawberry Sorbet
      Strawberry Sorbet       Vanilla
   ```

{{% notice green "Tip" "rocket" %}}

   Instead of declaring and initializing the `comparer` object, we could
   combine steps 1 and 2 by using a single statement:

   ```csharp
      availableFlavors.Sort(new FlavorComparer());
   ```

{{% /notice %}}

## Sorting Cones by Cost

Now let's sort our `availableCones` list by cost, from least expensive to most
expensive.

1. Create the new class `ConeComparer`.

1. Follow the example above to implement the `IComparer` interface and
   evaluate `Cone` objects by cost.
   Since comparing two numbers is different from comparing strings, try getting the difference between the two numbers. If the difference is positive, then we know the first number is greater. If the difference is negative, then we know that the second number is greater.

   {{% expand "Check your solution" %}}

   ```csharp {linenos=table}
      public class ConeComparer : IComparer<Cone>
      {
         public ConeComparer()
         {
         }

         public int Compare(Cone x, Cone y)
         {
            double diff = x.Cost - y.Cost;
            if(diff == 0)
            {
               return 0;
            }
            else if (diff < 0)
            {
               return -1;
            }
            else
            {
               return 1;
            }
         }
      }
   ```

   {{% /expand %}}

1. In the `Main()` method, sort the `availableCones` list, then print the elements to the screen
   to verify the results.

   ```console
      Before:           After:

      Waffle: $1.25        Bowl: $0.05
      Sugar: $0.75         Wafer: $0.50
      Wafer: $0.50         Sugar: $0.75
      Bowl: $0.05          Waffle: $1.25
   ```

   {{% expand "Check your solution" %}}

   ```csharp {linenos=table}
      ConeComparer compareCones = new ConeComparer();
   availableCones.Sort(compareCones);
   foreach (Cone c in availableCones)
   {
      Console.WriteLine(c);
   }
   ```

   {{% /expand %}}

{{% notice green "Tip" "rocket" %}}

   Remember that the `cost` field is of type `double` and `Compare()` has a return type of type `int`!

{{% /notice %}}

## Bonus Mission

Modify `FlavorComparer` to sort `Flavor` objects by the number of allergens, from lowest to highest.

## Next Steps

In these exercises, you practiced implementing existing interfaces. In the
studio activity, you will design and implement your own.