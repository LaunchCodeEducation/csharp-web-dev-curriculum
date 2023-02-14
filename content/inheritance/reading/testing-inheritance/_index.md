---
title: "Testing Inheritance"
date: 2023-01-31T15:39:38-06:00
draft: false
weight: 6
originalAuthor: Courtney Frey # to be set by page creator
originalAuthorGitHub: speudusa # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

Not sure you get the whole inheritance idea? Still not sure which fields and methods get inherited and which are overridden? Looking to test your understanding?

<!-- TODO: add 1st Link => Chapter 6 TOC -->

Knowing what we know now about [Unit Testing](LINK) and Inheritance, we can test that our subclasses extend their base classes.

We can add a `CatTests` project to our `Cats` solution and write some code to ensure that `HouseCat` inherits what we expect it to.

```csharp{linenos=table,hl_lines=[],linenostart=1}
[TestMethod]
public void InheritsBaseInFirstConstructor()
{
   HouseCat keyboardCat = new HouseCat("Keyboard Cat", 7);
   Assert.AreEqual(7, keyboardCat.Weight, .001);
}

```

Here, we’re testing that one of our `HouseCat` constructors will call the Cat constructor and appropriately assign the `HouseCat` object’s `weight` field. Remember, we don’t need to write unit tests for getters or setters unless they do something extra in addition to getting or setting the field. The purpose of this test, though, is less to test getting `keyboardCat.Weight` and more to validate that the subclass constructor has inherited the base class constructor.

It’s a good practice to test your subclasses to verify the items that they inherit or override.

## Check Your Understanding


{{% notice green  "Question" "rocket" %}} 
Fill in the blank to test that the no-argument constructor of Cat is called when the second constructor on HouseCat is used?

Second HouseCat constructor:
```csharp{linenos=table,hl_lines=[],linenostart=14}
public HouseCat(string name)
{
   Name = name;
}
```
```csharp{linenos=table,hl_lines=[],linenostart=1}
[TestMethod]
public void InheritsDefaultCatInSecondConstructor()
{
   HouseCat keyboardCat = new HouseCat("Keyboard Cat");
   // <insert assertion method here>
}
```

   1. `Assert.AreEqual(13, keyboardCat.Weight);`
   1. `Assert.IsNotNull(keyboardCat.Weight);`
   1. `Assert.AreEqual(13, keyboardCat.Weight, .001);`
   1. `Assert.IsNotNull(keyboardCat.weight);`

<!-- ans:  ``Assert.AreEqual(13, keyboardCat.Weight, .001);``    -->
{{% /notice %}}


{{% notice green  "Question" "rocket" %}} 

What additional assert method can we add to this test to properly verify that `HouseCat` inherits `Eat()`?

```csharp{linenos=table,hl_lines=[],linenostart=1}
[TestMethod]
public void IsNotInitiallyTired()
{
   HouseCat keyboardCat = new HouseCat("Keyboard Cat");
   Assert.IsFalse(keyboardCat.Hungry);
   Assert.IsFalse(keyboardCat.Tired);
   keyboardCat.Eat();
}
```

1. `Assert.IsFalse(keyboardCat.Tired);`
1. `Assert.IsTrue(keyboardCat.Tired);`
1. `Assert.IsTrue(keyboardCat.Hungry);`
1. `Assert.IsFalse(keyboardCat.tired);`

<!-- ans: `Assert.IsTrue(keyboardCat.Tired);` -->
{{% /notice %}}
