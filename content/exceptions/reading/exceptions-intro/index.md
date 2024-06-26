---
title:  "Introduction to Exceptions"
date: 2023-02-08T10:27:25-06:00
draft: false
weight: 1
originalAuthor: Courtney Frey # to be set by page creator
originalAuthorGitHub: speudusa # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

Like most programming languages, C# includes exceptions and exception handling tooling. Some exception objects are provided by .NET itself. Other exception objects we may get from external C# libraries. We may even write these objects ourselves.

**Exceptions** in C# are objects derived from the `System.Exception` class. You see exception objects at runtime when some event takes place outside of the expected flow of our code. When you want to explicitly call an exception in your code, you do so with the throw keyword. We’ve actually done this before in this book and will return to that example shortly.

Maybe you see the term “exception” and instinctively groan or roll your eyes? Isn’t programming only enjoyable when it works? While it would be nice if our code ran perfectly every time, exceptions are a key component of a healthy codebase. When an exception arises, we, as programmers, can use the info to debug our code. For our fellow programmers, the exceptions we provide give them necessary intel on how our app runs and is meant to be used.

## When Exceptions Arise

You may have seen exceptions in C# or another programming language already, perhaps in one of these scenarios:

- Failure to connect to services external to your application, such as a database or API.
- Failure to read or write to or from a file.
- Failure to convert data, such as trying to convert something like "dog" to an int type.
- Failure to reach an actual object.

{{% notice blue "Note" "rocket" %}} 
This last scenario is a **null pointer**. This is an object reference that doesn’t actually contain an object. 
{{% /notice %}}

Indeed, we have even used exceptions in this book already. Recall the temperature example where we throw a built-in exception when a provided argument falls outside of an acceptable range. Later, we refine our [temperature app]({{% relref "../../../classes-part-2/reading/custom-fields/#a-temperature-example" %}}) and throw the more targeted `ArgumentOutOfRangeException`.

The example below is found in the `TemperatureExceptions` project in the [example code repo](https://github.com/LaunchCodeEducation/csharp-web-dev-exceptions).

```csharp{linenos=table,hl_lines=[],linenostart=1}
public class Temperature
{

   private double fahrenheit;
   public static double AbsoluteZeroFahrenheit { get; } = -459.67;

   public Temperature(double fahrenheit)
   {
      Fahrenheit = fahrenheit;
   }

   public double Fahrenheit
   {
      get
      {
         return fahrenheit;
      }
      set
      {

         if (value < AbsoluteZeroFahrenheit)
         {
            throw new ArgumentOutOfRangeException("Value is below absolute zero");
         }

         fahrenheit = value;
      }
   }
}
```

The program provides a plan for what to do in the event that bad data is passed into a class’s field. Imagine that a user or fellow programmer unintentionally sets a Fahrenheit value outside of the appropriate range.

Try this yourself to witness the breaking exception:

{{% notice blue "Example" "rocket" %}} 

*Input:*

```csharp
Temperature insideTemp = new Temperature(73);
Console.WriteLine(insideTemp.Fahrenheit);

Temperature outsideTemp = new Temperature(-8200);
Console.WriteLine(outsideTemp.Fahrenheit);
```

*Output:*
```bash
Unhandled exception. System.ArgumentOutOfRangeException: Specified argument was out of the range of valid values. (Parameter 'Value is below absolute zero')
   at TemperatureExceptions.Temperature.set_Fahrenheit(Double value) in /...file location.../Temperature.cs:line 25
   at TemperatureExceptions.Temperature..ctor(Double fahrenheit) in /...file location.../Temperature.cs:line 11
   at Program.<Main>$(String[] args) in /...file location.../Program.cs:line 6
```

{{% /notice %}}

Above, the Temperature constructor predictably sets the Fahrenheit value of `insideTemp` and throws an exception when provided a Fahrenheit value outside of the appropriate range. We don’t see any results of the print statement on the input’s line 5 since the exception has caused the program to stop running.

When we throw an exception like in the example above, we flag the anomalous circumstance. If we choose to do nothing when the exception is thrown, the program will stop and a record of the exception can be found in the stack trace. Alternatively, we can handle an exception and offer an alternative action, bypassing the need to stop the program. We’ll cover how to handle exceptions on the next page.

This is a common reason to include exception handling in your code. User input opens the door to a variety of erroneous figures and good programs account for this uncertainty. Without exceptions in these circumstances, a small typo could lead to any number of errors down the stack trace.

## When to Use Exceptions

It is wise to use an exception if you find that there is some level of chance involved in your program. This could be a situation where a variable is dependent on user input or a connection to another service.

You may want to address those uncertainties in a different fashion. With our temperature app for example, rather than throwing an exception, we can add a conditional statement to tell the user not to set the Fahrenheit value to an unacceptable level. This is perfectly acceptable if the app in production allows for such a message. As you will see on the next page, exception handling works very similarly to conditional statements like this.

There are many places where user-directed error messages simply won’t be appropriate. For example, what if the value being set doesn’t come from a user but from a different method in the program? In a situation like this, where the anomaly is not visible to the user, an exception conveys the issue to fellow programmers who are using our codebase.

Or another hypothetical. What if managing the variety of errors that may arise is outside the scope of the project? In these cases where we do not, or cannot, make up for the edge cases with coded solutions, we can throw an exception. Exceptions are an informed way to convey the constraints of your program.

## Check Your Understanding

{{% notice green  "Question" "rocket" %}} 

What is the action of invoking an exception called?

   1. excepting
   1. catching
   1. throwing
   1. handling 

<!-- ans: throwing -->

{{% /notice %}}

{{% notice green  "Question" "rocket" %}} 

**True/False:** Encountering an exception will always result in terminating a running program.

<!-- ans: False, When appropriate, an exception can be handled to initiate an alternate pathway -->

{{% /notice %}}