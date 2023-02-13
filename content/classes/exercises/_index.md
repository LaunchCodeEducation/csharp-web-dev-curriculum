---
title: "Exercises"
date: 2023-01-23T13:36:52-06:00
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

Before you get started, make sure you have forked and cloned the [starter code](https://github.com/LaunchCodeEducation/csharp-web-dev-exercises) repository for the exercises.
We will be focusing on the project named `Classes`.

1. Open up the file, `Student.cs`, and update the starter code to make use of auto-implemented properties.

   {{% expand "Check Your Solution" %}}

   ```csharp {linenos=table}
      public class Student
      {
         private static int nextStudentId = 1;
         public string Name { get; set; }
         public int StudentId { get; set; }
         public int NumberOfCredits { get; set; } = 0;
         public double Gpa { get; set; } = 0.0;
         
         public Student(string name, int studentId, int numberOfCredits, double gpa)
         {
            Name = name;
            StudentId = studentId;
            NumberOfCredits = numberOfCredits;
            Gpa = gpa;
         }
         
         public Student(string name, int studentId): this(name, studentId, 0, 0) { }
         
         public Student(string name): this(name, nextStudentId)
         {
            nextStudentId++;
         }
      }
   ```

   {{% /expand %}}

1. In `Program.cs`, instantiate the `Student` class using yourself as the student. For the
   `NumberOfCredits` give yourself `1` for this class and a GPA of `4.0`
   because you are a C# superstar!

   Test your  new `Student` object with print statements.  Are you able to get and set each field?

   {{% expand "Check Your Solution" %}}

   ```csharp {linenos=table}
      // TODO: Instantiate your objects and test your exercise solutions with print statements here.

      Student kimberly = new Student("Kimberly", 1, 1, 4.0);
      Console.WriteLine("The Student class works! " + kimberly.Name + " is a student!");
   ```
   
   {{% /expand %}}

1. In the `Classes` project, create a class `Course` with at least three
   fields. Before diving into Visual Studio, try using pen and paper to work through
   what these might be. At least one of your fields should be a `List`
   or `Dictionary`, and you should use your `Student` class.

   {{% expand "Check Your Solution" %}}

   ```csharp {linenos = table}
      // Create a new file Course.cs

      using System;
      using System.Collections.Generic;
      
      namespace SchoolPractice
      {
         public class Course
         {
            private string topic;
            private Teacher instructor;
            private List<Student> enrolledStudents;
         }
      }
   ```
   
   {{% /expand %}}

1. Using auto-implemented properties, in the `SchoolPractice` project, create a class `Teacher` with four properties:
   `FirstName`, `LastName`, `Subject`, and `YearsTeaching`.