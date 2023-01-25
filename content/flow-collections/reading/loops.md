---
title: "Loops"
date: 2023-01-25T13:44:27-06:00
draft: false
weight: 2
originalAuthor: Courtney # to be set by page creator
originalAuthorGitHub: <no value> # to be set by page creator
reviewer: # to be set by the page reviewer
reviewerGitHub: # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

## `for` Loop

In C#, we write a **definite** loop (aka a `for` loop) as:

```csharp
for (int i = 0; i < 10; i++ ) {
   Console.WriteLine(i);
}
```
**Output:**
```
0
1
2
3
4
5
6
7
8
9
```

The C# `for` loop gives you explicit control over the starting, stopping, and stepping of the loop variable inside the parentheses. You can think of it this way:

```csharp
for (start clause; stop clause; step clause) {
   statement1
   statement2
   ...
}
```

If you want to start at 100, stop at 0 and count backward by 5, the loop is written as:

```csharp
for (int i = 100; i >= 0; i -= 5) {
   Console.WriteLine(i);
}
```

**Output:**

```
100
95
90
... //countdown continues 
```

## `foreach` Loop
C# also provides a syntax to iterate over any sequence or collection, such as an array:

```csharp
int[] nums = {1, 1, 2, 3, 5, 8, 13, 21};

foreach (int i in nums) {
   Console.WriteLine(i);
}
```
Here, the loop variable moves through the items in the array of integers, `nums`. The syntax here uses the word, in. This type of loop is known as a **foreach loop**.

{{% notice green "Tip" "rocket" %}} 
   When considering this structure, it can be helpful to read the code sample above to yourself as “For each integer in array `nums`…”.
{{% /notice %}}

This loop version also works with a string, where we can convert the string to an array of characters:

```csharp
string msg = "Hello World";

foreach (char c in msg.ToCharArray()) {
   Console.WriteLine(c);
}
```

As you see, to iterate through a string in this way, C# requires an extra string method, `.ToCharArray()`, to convert the string to an array of characters.

## `while` Loop
C# also supports the while loop, or indefinite loop. A while loop in C#:

```csharp
int i = 0;
while (i < 3) {
   i++;
}
```

## `do-while` Loop
C# adds an additional, if seldom used, variation of the while loop called the `do-while` loop. The `do-while` loop is very similar to `while`, except that the condition is evaluated at the end of the loop rather than the beginning. This ensures that a loop will be executed at least one time. In some situations, the `do-while` loop is preferable, because it avoids an additional assignment prior to the loop.

For example:
```csharp
do {
   Console.WriteLine("Hello, World");
} while (false);
```

**Output:**

```
Hello, World
```
Above, the message prints despite the condition never being met.

## Break Statements in Loops
There are instances where you may want to terminate a loop if a given condition is met. In these instances, the `break` statement comes in handy. For example, say you want to loop through an array of integers to search for a given value. Once that number is found, you want to quit the loop. You can do the following:

```csharp
int[] someInts = {1, 10, 2, 3, 5, 8, 10};
int searchTerm = 10;
foreach (int oneInt in someInts) {
   if (oneInt == searchTerm) {
      Console.WriteLine("Found it!");
      break;
   }
}
```

In the code above, instead of the `for` loop iterating through all the integers in the array, it will stop after it finds the first matching instance. So once it finds the first `10` in the array, it prints `“Found it!”` and then terminates the loop. If the `break` statement weren’t there, the loop would continue and when it found the second `10`, it would print “Found it!” a second time.

Note that the `break` statement terminates the innermost loop that it is contained within. So if you have nested loops and use a `break` statement within the innermost loop, then it will only terminate that loop and not the outer one. If a `break` is present in the outer loop, it — and any other block nested within it — is terminated when the `break` runs.

## `continue` Statements in Loops
The `continue` statement is similar to, but importantly different from, the break statement. Like `break`, it interrupts the normal flow of control of the loop. But unlike `break`, the `continue` statement only terminates the current iteration of the loop. So the loop will continue to run from the top after a continue statement. Here is an example:

```csharp
int[] someInts = {1, 10, 2, 3, 5, 8, 10};
int searchTerm = 10;
foreach (int oneInt in someInts) {
   if (oneInt == searchTerm) {
      Console.WriteLine("Found it!");
      continue;
   }
   Console.WriteLine("Not here");
}
```

The above program will print `“Not here”` on every iteration of the for loop except where the number has been found. So the output looks like this:

```
Not here
Found it!
Not here
Not here
Not here
Not here
Found it!
```

Because of the `continue` statement, the final print statement in the for loop is skipped. If the `continue` statement weren’t there, the output would look like this instead (notice the extra “Not here” printouts):

```
Not here
Found it!
Not here
Not here
Not here
Not here
Not here
Found it!
Not here
```

## Concatenating Strings in Loops
A use case of loops may be to concatenate strings. For example, if we have an array of strings containing each word in a sentence, we may want to concatenate each value in the array to reform our sentence.

```csharp
string[] arrayOfWords = {"Books", "Cheese", "Trees", "Laughter"};

string finalSentence = "";

foreach (string word in arrayOfWords) {
   finalSentence += word;
}
```

This code would work well for this situation. However, because strings are immutable, when the value of `word` is appended onto `finalSentence`, a new string object is created. This means that the longer `arrayOfWords` is, the more intensive and inefficient the code becomes. We can accomplish the same thing with the `StringBuilder` class. `StringBuilder` objects are mutable strings of characters and the documentation contains a full list of important properties and methods.

If we wanted to use a `StringBuilder` object instead of a simple string in the above code, we would modify it like so:

```csharp
StringBuilder finalSentence = new StringBuilder();

foreach (string word in arrayOfWords) {
   finalSentence.Append(word);
}
```

First, we need to initialize a new `StringBuilder` object, `finalSentence`, with new `StringBuilder()`. The `Append()` method in the `StringBuilder` class adds the value of `word` to the end of the `finalSentence` object.

While concatenating strings is just one of the many use cases of loops in C#, `StringBuilder` is a fun tool to add to your toolkit. If we don’t use a `StringBuilder` object, the longer `arrayOfWords` is, the slower our program will get. While at this level, we may not be too concerned with a program’s performance, in enterprise applications, performance can be everything.

## Check Your Understanding

{{% notice green "Question" "rocket" %}} 

```csharp
char[] chars = {'p', 'l', 'r', 's', 't'};

for (<loop-statement>) {
   Console.WriteLine(i);
}
```

What does the missing <loop-statement> need to be to print each item in `chars`?

   1. `char i : chars`
   1. `char i : chars[]`
   1. `char i in chars`
   1. `char i in chars[]`

<!-- ans: ``char i in chars`` -->
{{% /notice %}}

{{% notice green "Question" "rocket" %}} 

```csharp
do {
   Console.WriteLine("Hello world!");
} while (3 < 2);
```

How many times does the message print and why?

   1. 0 — The `while` condition is never true.
   1. 1 — The print statement is evaluated before the conditional.
   1. Infinite times — 3 is less than 2, and the condition is never changed in the loop.

<!-- ans: 1 --- The print statement is evaluated before the conditional. -->
{{% /notice %}}

