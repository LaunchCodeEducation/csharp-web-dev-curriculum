---
title: "Accessing Data"
date: 2023-03-10T09:32:46-06:00
draft: false
weight: 3
originalAuthor: Courtney Frey # to be set by page creator
originalAuthorGitHub: speudusa # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

Now that we have connected our C# application to a MySQL database, we need to set up our C# code to interact with the new schema. In the previous chapters, we learned about performing basic operations on a database and its tables, such as creating, reading, updating, and deleting rows. One of the reasons we use ORM is so that now we can write C# code in our application to manage our relational database.

While classes determine the structure of a table in our relational database, a **data store** does the work of inserting, updating, and retrieving data from the database.

In our work so far, we have been using an in-application data store. This is the class `EventData`. The `EventData` class is an **in-memory data store**. It keeps track of new events using a C# data structure, which gets deleted from memory every time the app shuts down. With EF, we can create a **persistent data store**. A persistent data store retains data even when an app shuts down.

## Creating a `DbContext`

We are going to use the `DbContext` class.  [This class](https://learn.microsoft.com/en-us/dotnet/api/system.data.entity.dbcontext?view=entity-framework-6.2.0) works with databases to track and manage changes in our stored data.  

### Create `EventDbContext` Class
1. In the `Data` directory, create a new class called `EventDbContext`. 

   By convention, we name it `EventDbContext` since it is going to be used to work with Event objects and data.

1. To create a persistent data store for our `Event` class, we can extend the class `DbContext`, which is provided by EF. This will provide the base functionality we need.

   {{% notice blue "Check Your Code" "rocket" %}}
   ```csharp
   public class EventDbContext : DbContext
   ```
   {{% /notice %}}

   This class needs a `using Microsoft.EntityFrameworkCore;` statement.  Visual Studio's Intellisense should automatically add it for you.


1. `DbContext` is often paired with `DbSet<Entity>` which represents the collection of all entities of a given type that can be queried from the database.

   We are going to create a `DbSet<Entity>` of `Event` types and name it `Events`. This will allow us to query `Event` objects once our database is created.

   `DbSet<Events>` will need access to the `Event` Model class.  Make sure you provide the appropriate using statement.
   

   {{% notice blue "Check Your Code" "rocket" %}}
   ```csharp{linenos=table,hl_lines=[1],linenostart=9}
   public DbSet<Event> Events { get; set; }

   public EventDbContext()  
   {
   }
   ```
   {{% /notice %}}   

1. We want to the `EventDbContext` constructor to extend `DbContextOptions`.  This will configure the data store.  

   {{% notice blue "Check Your Code" "rocket" %}}
   ```csharp{linenos=table,hl_lines=[10,11],linenostart=1}
   using CodingEvents.Models;
   using Microsoft.EntityFrameworkCore;

   namespace CodingEvents.Data
   {
      public class EventDbContext : DbContext
      {
         public DbSet<Event> Events { get; set; }

         public EventDbContext(DbContextOptions<EventDbContext> options)
               : base(options)
         {
         }
      }
   }

   ```
   {{% /notice %}} 

This basic data store template can be used for _any_ class that you want to persist in a database. Each such class will need its own data store.


## Registering a Data Store

To make ASP.NET aware of this data store, we need to register `EventDbContext` in the `Program class`. `Program` is automatically executed every time our app starts up, and is a place where application configuration can be customized.

A persistent data store is considered a service in ASP.NET. We need register this service by applying the following code to `Program.cs`:

   ```csharp{linenos=table,hl_lines=[],linenostart=12}
      builder.Services.AddDbContext<EventDbContext>(dbContextOptions => dbContextOptions.UseMySql(connectionString, serverVersion));
   ```

This code adds EF Core as a service to our `CodingEvents` application.   Using the `AddDbContext<EventDbContext>(...)` to configure the `CodingEvents` database context options.

The `MySql()` method is passed the `connectionString` and `serverVersion` variables which provide us access to the correct database.  A single application may have multiple database connections. 

When `WebApplication.CreateBuilder(args);` runs in line 5 of `Program.cs`, the connection to the database begins. 

## Configuring a Primary Key

As you [learned previously](https://education.launchcode.org/SQL/chapters/mysql-part-2/relationships.html#table-keys), every relational table should have a primary key. When working with ORM, this means that every **persistent class** needs a primary key property. A persistent class is a class that we want to store (or persist) in a database.

Our `Event` class currently has an ID field.

```csharp{linenos=table,hl_lines=[],linenostart=16}
   public int Id { get; }
   static private int nextId = 1;

   public Event()
   {
      Id = nextId;
      nextId++;
   }

   public Event(string name, string description, string contactEmail) : this()
   {
      Name = name;
      Description = description;
      ContactEmail = contactEmail;
   }
```

When introducing this property previously, we intentionally named it `Id` in anticipation of using EF and a data store to persist `Event` objects. EF will _automatically_ configure any property named `Id` to be the primary key for that class. Therefore, we already have the necessary property!

So the code sample above can be simplified to the following.

```csharp{linenos=table,hl_lines=[],linenostart=16}
   public int Id { get; set; }

   public Event()
   {
   }

   public Event(string name, string description, string contactEmail)
   {
      Name = name;
      Description = description;
      ContactEmail = contactEmail;
   }
```

{{% notice orange "Warning" "rocket" %}}
Be sure to update your `Event` class to match the simplified codeblock above before you move on to the next section.
{{% /notice %}}


## Migrations

Our application is now completely configured to store `Event` objects in our MySQL database. However, if you look at the `coding-events` database, you’ll notice that it has no table in which to store such data. To create such a table, we need to create and run a **database migration**. A database migration (or migration, for short) is an update to a database made in order to reflect changes in an application’s model. Every time we change our application’s model by adding or removing a new persistent class, or by modifying a persistent class, we will need to create and run a migration.

The EntityFrameworkCore Tools package we installed in the last section provides tools for working with migrations. To get started, open a terminal (the Terminal app on MacOS or Powershell on Windows). Navigate to the `CodingEvents` [project folder]({{< relref "../orm-intro/#verify-ef-core-tools-are-present" >}}) _within_ your `CodingEvents` solution. 

Then run the following command to create a migration:

   ```bash
   $ dotnet ef migrations add InitialMigration
   ```

This instructs the EF tools to create a migration named `InitialMigration`. In doing so, EF scans our project looking for persistent classes (i.e. classes with data stores that have been registered in Startup) and compares them to the current state of the MySQL database. If any classes have been added, removed, or changed, it will generate code to update the database to be in sync with the application’s model. This code is stored in the `Migrations/` folder of your project.

In order to run a migration, we issue the command:

   ```bash
   $ dotnet ef database update
   ```

This command will apply the changes to the database. To verify the changes, open MySQL Workbench and notice that there is now an `Events` table with columns corresponding to the properties of our class.

{{% notice blue "Note" "rocket" %}}
EntityFrameworkCore uses the `_EFMigrationsHistory` table in the database to keep track of which migrations have already been run. When we run `dotnet ef migrations update`, EF will reference this table and run all migrations that have not yet been applied, in the correct order.
{{% /notice %}}

The next section will look at how we can store and retrieve `Event` objects from within our controller.



## Check Your Understanding

{{% notice green "Question" "rocket" %}}
   **True/False:** Every persistent class will automatically have a MySQL table created to use to store its data.

   <!-- ans: False - we have to use a migration to create the table
 -->
{{% /notice %}}

{{% notice green "Question" "rocket" %}}
   A data store should extend which of the following classes in the ``Microsoft.EntityFrameworkCore`` package?

   1. `DataStore`
   1. `DbContext`
   1. `MySqlStore`
   1. None of the above

   <!-- ans: `DbContext` -->
{{% /notice %}}