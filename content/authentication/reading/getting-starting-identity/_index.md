---
title: "Getting Started with Identity"
date: 2022-12-15T09:16:07-06:00
draft: false
weight: 3
originalAuthor: John Woolbright # to be set by page creator
originalAuthorGitHub: jwoolbright23 # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: 12/15/22 # UPDATE ANY TIME CHANGES ARE MADE
---

As a developer, you may find yourself wanting to add Identity in one of the two following situations:

1. You are creating a new project and you know that you need Identity in the project.
1. You are working with an existing project and need to add Identity to continue your work.

For this chapter, we are going to focus on the second situation and how we might add Identity to `CodingEvents`.
The process of adding Identity to an existing code base is called **scaffolding**.

{{% notice blue "Note" "rocket" %}}
Try and code along as you read more about Identity!
<!-- TODO: Need to link proper repos to the below topics -->
This page starts off with the code in the [orm2 branch](https://github.com/LaunchCodeEducation/CodingEvents/tree/orm2) of the [CodingEvents](https://github.com/LaunchCodeEducation/CodingEvents) repository. 
The final code for this page is in the [authentication branch](https://github.com/gildedgardenia/CodingEvents/) of the [CodingEvents](https://github.com/LaunchCodeEducation/CodingEvents) repository.
{{% /notice %}}

## Before You Start

Before getting started, you need to make note of the version of .NET Core SDK your project is using. Inside the project directory, run the following command:

```bash
dotnet --info
```

When you run this command, the output may look something like the following:

```bash
.NET SDK (reflecting any global.json):
   Version:   6.0.403
   Commit:    2bc18bf292

Runtime Environment:
   OS Name:     Mac OS X
   OS Version:  12.4
   OS Platform: Darwin
   RID:         osx.12-x64
   Base Path:   /usr/local/share/dotnet/sdk/6.0.403/

global.json file:
   Not found

Host:
   Version:      6.0.11
   Architecture: x64
   Commit:       943474ca16
```

If the .NET Core SDK listed on line 2 does not match the SDK specified in your `csproj` file, you may need to open up your `global.json` and edit it so that the SDK used by the project matches.

{{% notice blue "Note" "rocket" %}}
If you do not have a `global.json` file, but the .NET Core SDK is still not matching your `csproj` file, you can create a new `global.json` file with the following command:

```bash
dotnet new globaljson --sdk-version 6.0.403
```
{{% /notice %}}

You need to install six NuGet packages before getting started with this process:

1. ``Microsoft.EntityFrameworkCore.Design``
1. ``Microsoft.AspNetCore.Identity.UI``
1. ``Microsoft.AspNetCore.Identity.EntityFrameworkCore``
1. ``Microsoft.EntityFrameworkCore.SqlServer``
1. ``Microsoft.VisualStudio.Web.CodeGeneration.Design``
1. ``Microsoft.EntityFrameworkCore.Tools``

You can install these packages using the NuGet package manager or the [.NET Core CLI](https://learn.microsoft.com/en-us/dotnet/core/tools/):

Below you will find examples of how to install them using the `.NET Core CLI`

{{% notice blue "Note" "rocket" %}}
Make sure to execute the following commands within your project directory *inside* of the solution.
{{% /notice %}}

When installing these packages, make sure that the versions are the same as the .NET Core version your project is using. You can confirm this is the case by reviewing the code in your `csproj` file. The below examples are all using `dotnet 6`

```bash
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design --version 6.0
```

```bash
dotnet add package Microsoft.EntityFrameworkCore.Design --version 6.0
```

```bash
dotnet add package Microsoft.AspNetCore.Identity.EntityFrameworkCore --version 6.0
```

```bash
dotnet add package Microsoft.AspNetCore.Identity.UI --version 6.0
```

```bash
dotnet add package Microsoft.EntityFrameworkCore.SqlServer --version 6.0
```

```bash
dotnet add package Microsoft.EntityFrameworkCore.Tools --version 6.0
```

With these packages installed, you are ready to go!

## Scaffolding Identity in an Exisiting Project

In both Visual Studio for Mac and Visual Studio for Windows, you have the option to add new scaffolded items through the UI and through the terminal.

### Adding Identity Through the UI

1. Right click on the project folder at the top of the solution.
1. Select *Add* > *New Scaffolded Item*.
1. From the menu, select *Identity*.

{{% notice blue "Note" "rocket" %}}
This approach is the simpler of the two approaches. However, for some Mac users, you may not find Identity as an option when you use this approach. If that is the case, use the cli method.
{{% /notice %}}

### Adding Identity through the Command Line

All of these commmands should be run in the project directory *inside* of the solution.

1. Use the following command to make sure you have the necessary code generator tools installed.

```bash
dotnet tool install --global dotnet-aspnet-codegenerator --version <YOUR .NET VERSION>

```

If the tool is installed, check the version before proceeding to make sure it works with your .NET version.

1. Now you are ready to add Identity to your project! You can configure Identity in any number of ways to fit the project requirements. To see all of the options use this command:

```bash
dotnet aspnet-codegenerator identity -h
```

When you use this command, you will see a menu of options in your terminal and can configure from there.

```bash
Usage: aspnet-codegenerator [arguments] [options]

Arguments:
   generator  Name of the generator. Check available generators below.

Options:
   -p|--project             Path to .csproj file in the project.
   -n|--nuget-package-dir   
   -c|--configuration       Configuration for the project (Possible values: Debug/ Release)
   -tfm|--target-framework  Target Framework to use. (Short folder name of the tfm. eg. net46)
   -b|--build-base-path     
   --no-build               

Selected Code Generator: identity

Generator Options:
   --dbContext|-dc       : Name of the DbContext to use, or generate (if it does not exist).
   --files|-fi           : List of semicolon separated files to scaffold. Use the --listFiles option to see the available options.
   --listFiles|-lf       : Lists the files that can be scaffolded by using the '--files' option.
   --userClass|-u        : Name of the User class to generate.
   --useSqLite|-sqlite   : Flag to specify if DbContext should use SQLite instead of SQL Server.
   --force|-f            : Use this option to overwrite existing files.
   --useDefaultUI|-udui  : Use this option to setup identity and to use Default UI.
   --layout|-l           : Specify a custom layout file to use.
   --generateLayout|-gl  : Use this option to generate a new _Layout.cshtml
   --bootstrapVersion|-b : Specify the bootstrap version. Valid values: '3', '4'. Default is 4.
```

1. Configuration of Identity is dependent on you and your project requirements. In the case of `CodingEvents`, you would want to continue to use `EventDbContext`.

This is how your final generation command would look:

```bash
dotnet aspnet-codegenerator identity --dbContext EventDbContext --files "Account.Register;Account.Login;Account.Logout;Account.RegisterConfirmation"
```

{{% notice blue "Note" "rocket" %}}
In the above command, we used the option for `files`. Identity is a Razor Class Library so it comes with Razor pages preconfigured for registration, login, etc. This option means that we want the scaffolder to generate these files and add them to the solution, making it easier for us to customize these files in the future. The option for `defaultUI` means that we have no need to have these files in the solution and so we won't have the ability to customize them. 
{{% /notice %}}

1. Once we run this series of commands, we will have successfully scaffolded Identity code onto our existing project.

{{% notice blue "Note" "rocket" %}}
If you do not see any new scaffolding, try using the command `dotnet restore`. This will restore our NuGet packages manually as opposed to them automatically restoring. 
{{% /notice %}}

### DbContext

If you tried to run the application right now, you would encounter some build errors. While we specified in our scaffolding commands that we wanted to use `EventDbContext`, we need to open up `EventDbContext` and make some changes.

In order to use Identity, we need to change what `EventDbContext` extends. Currently, it extends `DbContext`. Let's change that to `IdentityDbContext` like so:

```csharp
public class EventDbContext : IdentityDbContext<IdentityUser, IdentityRole, string>
```

We also need to add an additional line to ``OnModelCreating()``:

```csharp
base.OnModelCreating(modelBuilder);
```

With these changes made, `EventDbContext` will look like the following:    

```csharp {linenos=table}
using CodingEvents.Models;
using Microsoft.EntityFrameworkCore;
using Microsoft.AspNetCore.Identity;
using Microsoft.AspNetCore.Identity.EntityFrameworkCore;

namespace CodingEvents.Data
{
    public class EventDbContext : IdentityDbContext<IdentityUser, IdentityRole, string>
    {
        public DbSet<Event> Events { get; set; }

        public DbSet<EventCategory> Categories { get; set; }

        public DbSet<Tag> Tags { get; set; }

        public EventDbContext(DbContextOptions<EventDbContext> options) : base(options)
        {
        }

        protected override void OnModelCreating(ModelBuilder modelBuilder)
        {
            modelBuilder.Entity<Event>()
                .HasOne(p => p.Category)
                .WithMany(b => b.events);

            modelBuilder.Entity<Event>()
                .HasMany(p => p.Tags)
                .WithMany(p => p.Events)
                .UsingEntity(j => j.ToTable("EventTags"));
            base.OnModelCreating(modelBuilder);
        }
    }
}
```

You may note that we didn't add any `DbSet` for `IdentityUser` like we did for other models in the application. This is not an oversight! With `EventDbContext` properly set up, we can run a migration and the database will add the appropriate tables for our authentication data.

Add the following line to your `Program.cs` file:

```csharp
builder.Services.AddRazorPages();
```

{{% notice blue "Note" "rocket" %}}
While you are editing your `Program.cs` file, you may need to also add a default identity user. We will learn more about how to configure this user in a later section. For now, you can add code to `Program.cs` to address this:
{{% /notice %}}

```csharp {linenos=table}
builder.Services.AddDefaultIdentity<IdentityUser>
(options =>
{
   options.SignIn.RequireConfirmedAccount = true;
   options.Password.RequireDigit = false;
   options.Password.RequiredLength = 10;
   options.Password.RequireNonAlphanumeric = false;
   options.Password.RequireUppercase = true;
   options.Password.RequireLowercase = false;
}).AddEntityFrameworkStores<EventDbContext>();
```

You will also need to add a couple lines of code below `app.UseAuthorization();`

```csharp
app.MapRazorPages();
app.MapControllers();
```

`app.MapRazorPages();` specifies to the app that the Identity pages should follow the routing laid out in `_LoginPartial.cshtml`.

These initial steps were to make sure that the application is still using `EventDbContext` for its connection to the database now that we have added Identity. However, if you take a look inside the `Areas/Identity/Data` directory, you will find a file also called `EventDbContext`. Delete that generated file and continue to use the one we initially created for `CodingEvents`.

You will also need to remove the following line from your `Program.cs` file:

```csharp
using CodingEvents.Areas.Identity.Data;
```

The CodingEvents application already has a connection string in addition to using our builder to add database context configured. Since we also configured our own default `identity` user earlier in the walkthrough we can also safely remove that as well. You will need to remove the following lines of code from your `Program.cs` file that were generated when adding our identity scaffolding:

```csharp {linenos=table}
var connectionString = builder.Configuration.GetConnectionString("EventDbContextConnection");builder.Services.AddDbContext<EventDbContext>(options =>
    options.UseSqlServer(connectionString));builder.Services.AddDefaultIdentity<IdentityUser>(options => options.SignIn.RequireConfirmedAccount = true)
    .AddEntityFrameworkStores<EventDbContext>();
```

{{% notice blue "Note" "rocket" %}}
If you do not delete the above file you will most likely receive warnings about having two Database Context classes.
{{% /notice %}}

{{% notice blue "Note" "rocket" %}}
If you do not immediately see Identity scaffolding, that is okay! Sometimes it takes a moment to appear.

{{% /notice %}}

### Views

In your solution, you will find a new view inside the `Views/Shared` directory called `_LoginPartial.cshtml`. This partial view contains the logic for the links to actions that the users need, such as registration forms, login forms, sign out actions, and so on. If you peek inside the file, you will find these links live inside a conditional.

```csharp {linenos=table}
@using Microsoft.AspNetCore.Identity
@using CodingEventsDemo.Data

@inject SignInManager<IdentityUser> SignInManager
@inject UserManager<IdentityUser> UserManager

<ul class="navbar-nav">
@if (SignInManager.IsSignedIn(IdentityUser))
{
   <li class="nav-item">
      <a id="manage" class="nav-link text-dark" asp-area="Identity" asp-page="/Account/Manage/Index" title="Manage">Hello @UserManager.GetUserName(IdentityUser)!</a>
   </li>
   <li class="nav-item">
      <form id="logoutForm" class="form-inline" asp-area="Identity" asp-page="/Account/Logout" asp-route-returnUrl="@Url.Action("Index", "Home", new { area = "" })">
         <button id="logout" type="submit" class="nav-link btn btn-link text-dark">Logout</button>
      </form>
   </li>
}
else
{
   <li class="nav-item">
      <a class="nav-link text-dark" id="register" asp-area="Identity" asp-page="Account/Register">Register</a>
   </li>
   <li class="nav-item">
      <a class="nav-link text-dark" id="login" asp-area="Identity" asp-page="/Account/Login">Login</a>
   </li>
}
</ul>
```

[UserManager](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.identity.usermanager-1?view=aspnetcore-6.0) deals with the user information in the database. We can use the properties and methods to perform operations on user objects such as adding a new user or fetching user information. On line 11 in the code above, `UserManager` is used to fetch the signed-in user's username so we greet them by name! [SignInManager](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.identity.signinmanager-1?view=aspnetcore-6.0) deals with users signing in. On line 8, `SignInManager` is used to check if the user is signed in. If the user is signed in, then the links that will be displayed are to manage the account or log out of the account. If the user is not signed in, then the links are to either log in or register for an account on the site.

This partial view can be placed anywhere you need it, but we recommend starting with placing it in `_Layout.cshtml` so that a signed-in user can easily access the necessary links from any page. To add it to the navbar, use the following syntax:

```html
<partial name="_LoginPartial" />
```

Add the above line of code to the following code block:

```html {linenos=table, hl_lines=[22]}
 <div class="navbar-collapse collapse d-sm-inline-flex justify-content-between">
   <ul class="navbar-nav flex-grow-1">
      <li class="nav-item">
            <a class="nav-link text-dark" asp-area="" asp-controller="Events" asp-action="Index">All Events</a>
      </li>
      <li class="nav-item">
            <a class="nav-link text-dark" asp-area="" asp-controller="Events" asp-action="Add">Add Event</a>
      </li>
      <li class="nav-item">
            <a class="nav-link text-dark" asp-area="" asp-controller="EventCategory" asp-action="Index">All Event Categories</a>
      </li>
      <li class="nav-item">
            <a class="nav-link text-dark" asp-area="" asp-controller="EventCategory" asp-action="Create">Add Category</a>
      </li>
      <li class="nav-item">
            <a class="nav-link text-dark" asp-area="" asp-controller="Tag" asp-action="Index">All Tags</a>
      </li>
      <li class="nav-item">
            <a class="nav-link text-dark" asp-area="" asp-controller="Tag" asp-action="Add">Add Tag</a>
      </li>
   </ul>
   <partial name="_LoginPartial" />
```

### Final Steps

<!-- TODO: Determine if the below is still accurate -->
No matter which approach you took for the initial steps in scaffolding, you need to run a new migration and update your database.
Once you update the database, your database will contain a number of tables related to Identity such as `AspNetUsers` and `AspNetRoles`.

To test that you are on the right track, run the application. Click on the link to register and create a new account.
Query the `AspNetUsers` table in the database to make sure that the newly added account is there.

Now that we have successfully added Identity to our project, we are ready to start coding!

