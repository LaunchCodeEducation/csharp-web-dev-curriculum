---
title: "Review the Starter Code"
date: 2023-01-03T10:42:56-06:00
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

Before diving in and starting to code, make sure you understand what the code
you've been given does. Since you're starting with a functioning---albeit
unfinished---program, go ahead and run it to get an idea of how it works. To do
this, explore the two projects in the solution. Right-click on the project that contains the `TechJobs` class and select *Run Project*.

{{% notice orange "Warning" "rocket" %}}

   The application will run until you force it to quit, re-prompting time
   after time. To kill it, press the "stop" icon in the upper corner the Run pane. We'll learn precisely how the program manages to work this way below.

{{% /notice %}}

Let's explore the code by starting with the source of the data our program is
providing access to.

## The Data File: `jobs_data.csv`

Our simple app doesn't connect to a database. If the prototype proves
useful and we continue development, we'll add that functionality later.
But for now, we've been given a CSV (comma-separated values) file from
the Company Team at LaunchCode that contains some recent jobs. This file
was exported from an Excel spreadsheet into this format, which is easy
for programs to read in.

If CSV files are new to you, don't worry, they're easy to understand.
CSV files are conceptually similar to simple spreadsheets in that they
organize data in rows and columns. The major difference is that they
don't have the ability to carry out calculations the way spreadsheets
do, and you can easily open, read, and edit them in plain text editors.

Open up `jobs_data.csv`, which is in the project. You'll see that the first line is:

```console
   name,employer,location,position type,core competency
```

While it isn't required, the first line of a CSV file often represents
the column names. We have 5 names here, which indicates that each of our
rows in the CSV file should have 5 fields. In this file format, a **row**
corresponds to a new line. So each line below the first will constitute
a row of data, or a record.

Have a look at the data below line 1, and ask yourself the following
questions:

1. Which fields match up with which column names above?
1. Why do some lines/rows (e.g. line 10) have more commas than others, if
   commas are supposed to separate columns?
1. What role do the double-quotes play in lines 10 and 79?

## The TechJobs Class

The `TechJobs` class contains three methods that will drive our
program's functionality:

1. `RunProgram()` - The main application runner.
1. `GetUserSelection()` - A utility method that displays a menu of choices and
   returns the user's selection.
1. `PrintJobs()` - This is meant to print a list of jobs to the console in a
   nicely formatted manner, but hasn't been implemented yet. 

Let's take a closer look at the first two methods, `RunProgram()` and `GetUserSelection()`.

### The `RunProgram()` Method

The logic within `RunProgram()` presents menus in turn, and based on the
user's choice, takes appropriate action.

It begins by declaring two local variables: `actionChoices` and
`columnChoices`. These contain information relating to the menus that
we'll display, and we'll look at them in more detail later.

Next, we notice a `while loop` that starts `while (true)`. While we usually
want to avoid creating infinite loops, we have a good reason for doing so in
this case! We want our application to continually run until the user decides
they want to quit. The simplest way to do this is to loop forever. When the
user wants to quit our app, they can enter `x` at the initial `View jobs by` prompt. 

{{% notice blue "Note" "rocket" %}}

   There are two ways to stop a running app. Either option works so you can pick the one that works best for you!
   
   1. Use the IDE.  Click Visual Studio's *Stop* icon, the square that replaces the *Run* triangle once an app is running.
   1. In the terminal, press *ctrl+C*. This will work in any terminal context, and not just for our console program in Visual Studio

{{% /notice %}}

The `RunProgram()` method can be summarized as follows:

1. Present the user with choices on how to view data: *list* or *search*.
1. Based on that choice, prompt them for the column to apply the choice to. In
   the case of a search, we also ask for a search term.
1. Carry out the request to the `JobData` class via one of its public
   methods.
1. Display the results of the request.
1. Repeat.

`RunProgram()` simulates a *query* to an external source:

1. We ask the method for data that originates from a non-C# source.
1. The method parses and filters that data.
1. The method presents the data in a useful manner.

### The `GetUserSelection()` Method

The `GetUserSelection()` method takes in a string to display above the
menu, to provide context for what they are being asked. It also takes in
a `Dictionary` with string keys and string values. How is this used? What
will this `Dictionary` contain when the method runs?

To figure this out, right-click on the method name and select *Find (All)
References*. This will open a pane and display each location in the program
where `GetUserSelection()` is called. The first such usage is the first
line of the main `while loop`:

```csharp {linenos=table, linenostart=30}
   string actionChoice = GetUserSelection("View Jobs", actionChoices);
```

What is this `Dictionary` named `actionChoices`? If we look a few lines
above, we see:

