---
title: "Some C# Practice"
date: 2023-01-17T16:28:22-06:00
draft: false
weight: 2
originalAuthor: Sally Steuterman # to be set by page creator
originalAuthorGitHub: gildedgardenia # to be set by page creator
reviewer: # to be set by the page reviewer
reviewerGitHub: # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

Let’s move beyond our "Hello, World" example from the introduction and explore a simple temperature
conversion program. We want our function to convert a Fahrenheit temperature to
Celsius.

To get started, fork and clone the [csharp-web-dev-examples repository](https://github.com/LaunchCodeEducation/csharp-web-dev-examples). This repo includes examples you should review as you read for the first 7 or so lessons.

## Temperature Conversion

1. Open the `TempConverter` project in your `csharp-web-development-examples` solution in Visual Studio.

   ![TempConverter project](pictures/tempConverterTree.png)

1. Here's what the file should look like. We will analyze the different statements in a moment.

   ```csharp {linenos=table}
      double fahrenheit;
      double celsius;
      string input;

      Console.WriteLine("Temperature in F:");
      input = Console.ReadLine();
      fahrenheit = double.Parse(input);

      celsius = (fahrenheit - 32) * 5 / 9;
      Console.WriteLine("The Temperature in C is: " + celsius);
      Console.ReadLine();
   ```

1. Run the program to verify that it works. Entering a Fahrenheit
   temperature of `212` yields the result, `The temperature in Celsius is: 100`.

There are several new concepts introduced in this example. We will look
at them in the following order:

1. The `using` statement
1. Variable declaration
1. The `Console` class

## `using`

The `using` statement in C# allows us to access classes, methods, and
data stored in different files other than the one we are currently in.

In C#, you can use any class that is available without having to import
the class - subject to two very important conditions:

1. The C# compiler must know that the class exists.
2. You must use the full name of the class.

Classes that are available to you may be those in the project you are currently working on,
or those that come along with the .NET class library, as well as anything you might get 
from added dependencies.

The class naming system in C# is very hierarchical. The *full* name of the `Console`
class used first on line 13 is really `System.Console`. You can think of this name as having
two parts. The first part, `System`, is called the **namespace**, and
the last part is the **class**. We’ll talk more about the class naming
system a bit later. 
One thing to know about the `using` statement is that it is not responsible for loading classes into memory.
That task falls on the **assembly**, which is the unit of compiled code
created by Visual Studio (or the C# compiler, more generally).

The `using` statement tells the compiler that we are going to use a
shortened version of the class’s name. In this example, we are going to
use the class `System.Console`, but we can refer to it as just
`Console`. We could use the `System.Console` class without any
problem and without any import statement provided that we always
referred to it by its full name.

Don’t just trust us, try it yourself! Remove the `using` statement and
change `Console` to `System.Console` in the rest of the code. The
program should still compile and run.

## Declaring Variables

In the example above, these lines contain variable declarations:

```csharp {linenos=table}
   double fahrenheit;
   double celsius;
   string input;
```

Specifically, we are saying that `fahrenheit` and `celsius` are going
to reference objects that are of type `double`. The variable `input`
will contain a string. This means that if we were to try an assignment
like `fahrenheit = "xyz"` the compiler would generate an error because
`"xyz"` is a string and `fahrenheit` is supposed to be a double.

Suppose we forgot the declaration for `celsius` and instead
left that line blank. What would happen if we try to run our program?

We get a few errors! The end of the build output looks something like this:

```console 
   Build FAILED.

   warning CS8600: Converting null literal or possible null value to non-nullable type.
   warning CS8604: Possible null reference argument for parameter 's' in 'double double.Parse(string s)'.
   error CS0103: The name 'celsius' does not exist in the current context
   error CS0103: The name 'celsius' does not exist in the current context
      2 Warning(s)
      2 Error(s)

   Time Elapsed 00:00:00.55

   ========== Build: 0 succeeded, 1 failed, 0 up-to-date, 0 skipped ==========

   Build: 2 errors, 2 warnings
```

The compiler detects an error and Visual Studio displays this message.
Visual Studio will notify you of the errors detected in a few locations, including 
the errors pane and the Application Output pane.

{{% notice blue "Note" "rocket" %}}

   You may have expected to receive an error from some red in your program file.
   When using an IDE such as Visual Studio, your code is typically checked
   by the IDE’s built-in compiler as you write your code. Thus, errors are
   usually visually indicated within your code by the IDE as you write your
   code, saving you the extra step of having to explicitly compile your
   code before finding compiler errors. Nice, huh?

{{% /notice %}}

The general rule in C# is that you must decide what kind of an object
your variable is going to reference and then you must declare that
variable before you use it. There is much more to say about the static
typing of C#, but for now this is enough.

## Input / Output and the Console Class

Console input and output is facilitated by the class `System.Console`.
We’ll rely heavily on just two methods of this class:
`Console.WriteLine` and `Console.ReadLine`.

`Console.WriteLine` can take parameters of various types, including
`string`, `char`, `double`, `bool`, and others. `Console.WriteLine` can only 
be provided a single argument. Thus, we’ll need to manually concatenate strings and other 
values if we want to print a composite value, converting types if necessary. A newline
character is output after the given message.

```csharp
   int year = 2020;
   Console.WriteLine("Hello" + "World")
   Console.WriteLine("The year is " + year.ToString());
```

Similarly, `Console.ReadLine` returns input as a string. To convert it
to a desired type, you can generally use the syntax
`[TYPE].Parse(value)`, with `[TYPE]` replaced by the given type.
Here’s an example:

```csharp
   string userInput = Console.ReadLine();
   int year = int.Parse(userInput);
```

## Add Comments to Your Code

As programs get bigger and more complicated, they get more difficult to read.
Good programmers try to make their code understandable to others, but it is
still tricky to look at a large program and figure out what it is doing and
why.

Also, there are times when programmers need to isolate or ignore certain
portions of their code as they are testing it. In the "Try It" box above, you
were instructed to *remove* a line of code in order to create compiler errors.
However, programmers are usually reluctant to delete lines that they might need
to bring back.

Best practice encourages us to add **comments** to our programs. Comments are
notes that clearly explain what the code is doing.

A comment is text within a program intended only for a human reader—--it is
completely ignored by the compiler or interpreter. In C#, the `//` token
indicates the start of a comment, and the rest of the line gets ignored. For
comments that stretch over multiple lines, the text falls between the symbols
`/*   */`.

Comments can be used to temporarily skip a portion of the code when a
program runs. Instead of removing `double celsius;` in `TempConverter`, we
could *comment out* the line. This would create the same compiler errors we
wanted to witness, but it would preserve the original code and allow us to
easily reactivate it by removing the `//` token from the line.

{{% notice blue "Example" "rocket" %}}

   ```csharp {linenos=table}
      // Here is an example of a comment.

      /* Here is how
      to have
      multi-line
      comments. */

      /*
      Or
      like
      this.
      */

      Console.WriteLine("Hello World!"); // Comments do not have to start at the beginning of a line.
      // Console.WriteLine("Hello comments!"); This line won't print!
   ```
{{% /notice %}}

{{% notice blue "Note" "rocket" %}}

   In addition to single-line comments and multi-line comments, C# developers can also use XML documentation comments.
   XML documentation comments start with `///` and when properly written, can be used to generate documentation for a project.
   This comment type is something you may encounter working on enterprise code for a company, but is not something that you would use in smaller, personal projects.
   For more information on XML documentation comments, check out the [documentation](https://docs.microsoft.com/en-us/dotnet/csharp/codedoc).
{{% /notice %}}

## Check Your Understanding

{{% notice green "Question" "rocket" %}}
   True or False, a `using` statement is required to use a C# class defined outside of your current file.\
{{% /notice %}}

{{% notice green "Question" "rocket" %}}
   What is the name of the method used to convert input strings to different types?
   1. `.Convert()`
   1. `.ToString()`
   1. `.Parse()`
   1. `.ReadLine()`
{{% /notice %}}