---
title: "Interfaces and Abstract Classes"
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

We mentioned previously that interfaces share some characteristics with
abstract classes. Recall that an abstract class is one declared with the
`abstract` keyword. You may not create an object from an abstract
class and, like an interface, an abstract class is allowed to contain
methods that only have signatures (that is, methods that don’t have
implementation code).

The main differences between interfaces and abstract classes are:

1. You *implement* an interface, while you *extend* an abstract class. The net effect of this is 
   that a class may implement interfaces while also extending a class. Note that while you can 
   implement *more than one* interface, you can only extend *one* class.
1. Abstract classes may contain non-constant fields, while interfaces can only contain constant 
   fields.
1. Abstract classes should be used to collect and specify behavior by *related* classes, while an 
   interface should be used to specify related behaviors that may be common across *unrelated* 
   classes.

   {{% notice blue "Example" "rocket" %}}

   Think about our `IFeedable` interface. If we want to 
   add a `Dog` class to our application, we might implement the `IFeedable` interface for our 
   `Dog` class. This makes sense as dogs are creatures that we feed. However, as dogs and cats are so 
   different, it is unlikely that they would share many characteristics through a `Pet` class.

   {{% /notice %}}

## Check Your Understanding

{{% notice green "Question" "rocket" %}}

   Check all statements that are TRUE about the differences between interfaces and abstract classes.

   1. You extend an abstract class, but implement an interface.
   1. You can implement many interfaces and many classes.
   1. Interfaces cannot contain non-constant fields, but abstract classes can.
   1. Methods that use instance properties can be in both interfaces and abstract classes.

{{% /notice %}}

<!-- a,c. You extend an abstract class, but implement an interface. and Interfaces cannot contain non-constant fields, but abstract classes can. -->