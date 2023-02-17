---
title: "Exercises"
date: 2023-01-25T13:44:27-06:00
draft: false
weight: 7
originalAuthor: Courtney Frey # to be set by page creator
originalAuthorGitHub: speudusa # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

## Control Flow and Collections

You will be working in the [csharp-web-dev-exercises](https://github.com/LaunchCodeEducation/csharp-web-dev-exercises) repository.  Each section will provide you with the project you will need. 

## Array Practice
Using the `Arrays` project in the Exercises repo complete the following:

1. Create and initialize an array with the following values in a single line:

   ```
   1, 1, 2, 3, 5, 8
   ```

1. Loop through the array and print out each value.

   {{% expand "Check your solution" %}} 

   ```csharp
   foreach(int num in numberArray)
      {
         Console.WriteLine(num);
      }
   ```

   Remember: this is not the only way to loop through an array.

   {{% /expand %}}

1. Modify the loop to only print the odd numbers from the array.


### String Practice
Using the `Strings` project in the Exercises repo complete the following:

1. For this exercise, create a string for the value:

   ```
   I would not, could not, in a box. I would not, could not with a fox.
   I will not eat them in a house. I will not eat them with a mouse.
   ```

1. Use the Split method to divide the string at each space and store the individual words in an array. If you need to review the method syntax, look back at the string methods table.
 
1. Print the array of words to verify that your code works. The syntax is:

   ```csharp
   Console.WriteLine(string.Join(",", arrayName));
   ```

   {{% expand "Check your solution" %}}
   ```csharp
   string sentence = "I would not, could not, in a box. I would not, could not with a fox. I will not eat them in a house. I will not eat them with a mouse.";
   
   string[] words = sentence.Split(" ");
   
   Console.WriteLine(string.Join(",", words));
   ```
   {{% /expand %}}  

1. Repeat steps 2 and 3, but change the delimiter to split the string into separate sentences.




### List Practice
Using the `Lists` project in the Exercises repo complete the following:

1. Write a static method to find the sum of all the even numbers in a `List`.

   {{% expand "Check your solution" %}}

   ```csharp
   static int sumEven(List<int> arr)
   {
      int total = 0;
      foreach (int integer in arr)
      {
         if (integer % 2 == 0)
         {
            total += integer;
         }
      }
      return total;
   }
   ``` 
   {{% /expand %}}

1. Create a list with at least 10 integers and call your method on the list.

1. Write a `static` method to print out each word in a list that has exactly 5 letters.

   {{% expand "Check your solution" %}}
   ```csharp
   static void printFiveLetterWords(List<string> wordlist)
   {
      foreach (string word in wordlist)
      {
         if (word.Length == 5)
         {
            Console.WriteLine(word);
         }
      }
   }
   ``` 
   {{% /expand %}}

1. Modify your code to prompt the user to enter the word length for the search.

   {{% expand "Check your solution" %}}
   ```csharp
      Console.WriteLine("Enter a word length: ");
      string numInput = Console.ReadLine();
      int numChars = int.Parse(numInput);

      // Call the method to print out list words of the chosen length:
      printXLetterWords(wordList, numChars);


      static void printXLetterWords(List<string> wordlist, int length)
      {
         foreach (string word in wordlist)
         {
            if (word.Length == length)
            {
               Console.WriteLine(word);
            }
         }
      }
   ```
   {{% /expand %}}

## Dictionary Practice
Using the `Dictionaries` project in the Exercises repo complete the following:

1. Make a program similar to `GradebookDictionary` that does the following:
   
   1. It takes in student names and ID numbers (as integers) instead of names and grades.
   {{% expand "Check your solution" %}}
   ```csharp
   Console.WriteLine("Enter your students' names and ID numbers (or ENTER to finish):");

   Console.WriteLine("Student Name: ");
   newStudent = Console.ReadLine();

   if (newStudent!= "")
   {
      Console.WriteLine("ID: ");
      int newID = int.Parse(Console.ReadLine());
      students.Add(newID, newStudent);
   }
   ```
   {{% /expand %}}

   1. The keys should be the IDs and the values should be the names.
   {{% expand "Check your solution" %}}
   ```csharp
   Console.WriteLine("\nClass roster:");

   foreach (KeyValuePair<int, string> student in students)
   {
      Console.WriteLine(student.Value + "'s ID: " + student.Key);
   }

   Console.WriteLine("Number of students in roster: " + students.Count);
   ```
   Review the `Array` and `List` Gradebooks to see how they used loops
   {{% /expand %}}

   1. Modify the roster printing code accordingly.

### Bonus Mission
Update your solution from the **List Practice** section above to use the string from the **String Practice** section. Search *“C# convert string to list”* online to see how to split a string into the more flexible `List` collection.