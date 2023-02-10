---
title: "Exercises: Objects and Classes, Part 2"
date: 2023-01-30T09:32:46-06:00
draft: false
weight: 3
originalAuthor: Courtney Frey # to be set by page creator
originalAuthorGitHub: speudusa # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: Courtney Frey # update any time edits are made after review
lastEditorGitHub: speudusa # update any time edits are made after review
lastMod: 2023-08-02 # UPDATE ANY TIME CHANGES ARE MADE
---

<!-- TODO: Link to repo -->
You will find these exercises in `Classes-Part-2` project of the exercises repo. You will update your `Student.cs` file by implementing the `AddGrade` and `GetGradeLevel` methods that were sketched out in the [Instance Methods]({{< relref "../reading/instance-and-static/#instance-methods" >}}) section.

## The `GetGradeLevel` Method
This method returns the student’s level based on the number of credits they have earned: Freshman (0-29 credits), Sophomore (30-59 credits), Junior (60-89 credits), or Senior (90+ credits).

{{% expand "Check your solution" %}}
```csharp
   public string GetGradeLevel(int credits)
   {
      if (credits <= 29)
      {
         return "Freshman";
      }
      else if (credits <= 59)
      {
         return "Sophomore";
      }
      else if (credits <= 89)
      {
         return "Junior";
      }
      else
      {
         return "Senior";
      }
   }
```
{{% /expand %}}

## The `AddGrade` Method
This method accepts two parameters—a number of course credits and a numerical grade (0.0-4.0). With this data, you need to update the student’s GPA.

### GPA Information
GPA is computed via the formula:

> gpa = (total quality score) / (total number of credits)

The quality score for a class is found by multiplying the letter grade score (0.0-4.0) by the number of credits.

The total quality score is the sum of the quality scores for all classes.

For example, if a student received an “A” (worth 4 points) in a 3-credit course and a “B” (worth 3 points) in a 4-credit course, their total quality score would be: 4.0 * 3 + 3.0 * 4 = 24. Their GPA would then be 24 / 7 = 3.43.

### Determine the New GPA
To update the student’s GPA:

   1. Calculate their current total quality score by using the formula `gpa * numberOfCredits`.

   1. Use the new course grade and course credits to update their total quality score.

   1. Update the student’s total `numberOfCredits`.

   1. Compute their new GPA.

{{% expand "Check your solution" %}}
```csharp
public void AddGrade(int courseCredits, double grade)
   {
      // Update the appropriate properties: NumberOfCredits, Gpa
      double totalQualityScore = Gpa * NumberOfCredits;
      totalQualityScore += courseCredits * grade;
      NumberOfCredits += courseCredits;
      Gpa = totalQualityScore / NumberOfCredits;
   }
```
{{% /expand %}}

## `ToString` and `Equals`
   1. Add custom `Equals()` and `ToString()` methods to the `Student` class.
   1. Add custom `Equals()` and `ToString()` methods to the `Course` class which you started in the exercises for the previous chapter.

{{% expand "Check your solution" %}}
```csharp
public override string ToString()
   {
      return Name + " (Credits: " + NumberOfCredits + ", GPA: " + Gpa + ")";
   }

   public override bool Equals(object obj)
   {
      if (obj == this)
      {
         return true;
      }

      if (obj == null)
      {
         return false;
      }

      if (obj.GetType() != GetType())
      {
         return false;
      }

      Student studentObj = obj as Student;
      return StudentId == studentObj.StudentId;
   }
```
{{% /expand %}}