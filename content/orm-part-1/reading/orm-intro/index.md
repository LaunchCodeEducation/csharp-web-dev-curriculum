---
title: "Introduction to Object-Relational Mapping"
date: 2023-03-10T09:32:46-06:00
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

Currently our app only saves data while it is running. Once you end the session and close the program, all of the data you provided disappears. We can make that data **persistent** by connecting your application to a database.  This will retain the data even if the application is not running, and allow you to access it when you open a new session.  

Let's connect our MVC application to a [relational database](https://education.launchcode.org/SQL/chapters/mysql-part-2/relationships.html) and add persistent data storage to our apps. To do so, we need to use _object-relational mapping_.

**Object-Relational Mapping** or **ORM** is a technique for converting data between C# objects and relational databases. ORM converts data between two incompatible type systems (C# and MySQL), such that each model class becomes a _table_ in our database and each instance a _row_ of the table.

To make ORM work in our C# applications, we need an **object-relational mapper** to convert between C# and MySQL. When we create a new model class and configure it to be stored in a database, a mapper creates a MySQL query to make the corresponding table. 

{{% notice blue "Example" "rocket" %}}

Let's think about this in `CodingEvents`.

In CodingEvents, we have the `Events` class that contains the following properities:
- `Id`
- `Name`
- `Description`
- `ContactEmail`

Now we want to store this information in a MySQL database. We can use ORM so that the database of our application has a table to contain all objects instantiated from the `Events` class. 

The table called `Events` has four columns: 
- interger `Id`
- varchar `Name`
- varchar `Description`
- varchar `ContactEmail`.  

Now, let's instantiate a C# `Events` object:

```csharp {linenos=table}

public Events codeWithPride = new Events("Code With Pride", "Creating community for LGBTQIA+ technologists and allies", "info@launchcode.org")

```
Recall, the `Id` is set by the constructor at this time.  We will learn more about this soon.

Having set up our application, we can add info about the Code with Pride event to our `Events` table. While we will write the code to add Code With Pride's info to our database in C#, the frameworks and APIs that make ORM happen will run the following MySQL query for us:

```sql {linenos=table}
INSERT INTO Events (Name, Description, ContactEmail)
VALUES ("Code With Pride",Creating community for LGBTQIA+ technologists and allies", "info@launchcode.org");
```

Now Code with Pride and all the information we provided is stored in our MySQL database in the `Events` table!  

{{% /notice %}}


## ORM in ASP.NET
<!-- TODO: Link to chapter 14: data layers -->

One of the most widely used object-relational mappers available for C# and ASP.NET Core is **Entity Framework Core**. This framework makes use of **data layers**. When we learned about models, we learned that [data layers](LINK) add abstraction between models and the data we want to store. With Entity FrameworkCore, data layers take the form of classes that extend `DbContext`. Models are NOT persistent data stores and relational databases do NOT shape the C# objects we will be using. We want to make sure that the two remain separate.

{{% notice blue "Note" "rocket" %}}

We’ll often shorten Entity Framework Core to EF. The “Core” in the name indicates that we’re talking about the version of EF that is compatible with ASP.NET Core.

{{% /notice %}}

## Adding ORM to `CodingEvents`

### Verify EF Core Tools are Present

EF 6.0.X is typically installed with Visual Studio 2022.

You can test that it has been installed by running the following in your terminal.

1. `cd` your way down into the project folders. Verify your location by running the `ls` command. You should see all the folders within your project.

   ```bash
   student-computer:CodingEvents student$ ls
   CodingEvents.csproj               ViewModels
   Controllers                       Views
   Data                              appsettings.Development.json
   Models                            appsettings.json
   Program.cs                        bin
   Properties                        obj
   Startup.cs                        wwwroot
   ```

1. When you are this level run the following command:

   ```bash
   dotnet ef
   ```

   You should see the followng output:

      ```bash
         student-computer:CodingEventsDemo student$ dotnet ef

                  _/\__
            ---==/    \\
      ___  ___   |.    \|\
      | __|| __|  |  )   \\\
      | _| | _|   \_/ |  //|\\
      |___||_|       /   \\\/\\

      Entity Framework Core .NET Command-line Tools 6.0.X

      //code continues ...
      ```

{{% notice blue "Note" "rocket" %}}

   We recommend using or installing EF Core version 6.0.11 or higher.

{{% /notice %}}   

### Troubleshooting EF Core Tools

If you are not able to see the Entity Framework Core logo, then try the following steps to troubleshoot the issue.

1. Open a terminal window using your terminal app outside of Visual Studio.

1. Open a terminal and run:

   ```bash
   dotnet tool install -g dotnet-ef
   ```
   This command installs a set of command-line tools for working with EF _globally_, which means it will be available for any ASP.NET project we use in the future. We will use the tools provided by this package to update our database schema after adding or changing model classes.

1. Once you have taken these steps, you are ready to set up the appropriate models and controllers for the application. We’ll do that in the next section.

1. To test that this install worked, run `dotnet ef`. The output should be a message displaying basic EF tool commands and options

   {{% notice blue "Note" "rocket"%}}
   **Note for Mac users only**

   For these tools to be accessible from the command line, they must be within your user path. We create or update your bash profile. Your bash profile is a text file that you can add any paths needed. You may add to this as you continue on your programming journey.

   1. Open your ~/.bash_profile with this command:

      ```bash
      open ~/.bash_profile
      ```

      The `~` symbol is shorthand for your home directory, which is the directory you are in when you open a new terminal window.

   1. Add the following line to the very bottom of your profile:
      ```bash
      export PATH="$PATH:$HOME/.dotnet/tools/"
      ```

   1. Save and close the file. Then close your terminal window and open a new one, so that the changes can take effect.

   1. To test that this install worked, run `dotnet ef`. The output should be a message displaying basic EF tool commands and options.
   {{% /notice %}}

Once you have taken these steps, you are ready to set up the appropriate models and controllers for the application. We’ll do that in the next section.

## Check Your Understanding

{{% notice green "Question" "rocket" %}}
   **True/False:** An ORM converts data between C# objects and relational databases.

   <!-- ans: True -->
{{% /notice %}}


{{% notice green "Question" "rocket" %}}
   **True/False:** We need Entity Framework Core AND a MySQL provider to successfully use ORM in this project.

   <!-- ans: True -->
{{% /notice %}}


