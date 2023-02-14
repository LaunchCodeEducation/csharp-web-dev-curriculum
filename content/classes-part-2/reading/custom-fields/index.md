---
title: "Customizing Fields"
date: 2023-01-30T09:32:46-06:00
draft: false
weight: 1
originalAuthor: Courtney Frey # to be set by page creator
originalAuthorGitHub: speudusa # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: Courtney Frey # update any time edits are made after review
lastEditorGitHub: speudusa # update any time edits are made after review
lastMod: 2023-08-02 # UPDATE ANY TIME CHANGES ARE MADE
---

In the previous chapter, we used fields to store data within a class, and we explored how to access and modify the values of those fields.

Now, we will explore several ways to configure fields based on their intended use.

You will find the example code in the [csharp-web-dev-examples repo](https://github.com/LaunchCodeEducation/csharp-web-dev-examples/).  Be sure to try what you learn before moving on the the next section.

## Readonly Fields

A **readonly field** is one that cannot be changed once it is initialized. This means slightly different things for value and reference types. We create readonly fields by declaring them with the `readonly` keyword.

We cannot change the value of a `readonly` value field (`readonly` int, `readonly` double, etc.) after it is initialized.

Similarly, we cannot assign a new object to a `readonly` reference field (`readonly` `ClassName`, for example) after initialization. However, because objects are reference types and not value types, we can change the values within the object itself.

Here are some examples to illustrate. Each class would normally be in its own file, but we present them side-by-side for convenience. Additionally, we declare each field `public` to minimize the example code and more clearly demonstrate where compiler errors would occur.

Code for the example below can be found in the`ReadonlyExample` in the `Classes-Part-2` solution.

{{% notice blue "Example" "rocket" %}} 

In addition to `Program.cs`, we have two classes in a `FinalFields` project, `FinalFields` and `FortyTwo`.

`FortyTwo` contains one field:

   ```csharp{linenos=table,hl_lines=[],linenostart=6}
   public int intValue = 42;
   ```

`FinalFields` contains three fields:
   ```csharp{linenos=table,hl_lines=[],linenostart=6}
   public readonly int intValue = 42;
   public readonly double doubleValue;
   public readonly FortyTwo objectValue = new FortyTwo
   ```

Let’s see what happens when we try to reassign values to our `readonly` fields in `Program.cs`. 

```csharp{linenos=table,hl_lines=[],linenostart=8}
FinalFields demo = new FinalFields();

// This would result in a compiler error because IntValue has already been initialized.
demo.intValue = 6;

// This isn't allowed since we didn't initialize DoubleValue in the class declaration.
demo.doubleValue = 42.0;

// This would result in a compiler error.
demo.doubleValue = 6.0;

// This would result in a compiler error, since we're trying to
// give objectValue a different object value.
demo.objectValue = new FortyTwo();

// However, this is allowed since we're changing a field
// inside the final object, and not changing which object
// objectValue refers to.
demo.objectValue.intValue = 6;
```


{{% /notice %}}

Readonly fields help to prevent accidentally (or intentionally) changing the value of a field after it is initialized. As such, readonly fields may NOT have setters.

## Static Fields

A **static field** is one that is *shared by all instances of the class*, and it is declared with the `static` keyword.

For example, in our `Temperature` class there is no reason for each `Temperature` object to hold its own copy of the double `absoluteZeroFahrenheit`. That value remains constant in every class instance. Because of this, we make it a `static` field.

Previous examples used the `static` keyword with both fields and methods, but since this discussion is focused on class data, let’s focus on `static` fields for now.

### A Temperature Example

Inside the `Classes-Part-2` solution, you will find the following example in the `TemperatureExample` project.  Try it out as you read this section.

```csharp{linenos=table,hl_lines=[],linenostart=4}
public class Temperature
{

   private double fahrenheit;
   public static double absoluteZeroFahrenheit { get; } = -459.67;

   public double Fahrenheit
   {
      get
      {
         return fahrenheit;
      }
      set
      {

         if (value < absoluteZeroFahrenheit)
         {
            throw new ArgumentOutOfRangeException("Value is below absolute zero");
         }

         fahrenheit = value;
      }
   }
}
```

Static fields cannot be referenced by class instances, but a static field can by referenced by the *type*.  We can see this in the following example.

{{% notice blue "Example" "rocket" %}} 

Try this out for yourself in the example code repo. Print the messages from `Program.cs` using fields from the `Temperature` class.

```csharp
// If the static field is public, we can do this
Console.WriteLine("Absolute zero in F is: " + Temperature.absoluteZeroFahrenheit);

// If we have an object named "temp" of type Temperature, we cannot do this.
Console.WriteLine("Absolute zero in F is: " + temp.absoluteZeroFahrenheit);
```
{{% /notice %}}

### A Student Example

In the next example, you may add on to the `Student` project you created in the pervious chapter or start coding along in `StudentExample` project found in the `Classes-Part-2` solution.

{{% notice blue "Example" "rocket" %}} 

As another example, we might also provide a third constructor for our `Student` class that only requires the student’s name. Theoretically, the `StudentId` field would (or could) be generated by the class itself.

```csharp{linenos=table,hl_lines=[3, 25],linenostart=6}
public class Student {

   private static int nextStudentId = 1;
   public string Name { get; set; }
   private readonly int studentId;
   public int NumberOfCredits { get; set; }
   public double Gpa { get; set; }

   public Student(string name, int sId, int numberOfCredits, double gpa)
   {
      Name = name;
      studentId = sId;
      NumberOfCredits = numberOfCredits;
      Gpa = gpa;
   }

   public Student(string name, int sId)
   {
      Name = name;
      studentId = sId;
      NumberOfCredits = 0;
      Gpa = 0.0;
   }

   public Student(string name)
   {
      Name = name;
      studentId = nextStudentId;
      nextStudentId++;
      NumberOfCredits = 0;
      Gpa = 0.0;
   }
}
```


{{% /notice %}}


In line 6, we add a static integer field that will keep track of the next student ID to be assigned to a student. Then, our new constructor (line 30) takes only a name as a parameter and assigns the student the next available ID. This works because static fields are shared across all objects created from the `Student` class, so it functions as a counter of sorts for the number of `Student` objects created.

## Constants

In C#, we can also declare a constant, or unchanging, variable, using the `const` keyword.

```csharp{linenos=table}
public class Constants {
   public const double PI = 3.14159;
   public const string FIRST_PRESIDENT = "George Washington";
}
```

A couple things to note from this example:

   1. There is no strong reason to make constants `private`, since restricting access would force us to re-declare the same values in different classes. We’ll generally make our constants `public`.

   1. We must declare and initialize a constant at the same time. If we do not declare and initialize the constant in the same statement, we cannot assign it a value later. The constant’s value remains empty.

A good use of a constant can be seen in our `Temperature` class. Since absolute zero will never change, we can ensure that nobody ever alters it (intentionally or by mistake) by using `const` to make it a constant.

{{% notice blue "Example" "rocket" %}} 

Try updating the `absoluteZeroFahrenheit` from a `double` to a `const` value in your `TemperatureExample` project.

```csharp{linenos=table}
public class Temperature {

   private double fahrenheit;

   public const double ABSOLUTE_ZERO_FAHRENHEIT = -459.67;

   /* rest of the class... */

}
```
{{% /notice %}}

## Check Your Understanding

{{% notice green  "Question" "rocket" %}} 
Assume that we define a `Pet` class that uses the fields `name`, `age`, `mass`, and `species`.

Assuming you do not give your pet away, which of these fields should be declared `readonly`? (There may be more than one).

   1. name
   1. age
   1. mass
   1. species

<!-- The correct answers are "name", "species" -->
{{% /notice %}}

{{% notice green  "Question" "rocket" %}} 
Should any of the fields be declared `static`?

   1. Yes
   1. No
<!-- The correct answer is "No". -->
{{% /notice %}}

{{% notice green  "Question" "rocket" %}} 
Assume we define several fields in a `Circle` class. Which of the following is the BEST choice to be declared `static`?

   1. `radius`
   1. `area`
   1. `pi`
   1. `circumference`

<!-- The correct answer is "pi". -->
{{% /notice %}}

{{% notice green  "Question" "rocket" %}} 
Which of the following is the BEST syntax for defining a variable to hold the (constant) speed of light in a vacuum?

   1. `public const int SPEED_OF_LIGHT = 299792458;`
   1. `private const int SPEED_OF_LIGHT = 299792458;`
   1. `public const int SPEED_OF_LIGHT;`
   1. `private const int SPEED_OF_LIGHT;`
<!-- The correct answer is "public const int SPEED_OF_LIGHT = 299792458;". -->
{{% /notice %}}