---
title: "Inheritance in C#"
date: 2023-01-31T15:39:38-06:00
draft: false
weight: 2
originalAuthor: Courtney Frey # to be set by page creator
originalAuthorGitHub: speudusa # to be set by page creator
reviewer: # to be set by the page reviewer
reviewerGitHub: # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

Let’s examine an inheritance relationship between two classes: `Cat` and `HouseCat`. `HouseCat` is a class that inherits from Cat, so `HouseCat` receives the data and behaviors of Cat. These inherited traits are things like fields, properties, and methods. Any fields and non-constructor methods in Cat are available to each instance of `HouseCat`.

When we speak about an inheritance relationship, we say that a `HouseCat` is a `Cat`, or **extends** `Cat`. In order to define a class that inherits from another, we use the : syntax.