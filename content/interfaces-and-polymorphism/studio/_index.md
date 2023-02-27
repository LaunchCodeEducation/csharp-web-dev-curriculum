---
title: "Studio: Spinning Discs"
date: 2023-02-01T13:10:40-06:00
draft: false
weight: 3
originalAuthor: Sally Steuterman # to be set by page creator
originalAuthorGitHub: gildedgardenia # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

Although they look the same, the old optical discs---CDs and DVDs---are quite
different from each other. Let's use them as the focus for creating a new
interface.

## Getting Ready

Set up a local copy of the project:

1. Visit the [repository page](https://github.com/LaunchCodeEducation/SpinningDiscs-Studio) for this project and fork it to create a copy under your own GitHub account.
1. Open up the solution in Visual Studio to get started.

## Disc Project Overview

In this activity, you will pair up to design a new custom interface and an abstract class.

Take a look at the prepared `CD` and `DVD` classes in the starter
code. Neither class contains members and methods. You will add these by
extending a base class and implementing your interface. Before you do this,
however, you need to consider what code to place in the interface vs. the
abstract class vs. each specific class.

Just like you did with your [Restaurant Menu studios]({{< relref "../../classes/studio" >}}), you will begin with pen
and paper (or similar tools).

## Consider Generic Behaviors

Here are a few behaviors that both CDs and DVDs share:

1. They both spin.
1. They both store data.
1. Data gets written to the discs by using a laser.
1. The data on the discs can be read by using a laser.
1. Once loaded, they both report information like name, capacity, contents, and
   disc type.

With your partner, add one or two more behaviors to the list. Feel free to
do some quick research online if needed. Note that information like storage
capacity does NOT belong on this list, since it describes a *property* rather than a *behavior*.

For each behavior, identify if it depends on any type of instance variable.
For example, the spinning behavior does not require any field information
from the `CD` or `DVD` classes.

This collecting and sorting of behaviors is the first step toward designing
your interface and abstract class. It prompts you to consider behaviors that
can be generally applied vs. those that depend on data stored in a specific
object.

## Consider Class-Specific Behavior and Data

Next, you and your partner need to decide which behaviors go into the
interface vs. an abstract class.

Behaviors added to an interface do NOT have to be identical for every object
that implements the interface. The key is that the methods require no
object-specific data. The methods can accept parameters, but these should
represent generic values like a search term rather than field data
like the title of a DVD.

For example, even though CDs and DVDs both spin, they do so at different
speeds. Their behavior (spinning) is the same, but the details of that
behavior vary. Thus, a method like `SpinDisc()` fits well into an interface.

1. For the other behaviors you and your partner sorted, decide which ones
   belong in the interface.
1. Write down details about how these behaviors differ for CDs and DVDs. This
   guides your thinking about how each class should implement the methods.
1. For the behaviors that cannot go into the interface, decide if they could be
   placed in an abstract class or if they need to appear in the separate `CD`
   and `DVD` classes.
1. Finally, write down the fields and properties needed to define the properties of a CD or
   DVD (e.g. `StorageCapacity`). Consider:

   1. Which members are shared by both types of discs, and which ones are
      unique to each class?
   1. Do any of the members represent *constants*?

## Code the Interface

Now that your team has completed the before-coding thinking, it's time to
start building!

1. Add an `IOpticalDisc` file for the interface. Refer back to
   [creating an interface]({{< relref "../reading/interfaces/#creating-an-interface" >}}) if you need a quick
   review of the syntax.
1. Declare and initialize any constants.
1. Add a method signature for each of the behaviors you identified for the
   interface. For example:

   ```csharp
      void SpinDisc();
   ```

Good work. Now you need to step back from the interface for a moment and take
care of the remaining methods and fields.

## Code the Abstract Class

To streamline the field and constructor code for `CD` and `DVD`, you
need to start with a base class.

1. Create an abstract `BaseDisc` class and declare the fields used by both
   `CD` and `DVD`.
1. Code the shared constructors and required methods.

OK. Now put your code to work.

## Complete the Disc Classes

1. Extend the base class into the `CD` and `DVD` classes.
1. Implement the interface in each class.
1. Fill in the code for each of the interface methods.
1. Add any other necessary methods needed by each class.

## Add Method Calls to `Main`

In the `Main` method, declare and initialize a `CD` and `DVD` object,
then run each of the behaviors you and your partner identified.

{{% notice blue "Example" "rocket" %}}

   ```csharp {linenos = table}
      myCd.SpinDisc();
      myDvd.SpinDisc();
   ```

   **Output**

   ```console
      A CD spins at a rate of 200 - 500 rpm.
      A DVD spins at a rate of 570 - 1600 rpm.
   ```

{{% /notice %}}

## Bonus Missions: Other Discs & Disks?

1. CDs and DVDs are not the only flat, circular media that have been used to
   store and return data.

   1. Add classes for vinyl records (LPs) and floppy disks.
   1. Does your interface apply to all four classes? If so, implement the
      interface and its methods in the LP and floppy classes.
   1. If your interface does NOT apply to all of the classes, modify it to do so.
      (Note: At the very least, you need to rename the interface).
   1. Does your abstract class apply to LPs and floppy disks? If so, extend it
      into the new classes. If not, should you modify it or extend a
      *different* abstract class?

1. What about wheels and Frisbees? These are also spinning disks, but they are
   not used for data storage.

   1. Abstract class or interface? Which one can be applied to the `Wheel`
      and `Frisbee` classes?
   1. Discuss these questions with your peers, then code one of the classes
      just for fun.