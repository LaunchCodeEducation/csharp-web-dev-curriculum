---
title: "Exercises"
date: 2023-01-17T16:28:22-06:00
draft: false
weight: 2
originalAuthor: Sally Steuterman # to be set by page creator
originalAuthorGitHub: gildedgardenia # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

To get started, open up Visual Studio and create a new console program.

{{% notice green "Tip" "rocket" %}}

   If you do not recall how to create a new console program or need a quick refresher to get started, check out the section on [creating a C# project]({{< relref "../../introduction-and-setup/reading/creating-a-project" >}}).

{{% /notice %}}

For each part of the exercises, create a new project in your solution. When you are done, push your solution up to a repository on your Github account!

## Input/Output

1. Write a new "Hello, World" program to prompt the
   user for their name and greet them by name.

   a. Add a question to ask the user:

      ```csharp
         Console.WriteLine("What is your name?");
      ```

   b. Create a variable to store the user's input:

      ```csharp
         string name = Console.ReadLine(); 
      ```

   c. Use concatenation to print the greeting:

      ```csharp
         Console.WriteLine("Hello " + name);
      ```

   d. Run your program.

   {{% expand "Check your solution" %}}

   ```csharp {linenos = table}
      Console.WriteLine("What is your name?");
      string myName = Console.ReadLine();
      Console.WriteLine("Hello " + myName + "!");
   ```

   {{% /expand %}}

## Numeric Types

1. Write a program to calculate the area of a
   rectangle and print the answer to the console. You should prompt the
   user for the dimensions. (What data types should the dimensions be?)

   a. Add a print line to prompt the user for the length of the rectangle.

   {{% expand "Check your solution" %}}

   ```csharp
      Console.WriteLine("What is the length of your rectangle?");
   ```

   {{% /expand %}}

   b. Define a variable to handle the user's response.

   c. Repeat the previous two steps to ask for and store the rectangle's width.

   {{% expand "Check your solution" %}}

   ```csharp
      Console.WriteLine("What is the width of your rectangle?");
      string width = Console.ReadLine();
   ```

   {{% /expand %}}

   d. Use the length and width values to calculate the rectangle's area.

   e. Print a statement using concatenation to communicate to the user what the area of their rectangle is.
   
   {{% expand "Check your solution" %}}

   ```csharp
      Console.WriteLine("The area of the rectangle is: " + area);
   ```

   {{% /expand %}}

   f. Run the program to verify your code.

## More on Numeric Types

1. Write a program that asks a user for the number of
   miles they have driven and the amount of gas they’ve consumed (in
   gallons), and print their miles-per-gallon.

   {{% expand "Check your solution" %}}

   ```csharp {linenos=table}
      Console.WriteLine("How many miles did you drive on your trip?");
      string mi = Console.ReadLine();
      int miles = Int32.Parse(mi);

      Console.WriteLine("How many gallons of gas did you use?");
      string gal = Console.ReadLine();
      int gallons = Int32.Parse(gal);

      int mpg = miles / gallons;
      Console.WriteLine("The MPG for the trip was: " + mpg);
   ```

   {{% /expand %}}

## Strings

1. The first sentence of *Alice’s Adventures in Wonderland*
   is below. Store this sentence in a string, and then prompt the user
   for a term to search for within this string. Print whether or not the
   search term was found. Make the search case-insensitive, so that searching
   for "alice", for example, prints `true`.
      ```
      Alice was beginning to get very tired of sitting by her sister on the
      bank, and of having nothing to do: once or twice she had peeped into the
      book her sister was reading, but it had no pictures or conversations in
      it, 'and what is the use of a book,' thought Alice 'without pictures or
      conversation?'
      ```

   {{% expand "Check your solution" %}}

   ```csharp {linenos=table} 
      string alice = @"Alice was beginning to get very tired of sitting by her sister on the
      bank, and of having nothing to do: once or twice she had peeped into the
      book her sister was reading, but it had no pictures or conversations in
      it, 'and what is the use of a book,' thought Alice 'without pictures or
      conversation?'";
      
      Console.WriteLine(alice);
      Console.WriteLine("What sentence would you like to look for in the sentence above?");
      string searchTerm = Console.ReadLine();
      string compSearchTerm = searchTerm.ToLower();
      string compAlice = alice.ToLower();

      if (compAlice.IndexOf(compSearchTerm, 0) != -1)
      {
         Console.WriteLine("true");
      }
      else 
      {
         Console.WriteLine("false");
      }
   ```

   {{% /expand %}}

1. Extend the previous exercise. Assume the user enters a word that is in the sentence. Print out its index within the string and its length. Next, remove the word from the string and print the sentence again to confirm your code. Remember that strings are *immutable*, so you will need to reassign the old sentence variable or create a new one to store the updated phrase.