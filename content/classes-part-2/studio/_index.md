---
title: "Studio: Restaurant Menu Continued "
date: 2023-01-30T09:32:46-06:00
draft: false
weight: 3
originalAuthor: Courtney Frey # to be set by page creator
originalAuthorGitHub: speudusa # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

We began designing and implementing our `Menu` and `MenuItem` classes in the [last studio]({{< relref "../../../classes/studio/_index.md" >}}). Let’s continue working on these classes by adding some methods.

## Design

To review, here are the details you have from the restaurant owner:

   1. The menu consists of several menu items.
   1. Each menu item has a price, description, and category (appetizer, main course, or dessert).
   1. It should be possible to display whether or not a menu item is new.
   1. The app should know when the menu was last updated, so visitors can see that the restaurant is constantly changing and adding exciting new items.

Based on these details, you need to include some *instance* methods:

   1. A way to add and remove menu items from the menu.
   1. A way to tell if a menu item is new.
   1. A way to tell when the menu was last updated.
   1. A way to print out both a single menu item as well as the entire menu.
   1. A way to determine whether or not two menu items are equal.

Starting with pen and paper (or your favorite notes application on your laptop), sketch out the methods that you need to add to these classes. List the method names and access levels, along with the types of all input and return parameters. Also, consider whether any methods should be `static`.

## Share Your Design

Once you have sketched out your methods, pair with a classmate and take turns presenting your designs. Class design can be subjective, so it’s important to properly think and talk through your choices before coding.

While your partner is presenting their design, ask questions about why they made the decisions they did. Consider other use cases that might come up, and see if their design fits with those.

## Implementation

1. In Visual Studio, open your `RestaurantMenu` project. Create a branch in your repository for your Lesson 4 Studio solution. For the studio, make sure all of your work is in that branch.
1. Within the project, add the methods you designed to your `Menu` and `MenuItem` classes.
1. Test your classes inside `Program.cs`:
   1. Create several items and add them to a menu.
   1. Print the entire, updated menu to the screen.
   1. Print an individual menu item to the screen.
   1. Delete an item from a menu, then reprint the menu.

## Commit Your Work

In the previous studio, you should have created a repository on GitHub for your restaurant project. Since you just modified that project in this studio, commit your changes and push them up to the same repository.

## Bonus Mission

If a user tries to add an item that is already on the menu, print a message that warns the user about the duplicate. Also, prevent the duplicate from being added to the menu.
