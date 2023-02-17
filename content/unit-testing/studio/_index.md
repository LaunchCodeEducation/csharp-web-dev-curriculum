---
title: "Studio"
date: 2023-01-25T13:23:58-06:00
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

For this studio, you will be writing unit tests to help you find 
errors in the `BalancedBrackets.cs` file in the starter code.

Discuss with your fellow students and TA how the given class should behave.
What are some examples of input? What would the desired output be for each input?

## Getting Started

1. Fork and clone the [studio repository](https://github.com/LaunchCodeEducation/csharp-web-dev-unittesting-studio).
1. In Visual Studio, check out your repository.
1. Write unit tests to find the errors in `BalancedBrackets.cs`.
   
   1. The tests you write should guide how you revise the sourcecode. Use TDD to 
      first write tests that will work for the desired behavior of `BalancedBrackets`.
      When your tests fail, correct the class to pass your tests.
   1. The content of your tests is up to you, but you should write at least 12 tests.

{{% notice green "Tip" "rocket" %}}

   Here's a first test to help get you started. Assert that brackets in the correct order, `"[]"`, return true.

   ```csharp
      [TestMethod]
      public void OnlyBracketsReturnsTrue() {
         Assert.IsTrue(BalancedBrackets.HasBalancedBrackets("[]"));
      }
   ```

{{% /notice %}}

{{% notice blue "Note" "rocket" %}}

   `BalancedBrackets` is essentially a wrapper class for a method. And 
   because it's only method is static, we don't need to create an instance
   to test `HasBalancedBrackets()`.

{{% /notice %}}

## Uploading Your Work

Push up your work to save your solution in your remote repository.