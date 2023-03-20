---
title: "Introduction to Enums"
date: 2023-02-27T14:58:53-06:00
draft: false
weight: 1
originalAuthor: Sally Steuterman # to be set by page creator
originalAuthorGitHub: gildedgardenia # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

Many statically-typed programming languages provide a feature called
**enumeration types**, or **enum types** for short. Enum types are special
classes that can have only one of a set of fixed values, such as days of the
week.

Imagine that we wanted to add a property to `Event` to specify which day of the
week an event takes place. You might start by creating a new field:

```csharp
   [Required]
   public string DayOfWeek { get; set; }
```

As defined here, a user could submit any of the following values representing Wednesday:

1. `"Wednesday"`
1. `"wednesday"`
1. `"Wed"`
1. `"WED"`
1. `"W"`

Accepting data like this leads to many complications.
For example, searching for all events taking place on Wednesday would need to account for all of these variations.
And what happens if a user misspells "Wednesday"?

When filling out forms on the web, you are used to seeing dropdown menus with prefilled values restricting the possible inputs.
For example, in the United States, when filling out a shipping address form, a `select` element may be used to create a list of the states to insure that users select the correct abbreviation for their state of residence.

Limiting the values that the user can select drastically reduces complexity and
ensures that our application data remains clean and standardized. Enum types
are one way to model fields like this.

## Creating an Enum Type

Let's see how we can create an enum type, or enum class.

{{% notice blue "Note" "rocket" %}}
   
   Recall that a class defines a new *data type*.
   Thus, the term "data type" can be used in place of "class".
   We'll typically call enum classes "enum types" since this is what most C# developers do.

{{% /notice %}}

The simplest enum type that we can define to represent days of the week looks
like this:

```csharp {linenos = table}
   enum Day
   {
      Sunday,
      Monday,
      Tuesday,
      Wednesday,
      Thursday,
      Friday,
      Saturday
   }
```

Using the `enum` keyword specifies that this class should be an enum type. In
other words, it should only be able to take on one of a fixed set of values.
Within the body of the class, we list the valid names (`Sunday`, `Monday`,
etc.). Unless otherwise specified, each name refers to a value.By default, the values of
an enum type will be integers beginning with `0`. In fact, the
enum above is very similar to this class:

```csharp {linenos = table}
   public class DayConst
   {
      public const int Sunday = 0;
      public const int Monday = 1;
      public const int Tuesday = 2;
      public const int Wednesday = 3;
      public const int Thursday = 4;
      public const int Friday = 5;
      public const int Saturday = 6;
   }
```

To refer to Thursday, you can use the value `DayConst.Thursday`. Recall our
`switch` [example from earlier]({{< relref "../../../flow-collections/reading/conditionals/#switch-statements" >}}).

```csharp {linenos = table}
   Console.WriteLine("Enter an integer: ");
   string dayString = Console.ReadLine();
   int dayNum = int.Parse(dayString);

   string day;
   switch (dayNum)
   {
      case 0:
         day = "Sunday";
         break;
      case 1:
         day = "Monday";
         break;
      case 2:
         day = "Tuesday";
         break;
      case 3:
         day = "Wednesday";
         break;
      case 4:
         day = "Thursday";
         break;
      case 5:
         day = "Friday";
         break;
      case 6:
         day = "Saturday";
         break;
      default:
         // in this example, this block runs if none of the above blocks match
         day = "Int does not correspond to a day of the week";
         break;
   }
   Console.WriteLine(day);
```

This code can be refactored using `DayConst`:

```csharp {linenos = table}
   Console.WriteLine("Enter an integer: ");
   string dayString = Console.ReadLine();
   int dayNum = int.Parse(dayString);

   string day;
   switch (dayNum)
   {
      case DayConst.Sunday:
         day = "Sunday";
         break;
      case DayConst.Monday:
         day = "Monday";
         break;
      case DayConst.Tuesday:
         day = "Tuesday";
         break;
      case DayConst.Wednesday:
         day = "Wednesday";
         break;
      case DayConst.Thursday:
         day = "Thursday";
         break;
      case DayConst.Friday:
         day = "Friday";
         break;
      case DayConst.Saturday:
         day = "Saturday";
         break;
      default:
         // in this example, this block runs if none of the above blocks match
         day = "Int does not correspond to a day of the week";
         break;
   }
   Console.WriteLine(day);
```

In essence, this code represents days of the week as fixed integer values, one
for each day. Enum types are essentially a more robust version of this
approach.

Let's revisit our `Day` enum type:

```csharp {linenos = table}
   enum Day
   {
      Sunday,
      Monday,
      Tuesday,
      Wednesday,
      Thursday,
      Friday,
      Saturday
   }
```

We can declare a variable of type `Day` and it will only be allowed to take
on one of the 7 defined values.

```csharp {linenos = table}
   // This works
   Day workWeekStart = Day.Monday;

   // This does not, throwing a compiler error
   Day workWeekEnd = "TGIF";
```

Enums are important because they provide *type safety* in situations where we
want to restrict possible values. In other words, they eliminate the
possibility of bad, or dirty, values.

## Enum Examples

The world is filled with examples ripe for representation by enums. Here are a
few from both the real world and the world of programming.

{{% notice blue "Example" "rocket" %}}

   Months of the year.

   ```csharp {linenos = table}
      enum Month
      {
         January,
         February,
         March,
         April,
         May,
         June,
         July,
         August,
         September,
         October,
         November,
         December
      }
   ```

{{% /notice %}}

{{% notice blue "Example" "rocket" %}}

   Given a model type like our `Event` class, enums can represent categories that model objects can fall into.

   ```csharp {linenos = table}
      enum EventCategory
      {
         Conference,
         Meetup,
         Workshop,
         Social
      }
   ```

{{% /notice %}}

{{% notice blue "Example" "rocket" %}}

   A common use of enums in programming is to set the log level of an
   application. The **log level** represents the types of log messages that
   should be displayed as the application runs.

   You might only want to see critical error messages when running an application on a production server, but you may want to see many more messages, such as warnings and informational messages, when developing the application locally.

   ```csharp {linenos = table}
      enum LogLevel
      {
         Debug,
         Info,
         Warning,
         Error
      }
   ```

   An application can change the way it logs messages by changing the log level.

{{% /notice %}}

## Check Your Understanding

{{% notice green "Question" "rocket" %}}

   We mentioned above that all classes define a data type.
   Is the inverse of this statement true?
   In other words, do all data types correspond to a class? (*Hint:* Try to think of a data type that is NOT a class.)

   1. Yes, everything in C# is a class.
   1. No, there are data types that do not correspond to a class. (Be sure to provide an example.)

{{% /notice %}}

<!-- b, primitive data types are not classes. -->

{{% notice green "Question" "rocket" %}}

   Which of the following would NOT be a good choice for an enum type?

   1. States in the US
   1. Shoe sizes (using the American scale)
   1. Price of a gallon of milk
   1. Sections in a bookstore

{{% /notice %}}

<!-- c, Price of a gallon of milk -->