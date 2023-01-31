---
title: "Testing in C#"
date: 2023-01-25T13:23:58-06:00
draft: false
weight: 1
originalAuthor: Sally Steuterman # to be set by page creator
originalAuthorGitHub: gildedgardenia # to be set by page creator
reviewer: # to be set by the page reviewer
reviewerGitHub: # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

Testing your code is a crucial practice for every developer. 
**Automated testing** ensures that your code works as expected every 
time it runs. Tests also function as internal documentation, giving a 
fellow programmer instructions on how to properly execute your classes 
and methods. While these purposes are the same for C# as any other language, 
the implementation of tests will look a bit different.

This course covers **unit testing** in C# with a test framework called
**MSTest**. Unit testing is based on breaking down the codebase into its 
smallest building blocks, individual statements and methods, and testing 
those building blocks.

{{% notice green "Tip" "rocket" %}}

   If you would like to review the benefits of automated testing, take a peek
   at
   [this section](https://education.launchcode.org/intro-to-professional-web-dev/chapters/unit-testing/why-test.html)
   in another LaunchCode text.

{{% /notice %}}

## Why We Test

### Refactoring

When we **refactor** code, we rewrite it without adding new features. Refactoring can 
increase efficiency at runtime, but it may also mean inadvertently introducing some bugs in the process.
Unit tests verify the most basic functionality of your code, thus safeguarding against 
bugs introduced in refactoring. 

Imagine this common workflow: 

1. You practice **test-driven development (TDD)**, writing your tests to stipulate 
   how your class's code should behave.

1. You write your class's code to pass the tests. 

1. Later, a stakeholder in the project requests that you refactor your code using 
   different syntax.

The features of the application will be the same, but the implementation of those features will change.
Because the changes in implementation do not effect change in the application features, unit tests can 
help with refactoring the codebase. If your tests continue
to pass after the refactor, you can move on, knowing you have not 
inadvertently introduced a bug. Writing tests just once provides innumerable 
benefits for the whole lifetime of the codebase.

### Documentation

In addition to assisting with refactoring, unit tests serve as vital documentation 
for fellow programmers. Again, because unit tests address the most fundamental tasks of your classes,
they serve as live-code use-cases. You may also have an 
external documentation directory with examples of how to run your
project, or perhaps you have been writing comments within your code
to best communicate with your teammates about your changes. Both of
these are great choices and should be done when possible. However, these choices 
also require more forethought to maintain. Each time you update
your code, you might not remember to update the documentation and 
comments. With unit testing, however, you have a more obvious reminder
that a change has been made if a previously-passing test fails.

## Testing Best Practices

Below are some best practices to keep in mind when writing unit tests, in any language.

1. The AAAs

   The AAAs of unit testing refers to the pattern to follow when 
   writing your unit tests. 

   1. Arrange the variables your test requires.
   1. Act on the methods your test requires.
   1. Assert the anticipated comparison of the expected and actual values.

1. Deterministic

   *Every* time a test is run, it should produce the same outcome. 
   A test that passes only most of the time is a worthless test.

1. Relevant

   Group tests by related class and function.

1. Meaningful

   There is no need to test trivial code. For example, unless a getter or setter contains some 
   additional functionality, you do not need to write a test for those methods. 

## Check Your Understanding

{{% notice green "Question" "rocket" %}}

   True or False: Comments are the best tool to make your code readable.

{{% /notice %}}

<!-- False, comments are helpful but can be used in tandem with other forms of documentation, including unit tests. -->

{{% notice green "Question" "rocket" %}}

   Unit tests are a form of:

   1. Manual testing
   1. Automated testing
   1. Integration testing
   1. Documentation testing

{{% /notice %}}

<!-- Automated testing -->