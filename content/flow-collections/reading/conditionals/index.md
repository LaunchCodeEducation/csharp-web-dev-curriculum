---
title: "Conditionals"
date: 2023-01-25T13:44:27-06:00
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

Before you start this chapter, fork and clone the [csharp-web-dev-examples](https://github.com/LaunchCodeEducation/csharp-web-dev-examples) repository. This repository contains the example projects in the reading section. 

For the Conditionals section, be sure to explore the `Conditionals` project in the repo.

## Operators
Before we review the syntax for conditionals, let’s go over the comparison and logical operators that we need to use in control flow statements.

### Comparison Operators

| Operator | Description |
|:----------|:------------|
|`==`       | Checks if two items are equal |
|`!=`       | Checks if two items are not equal | 
|`<`        | Checks if item on left is lesser than item on right |
|`<=`       | Checks if item on left is lesser than or equal to item on right |
|`>`        | Checks if item on left is greater than item on right |
|`>=`       | Checks if item on left is greater than or equal to item on right |

### Logical Operators

| Operator   | Description |
|-----------|------------|
| `!`        | Reverses the evaluation of the operand |
| `\|\|`     | Combines two expressions with OR | 
| `&&`       | Combines two expressions with AND |

## `if` Statements

Let’s consider an **if statement** with no `else` clause.

In C#, this pattern is simply written as:

```csharp
if (condition)
{
   statement1
   statement2
   ...
}
```

You can see that in C#, the curly braces define a block. Parentheses around the condition are required.

## `if else`

Adding an **else clause**, we have:

```csharp
if (condition)
{
   statement1
   statement2
   ...
}
else
{
   statement1
   statement2
   ...
}
```

## `else if`

An **else if** construction in C#:

```csharp
Console.WriteLine("Enter a grade: ");
string gradeString = Console.ReadLine();
int grade = int.Parse(gradeString);
if (grade < 60)
{
      Console.WriteLine('F');
}
else if (grade < 70)
{
      Console.WriteLine('D');
}
else if (grade < 80)
{
      Console.WriteLine('C');
}
else if (grade < 90)
{
      Console.WriteLine('B');
}
else
{
      Console.WriteLine('A');
}
```

## `switch` Statements
C# also supports a **switch** statement that acts something like an `else if` statement under certain conditions, called **cases**. The `switch` statement is not used very often, and we generally recommend you avoid using it. It is not as powerful as the `else if` model because the `switch` variable can only be compared for equality with a very small class of types.

Here is a quick example of a `switch` statement:

```csharp
Console.WriteLine("Enter an integer: ");
string dayString = Console.ReadLine();
int dayNum = int.Parse(dayString);

string day;
switch (dayNum) {
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

Note that each case ends with a `break` statement. We will look at why this is in the following section.

In the example above, here’s the output if a user enters the number `4`.

```
Enter an integer:
4
Thursday
```

And the output if that user enters `10`? Below:

```
Enter an integer:
`10`
Int does not correspond to a day of the week
```

Here’s how the above example looks using the `else if` construction:

```csharp
Console.WriteLine("Enter an integer: ");
string dayString = Console.ReadLine();
int dayNum = int.Parse(dayString);

string day;
if (dayNum == 0)
{
   day = "Sunday";
}
else if (dayNum == 1)
{
   day = "Monday";
}
else if (dayNum == 2)
{
   day = "Tuesday";
}
else if (dayNum == 3)
{
   day = "Wednesday";
}
else if (dayNum == 4)
{
   day = "Thursday";
}
else if (dayNum == 5)
{
   day = "Friday";
}
else if (dayNum == 6)
{
   day = "Saturday";
}
else
{
   day = "Int does not correspond to a day of the week";
}
Console.WriteLine(day);
```

## Fallthrough

Many C-based languages utilize switch statements. However, not all languages share the same behavior when it comes to **fallthrough**. Fallthrough is what happens when a `break` statement is omitted and is described in detail in this article on [switch statements](https://en.wikipedia.org/wiki/Switch_statement#Fallthrough). In C#, you can take advantage of fallthrough behavior in specific circumstances with blank cases. If the behavior we want matches for two cases, then we can take advantage of this fallthrough action.

We want to use a `switch` statement to tell us if it is the weekend or a weekday. Here is how we might modify the switch statement from above and make use of fallthrough.

```csharp
Console.WriteLine("Enter an integer: ");
string dayString = Console.ReadLine();
int dayNum = int.Parse(dayString);

string weekZone;
switch (dayNum)
{
    case 0:
        weekZone = "Weekend";
        break;
    case 1:
    case 2:
    case 3:
    case 4:
    case 5:
        weekZone = "Week Day";
        break;
    case 6:
        weekZone = "Weekend";
        break;
    default:
        // in this example, this block runs if none of the above blocks match
        weekZone = "Int does not correspond to a day of the week";
        break;
}
Console.WriteLine(weekZone);
```

Because we want to set the value of `weekZone` to `"Week Day"` for cases 1-5, we omit the `break` statements and any other code.

## Check Your Understanding

{{% notice green "Question" "rocket" %}} 
When does fallthrough occur in C#?
   1. Omitting an else clause from a conditional.
   1. Omitting an else clause from switch statement.
   1. Omitting a default case from a switch statement.
   1. Omitting a break line from a switch statement.

<!-- ans: Omitting a break line from a switch statement. -->
{{% /notice %}}

{{% notice green "Question" "rocket" %}} 
```csharp
Console.WriteLine("Are you a space cadet? yes or no");
string response = Console.ReadLine();

switch (response) {
   case "yes":
      Console.WriteLine("Greetings, cadet.");
   case "no":
      Console.WriteLine("Greetings, normie.");
   default:
      Console.WriteLine("Are you an alien?");
}
```
Given the code above, what prints if the user enters `no` after the prompt?
1. ```
   Greetings, cadet.
   ```
1. ```
   Greetings, normie.
   ```
1. ```
   Greetings, normie.
   Are you an alien?
   ```
1. ```
   Greetings, cadet.
   Greetings, normie.
   ```
1. The program doesn’t work as written.

<!-- ans:  The program doesn't work as written. -->
{{% /notice %}}