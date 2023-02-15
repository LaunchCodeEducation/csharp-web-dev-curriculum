---
title: "Objects and Methods, a Primer"
date: 2023-01-17T16:28:22-06:00
draft: false
weight: 4
originalAuthor: Sally Steuterman # to be set by page creator
originalAuthorGitHub: gildedgardenia # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

There is a lot to say about objects in C# that we'll cover in due time. Here, we highlight some introductory 
concepts of how C# works as an object-oriented programming language.

## Objects

In C#, **objects** are structures that have a *state* and a set of
*behaviors*. The state of an object includes properties/data that the coder can
define and modify. Behaviors are actions that run when requested, and they can
be used to evaluate, manipulate, or return data.

As we've said several times now, every variable in C# refers to an object.

The `string` data type is an object. For
`string language = "C#"`, the data would be the characters. The
[String Manipulation]({{< relref "../strings-chars-and-arrays#string-manipulation" >}}) section gives several of the
behaviors available to the `language` object. For example,
`language.Length` is `2`, which tells us how many
characters are present in the string.

An [array]({{< relref "../strings-chars-and-arrays/#arrays" >}}) is also an example of an object. It contains *data*, which are the values
stored as the individual elements. The *behaviors* are methods not unlike those listed in the 
string manipulation table that perform actions related to the elements in the array. We haven't 
provided an array methods table, but you can explore array methods in 
[the docs](https://docs.microsoft.com/en-us/dotnet/api/system.array?view=netframework-4.8#methods).

## Static Methods

In pure object-oriented languages like C# and Java, we don’t have
functions in the sense you may be used to. Functions may not be declared
outside of a class. Within the context of a class, functions are
referred to as **methods**. We’ll adopt this terminology from now on.

We’ll dive into learning about classes and objects in C# soon enough,
but first let’s learn a little about **static methods**, which behave
somewhat similarly to stand-alone functions. A static method is one that 
can be called without creating an object instance of the class to which it belongs.

{{% notice blue "Example" "rocket" %}}

   Define the class `Cat` and include the `static` keyword before the
   `makeNoise` method name:

   ```csharp {linenos=table}
      public class Cat {
         public static void MakeNoise(String[] args) {
            // some code
         }
      }
   ```

   Since `makeNoise` is `static`, we do NOT need to create a `Cat` object to
   access it.

   Instead of doing this:

   ```csharp
      Cat myCat = new Cat();     // Create a new Cat object.
      myCat.MakeNoise("purr");   // Call the MakeNoise method.
   ```

   We can call the method directly:

   ```csharp
      Cat.MakeNoise("roar");
   ```
{{% /notice %}}

Until we get further into object oriented programming, every method you write
should use the `static` keyword. Leaving off `static` will prevent or
complicate the process of calling the methods you defined.

We will explore exactly what `static` does in more detail in later lessons.

## `HelloMethods`

Let’s examine two classes in C# to explore defining and using methods. Open the 
`HelloMethods` project in `csharp-web-development-examples`.

The first class is defined in the `HelloMethods/Program.cs` file. The second class is defined in a separate `HelloMethods/Message.cs`
file, and it contains a `GetMessage` method that we want to call from within
`Main`.

{{% notice blue "Example" "rocket" %}}

   `HelloMethods/Program.cs`:

   ```csharp {linenos=table}
      string message = Message.GetMessage("fr");
      Console.WriteLine(message);
      Console.ReadLine();
   ```

   `HelloMethods/Message.cs`:

   ```csharp {linenos=table, linenostart=3}
      namespace HelloMethods
      {
         public class Message
         {
            public static string GetMessage(string lang)
            {
                  if (lang.Equals("sp")) {
                     return "Hola Mundo";
                  }
                  else if (lang.Equals("fr"))
                  {
                     return "Bonjour le monde";
                  }
                  else
                  {
                     return "Hello World";
                  }
            }
         }
      }
   ```

{{% /notice %}}

We won’t explore every new aspect of this example, but rather will focus
on the `GetMessage()` method.

1. Take a look at the `Message` class. It has one method that isn't called within the class. Code within the `Message` class must be called from elsewhere in order to execute.
1. The `Message` class contains the `GetMessage()` method. It has the `static` keyword and a return type of `string`.
1. `GetMessage()` takes a single `string` parameter, `lang`.

Since C# is statically typed, each method must declare its return type -
that is, the data type of what it will return - along with the type of
each parameter. One consequence of this that may not be immediately
obvious is that methods in C# may not return different types of data.
For example, we would not be able to replace the last `return`
statement of `GetMessage()` with something like `return 42;`. This
would be flagged as a compiler error.

### `Main()` Methods

After Microsoft released .NET 6, the `Program.cs` class looked different. Prior to this release, `Program.cs` contained a `Main()` method and code was written inside the `Main()` method. Now at the time of compilation, your code in `Program.cs` is synthesized with a `Main()` method. This is important to know because in a C# project, only one `Main` method is allowed. When the project is compiled and run, the `Main` method indicates what should be executed,
and if there were multiple `Main` methods this would be ambiguous. What you write in `Program.cs` becomes the body of the `Main()` method for the project.

{{% notice blue "Example" "rocket" %}}
   To get a sense for this, let's revisit the code in `Program.cs` for the TempConverter project.

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

   In older C# code, with the `Main()` method made available to the developer, the same `Program.cs` file would look like:

   ```csharp {linenos=table}
      using System;

      namespace TempConv
      {
         class Program
         {
            public static void Main(string[] args)
            {
                  double fahrenheit;
                  double celsius;
                  string input;

                  Console.WriteLine("Temperature in F:");
                  input = Console.ReadLine();
                  fahrenheit = double.Parse(input);

                  celsius = (fahrenheit - 32) * 5 / 9;
                  Console.WriteLine("The Temperature in C is: " + celsius);
                  Console.ReadLine();
            }
         }
      }
   ```

{{% /notice %}}

### Public Methods

Finally, let’s note how a static method is called. The first line of the `Program` class is:

```csharp
   Message.GetMessage("fr");
```

To call a static method, we must use the name of the class in which it is
defined, followed by `.`, followed by the name of the method.

```csharp
   ClassName.methodName(arguments);
```

We are able to call this method from another class because it is
declared to be `public`. If we wanted to restrict the method from
being called by another class, we could instead use the `private`
modifier. We’ll explore *access modifiers* in more depth in coming
lessons.

{{% notice blue "Note" "rocket" %}}

   As you have been following along with this example, you may have noticed
   that the class file, `Message.cs`, is named exactly the same as the class it holds.

   There is *NOT* a rule in C# dictating that a file must be named the same as the class it contains, 
   but it is considered best practice.

{{% /notice %}}

### Try It

Poke around with the `HelloMethods` project in Visual Studio and experiment with the
following:

1. Figure out how to alter the `HelloMethods` code to change the message returned.
1. Add another "Hello, World" language option.
1. Change one `public` keyword to `private` to see what happens. Repeat for each occurrence of `public`.

## Check Your Understanding

{{% notice green "Question" "rocket" %}}
   Which of the following defines a method that takes an integer as a parameter and returns a string value?
   1. `public static void MethodName(string parameterName)`
   1. `public static void MethodName(int parameterName)`
   1. `public static int MethodName(string parameterName)`
   1. `public static string MethodName(int parameterName)`
{{% /notice %}}

{{% notice green "Question" "rocket" %}}
   True/False: A C# project may contain more than one `Main` method, as long as at least one of those methods is marked `private`.
{{% /notice %}}