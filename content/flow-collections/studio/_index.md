---
title: "Studio"
date: 2023-01-25T13:44:27-06:00
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

## Counting Characters

In this studio, you will write a program to count the number of times each character occurs in a string and then print the results to the console

### Getting Started

<!-- TODO: Link to chapter 1 -->
Create your own project from scratch. Review [Creating a C# Project]({{relref ../}}) if you need to.

### Some Items to Ponder Before Coding
1. There are multiple ways to approach this task, but one way involves the following steps:
   1. Loop through the string one character at a time,
   1. Store and/or update the count for a given character using an appropriate data structure.
   1. Loop through the data structure to print the results (one character and its count per line).

1. Which type of data structure (`List`, `Array`, or `Dictionary`) should you use to store character counts? Any of these options would work, but using one of these data structures will optimize your code’s efficiency.

1. You’ll need to initialize the counts for the characters in some fashion. It’s probably better to do this as you go through the string instead of doing so before you loop through it. (WHY?)

<!-- TODO: Link to chapter 2 -->
1. If you need to review how to create a new class, revisit the [Hello Methods](ADD LINK) program.

1. Don’t forget to check out the Bonus Missions below.

{{% notice green "Tip" "rocket" %}} 
Remember, you can turn a string object into an array of characters using:
   ```csharp
   char[] charactersInString = myString.ToCharArray();
   ```
{{% /notice %}}

### Sample Input
Feel free to prompt the user for a string. However, for the sake of simplicity, you might want to start by hard-coding some text and storing it in a variable. For your convenience, here is some [lorem ipsum](https://loremipsum.io/) text:

```
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nunc accumsan sem ut ligula scelerisque sollicitudin. Ut at sagittis augue. Praesent quis rhoncus justo. Aliquam erat volutpat. Donec sit amet suscipit metus, non lobortis massa. Vestibulum augue ex, dapibus ac suscipit vel, volutpat eget massa. Donec nec velit non ligula efficitur luctus.
```
### Sample Output
For the example string above, your output should look something like:
   ```
   L: 1
   o: 15
   r: 9
   e: 26
   m: 11
    : 50  
   i: 27
   p: 7
   s: 29
   u: 28
   d: 4
   l: 17
   t: 29
   a: 22
   ,: 4
   c: 17
   n: 14
   g: 7
   .: 8
   N: 1
   q: 3
   U: 1
   P: 1
   h: 1
   j: 1
   A: 1
   v: 4
   D: 2
   b: 3
   V: 1
   x: 1
   f: 2
   ```

### Bonus Missions
Try these modifications on your code:

   1. Prompt the user to enter the string in the command line.
   1. Make the character counts case-insensitive.
   1. Exclude non-alphabetic characters.

### Super Bonus
Read the string in from a file.

{{% notice blue "Note" "rocket" %}} 
This is a hard one. We won’t talk about reading from files in C# in this course, so be ready for a tough challenge if you accept this mission.
{{% /notice %}}