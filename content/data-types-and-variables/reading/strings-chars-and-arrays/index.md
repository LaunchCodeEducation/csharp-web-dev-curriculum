---
title: "Strings, Characters, and Arrays"
date: 2023-01-17T16:28:22-06:00
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

## Strings and Characters

### Immutability

Strings in C# are *immutable*, which means that the characters within a
string cannot be changed.

### Single vs. Double Quotation Marks

C# syntax requires double quotation marks when declaring strings.

C# has another variable type, `char`, which is used for a single character.
`char` uses single quotation marks. The single character can be a letter,
digit, punctuation, or whitespace like tab (`'\t'`).

```csharp
   string staticVariable = "dog";
   char charVariable = 'd';
```

### String Manipulation

The table below summarizes some of the most common string methods available in
C#. For these examples, we use the string variable
`string str = "Rutabaga"`.

| C# Syntax | Description |
|-----------|-------------|
| `str.Substring(3,1)` | Returns the character in 3rd position, (`a`). |
| `str.Substring(2,3)` | Return substring from 2nd to 4th, i.e. substring starting at index 2 and 3 characters long, (`tab`). |
| `str.Length` | Tells us the length of the string, (`8`). |
| `str.IndexOf('a')` | Returns the index for the first occurrence of 'a', (`3`). |
| `str.Split('a')` | Splits the string into sections at each `delimiter` and stores the sections as elements in an array, ({`Rut`, `b`, `g`}). |
| `str + str` | Concatenate two strings together, (`RutabagaRutabaga`). |
| `str.Trim()` | Removes any whitespace at the beginning or end of the string, (`Rutabaga` --- there's not whitespace here). |
| `str.ToUpper(), str.ToLower()` | Changes all alphabetic characters in the string to UPPERCASE or lowercase, respectively,(`RUTABAGA`, `rutabaga`). |

## Arrays

Like a lot of programming languages, C# has multiple ways of storing
ordered data. The most basic type of list in C# is that of the `array`.

An array is an ordered, fixed-size collection of elements. Since C# is
statically typed, arrays may only store one type of object. We can
create an array of integers or an array of strings, but we may not
create an array that holds both integers and strings.

The syntax for creating an array capable of holding 10 integers is:

```csharp
   int[] someInts = new int[10];
```

Note the square brackets next to `int`. This indicates that we want
`someInts` to store a collection of integers instead of a single number.

To create an array of a different size, replace the number `10` in the
brackets with the desired size. To create an array holding a different type,
replace `int` (on both sides of the assignment) with the desired type, like
`double` or `string`.

In addition to the technique above, we can initialize an array using a
literal expression:

```csharp
   int[] someOtherInts = {1, 1, 2, 3, 5, 8};
```

Here, the size is implicit in the number of elements in the literal
expression `{1, 1, 2, 3, 5, 8}`. Also note the use of curly braces `{ }`
instead of square brackets `[ ]`.

To access array elements, we use square brackets and *zero-based indexing*.

```csharp
   int anInt = someOtherInts[4];
   // anInt stores the integer 5.
```

It is important to note that arrays in C# *may not* change size once created. This
turns out to be not very practical, so thankfully C# provides more
flexible ways to store data --- objects that allow us to rearrange, add
to, or remove data --- which we’ll explore in a later lesson.

Aside from using arrays to build some simple loop examples, we’ll only use them in 
special cases. However, they are ubiquitous in C# programming, so it’s good to know 
how they work.

## Check Your Understanding

{{% notice green "Question" "rocket" %}}
   Name the C# method or property responsible for removing whitespace from a string value:
   1. `.Length`
   1. `.Trim()`
   1. `.Split()`
   1. `.Strip()`
{{% /notice %}}

{{% notice green "Question" "rocket" %}}
   Assume that we declare the following C# array:
   ```csharp
      string[] someWords = new string[5];
   ```
   Which of the following shows a correct initialization for the array?
   1. `someWords = {'hello', 'world', '123', 'LaunchCode ROCKS!'}`
   1. `someWords = {"hello", "world", "123", "LaunchCode ROCKS!", "Java"}`
   1. `someWords = {"hello", "world", 'a', "LaunchCode ROCKS!", "Java"}`
   1. `someWords = {"hello", "world", "avocado", "LaunchCode ROCKS!"}`
{{% /notice %}}