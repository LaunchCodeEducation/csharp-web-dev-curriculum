---
title: "Single Responsibility Principle"
date: 2023-01-23T13:36:52-06:00
draft: false
weight: 6
originalAuthor: Sally Steuterman # to be set by page creator
originalAuthorGitHub: gildedgardenia # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

As we wrap up our whirlwind tour of classes, we want you think a
bit about how to go about building good classes. Doing so is more of an
art than a science, and it will take you lots of practice and time.
However, there are a few rules that we’ve pointed out to help guide you.
Here’s one more.

From
[Wikipedia](https://en.wikipedia.org/wiki/Single_responsibility_principle):

> The **single responsibility principle** states that every module or
> class should have responsibility over a single part of the functionality
> provided by the software, and that responsibility should be entirely
> encapsulated by the class.

It isn’t always clear what “responsibility over a single part of the
functionality” means. However, it is often very clear what it doesn’t
mean. For example, we wouldn’t think of adding functionality to the
`Student` class that tracked all of the data for each of the student’s
classes, such as catalog number, instructor, and so on. Those are
clearly different areas of responsibility. One way to interpret the
single responsibility principle is to say that “classes should be
small.”

As you go forth and create classes, the main thing to keep in mind is
that your skill and judgement in creating C# classes will improve over
time. The best way to improve is to write lots of code, ask lots of
questions, and continue learning.

If you are interested in learning more about the 
Single Responsibility Principle, 
you can check out the entry on [Wikipedia](https://en.wikipedia.org/wiki/Single_responsibility_principle).