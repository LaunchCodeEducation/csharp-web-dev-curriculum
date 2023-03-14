---
title: "Setting Up a Persistent Database"
date: 2023-03-10T09:32:46-06:00
draft: false
weight: 2
originalAuthor: Courtney Frey # to be set by page creator
originalAuthorGitHub: speudusa # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---
<!-- TODO: Link back to MySQL book for refresher -->
To get started with using a relational database with our MVC applications, we need to first [set up a new database](https://education.launchcode.org/SQL/chapters/mysql-part-1/exercises.html) in MySQL Workbench.

In MySQL Workbench, do the following:

1. Create a new schema, `coding_events`.

1. Add a new user, `coding_events`, with a new password. Give the user all privileges to modify your new schema.


**UPDATE PROGRAM.CS**

```csharp{linenos=table,hl_lines=[],linenostart=1}

//CODE HERE FOR CONNECTING TO DATABASE

```

We now need to add a couple of NuGet packages to support our database connection. This process differs slightly for Windows and MacOS users.

###  Install MySQL Dependency

Working with the NuGet Package Manager

Open the NuGet Package Manager in Visual Studio:

 - **Windows** - Tools > NuGet Package Manager > Manage NuGet Packages for Solution

- **Mac** - Project > Manage NuGet Dependencies

Search for for all of the packages listed below. Select the package and install.

When installing these packages, make sure that the versions are the same as the .NET Core version your project is using. You can confirm this is the case by reviewing the code in your csproj file.

We will need to install the following NuGet packages:

1. `Pomelo.EntityFrameworkCore.MySql`. This dependency provides code that is able to connect to a MySQL database from within an ASP.NET Core application using EF. 

1. `Microsoft.EntityFrameworkCore.Relational`. This is a mapping framework that automates access and storage of data in your project’s database.

1. `Microsoft.EntityFrameworkCore.Design`. This helps manage data migrations and the design-time logic. 

{{% notice green "Tip" "rocket"%}}
   You can view installed packages and their dependencies by navigating to _Dependencies > NuGet_ in the Solution Explorer (or the Solution pane on Mac) and expanding a given package.
{{% /notice %}}


## Ensuring Connection Success and Security

Before we can get into the ins and outs of using ORM, we need to make sure that our application has a corresponding database and that our application is ready to connect to MySQL. We can start to do this by creating new schemas and setting user privileges in MySQL Workbench. We also _must_ make sure that the MVC application has the correct dependencies, username, and password to access the schema.

If we do not do these steps, then our application will not be able to use a persistent data source.

Setting the value of the `connectionString` property using the values of the username and password is NOT a best practice. We regularly commit our code to Github, meaning anyone who reads the code in our repository can see the username and password. While you can do it for the applications in this class, you do not want to do it in the future.

{{% notice blue "Note"  "rocket"%}}
   To avoid this in the future, you can configure your `connectionString` string to reference environment variables. You then hide the appropriate info by setting the environment variable’s value equal to the password, for example.
{{% /notice %}}

See Microsoft [documentation](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/configuration/?view=aspnetcore-6.0#environment-variables) to learn how to keep the username and password to your database safe and secure.

## Check Your Understanding

{{% notice green "Question" "rocket" %}}
   **True/False:** Writing usernames and passwords in plain text in a file is a GREAT idea!

   <!-- ans: False -->
{{% /notice %}}