```csharp {linenos=true,linenostart=11}
   // Top-level menu options
   Dictionary<string, string> actionChoices = new Dictionary<string, string>();
   actionChoices.Add("search", "Search");
   actionChoices.Add("list", "List");
```

If you recall how the program worked when you ran it, the first menu
that you chose had two options, *Search* and *List*, which seem to
correspond to the entries in `actionChoices`. This is, in fact, the
case. This is the data that is used to generate the first menu we see
when running the program.

The second usage of `GetUserSelection()` is a few lines below:

```csharp {linenos=table,linenostart = 38}
   string columnChoice = GetUserSelection("List", columnChoices);
```

This references `columnChoices`, which is declared in the 
`RunProgram()`method and has a similar structure to `actionChoices` (they're the
same data type and are used in calls to the same method). Most of the entries in `columnChoices`
correspond to columns in the jobs data set, but there's one additional
entry with key/value pair `"all"`/ `"All"`. These entries will help
us present the user with the options for searching our data, which will
correspond to searching within a given column, or searching all columns
at once.

The keys in `actionChoices` and `columnChoices` represent the
*internal* strings we'll use to refer to these options (e.g. when representing
the user's menu choice, or querying data). The values in the `Dictionary` represent the
*external* way that these are represented to the user.

Within `GetUserSelection()` itself, most of the code is within a
`do-while loop`. A [do-while
loop](https://www.tutorialsteacher.com/csharp/csharp-do-while-loop)
is similar to a `while` loop, but the conditional check is at the
*end* of the loop's code block. This has the net consequence that the
loop's code block *always runs at least once*. At the end of the block's
execution, we check a condition to determine if we should run the block
again. This nicely mimics the behavior of simple menu-driven
applications.

Within this loop, menu options are printed to the screen, and user input
is collected. If the input is valid, it returns the choice as a `string`
to the caller. This `string` corresponds to the chosen key (from
`choices`, which will be either `actionChoices` or
`columnChoices`) of the item the user selected. If invalid, it
re-prompts the user.

The local variable `choiceKeys` is used to easily enumerate the
`choices` `Dictionary`. This gives us a simple way to
provide an ordering to `choices`, which doesn't have an ordering of
its own.

## The `JobData` Class, `JobData.cs`

The `JobData` class is responsible for importing the data from the CSV
file and parsing it into a C#-friendly format, that is, into
`Dictionary` and `List` form. Look for the method named `LoadData()` (line 85), which does just what it
advertises. After parsing the file data, it stores the data in the
private property `AllJobs` which is of type
`List<Dictionary<string, string>>`.

{{% notice blue "Note" "rocket"%}}

   We haven't covered static properties and methods in-depth yet. For this
   assignment, know that they allow us to use properties and methods
   of a class without creating an object from that class. For example, we
   can call `JobData.FindAll()` from the `TechJob` class.

   If you want to create a new method in `JobData`, or add a property, be
   sure to declare it as `static`.

{{% /notice %}}

Let's look more closely at the data type of `AllJobs`. It purports to
be a `List` that stores `Dictionary` objects which have
`string` keys and `string` values. If we were to represent some of
this data visually, using `[]` for a `List` and `{}` for a collection of
key/value pairs (i.e., a `Dictionary`), it would look like this:

```csharp {linenos=table}
   [
       {
           "name": "Junior Data Analyst",
           "employer": "Lockerdome",
           "location": "Saint Louis",
           "position type": "Data Scientist / Business Intelligence",
           "core competency": "Statistical Analysis"
       },
       {
           "name": "Junior Web Developer",
           "employer": "Cozy",
           "location": "Portland",
           "position type": "Web - Back End",
           "core competency": "Ruby"
       },
       ...
   ]
```

If you look at the `LoadData()` method you'll see a lot of unfamiliar code.
Blake wrote this essential piece of code for you, and while you won't have to
modify it, it will be useful to have an idea of how it works. Read
through the code until you feel like you can describe its functionality
at a basic level.

There are three more methods in `JobData`, each of which is public
(and `static`, per our earlier note): 
- `FindAll()`
- `FindAll(string)`
- `FindByColumnAndValue(string, string)`. 

Note that there are two methods named `FindAll()`, but this is allowed in
C# via a feature called **overloading**. Overloading happens when
multiple methods have the same name, but they each have different input
parameters (also called argument lists). Read more about
[overloading](https://www.geeksforgeeks.org/c-sharp-method-overloading/) here.

Here are some questions to ask yourself while reading this code:

1. What is the data type of a "job" record?
1. Why does `FindAll(string)` return something of type `List<string>`
   while `FindByColumnAndValue(string, string)` and `FindAll()` return
   something of type `List<Dictionary<string, string>>`?
1. Why is `LoadData()` called at the top of each of these four methods? Does
   this mean that we load the data from the CSV file each time one of them
   is called?

