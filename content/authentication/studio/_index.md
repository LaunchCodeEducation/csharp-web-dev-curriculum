---
title: "Studio: TechJobs Authentication"
date: 2022-12-15T09:16:07-06:00
draft: false
weight: 19
originalAuthor: John Woolbright # to be set by page creator
originalAuthorGitHub: jwoolbright23 # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: 12/15/22 # UPDATE ANY TIME CHANGES ARE MADE
---

For this studio, you'll be tasked with adding simple user authentication to your `TechJobs` application. The steps to do this will match what you have already done in `CodingEvents`. You should refer back to the tutorial starting [here](https://education.launchcode.org/csharp-web-dev-curriculum/authentication/reading/getting-starting-identity/).

1. [Scaffolding](https://education.launchcode.org/csharp-web-dev-curriculum//authentication/studio/#scaffolding)
1. [Configuration](https://education.launchcode.org/csharp-web-dev-curriculum//authentication/studio/#configuration)
1. [Authorization](https://education.launchcode.org/csharp-web-dev-curriculum//authentication/studio/#authorization)

## The Starter Code

1. Fork and clone the starter code for 
[TechJobsAuthentication](https://github.com/LaunchCodeEducation/TechJobsAuthentication).

1. You will need to do some work to ensure that the user, and database password match your own local MySQL setup.

1. Open `Program.cs` and update the following code:

   ```csharp
   var connectionString = "server=localhost;user=your_username;password=your_password;database=techjobs_auth";
   ```

4. Before getting started with setting up Identity, run a new migration to make sure that all of the database info is correct.

{{% notice blue "Note" "rocket" %}}
We've greatly reduced the functionality of the app so you can focus on the work to set up authentication. Running the application now 
gives you a familiar-looking navbar with one menu option, *Add Jobs*. You can add jobs right away and an astute observer of the starter code and schema tables will notice that the fields on `Job` are only strings, not complex objects.
{{% /notice %}}

## Scaffolding

1. In the project you have cloned, scaffold Identity onto the codebase.

- Use the same files as the chapter content and `JobDbContext`.

1. Update `Program.cs` and `JobDbContext` as necessary.
1. Add the `LoginPartial` partial view to the navbar.
1. Run a new migration and test the application.

## Configuration

1. Use the appropriate methods to set the following validation conditions on the password:

- The password must be at a minimum of 8 characters.
- The password does NOT need to contain an uppercase letter.

1. Complete any additional necessary configuration steps in `Program.cs`.

## Authorization

1. Add the necessary attributes so only logged-in users can add jobs, but all visitors to the application can see the listing of jobs.

{{% notice blue "Note" "rocket" %}}
You will need to implement the `using Microsoft.AspNetCore.Authorization;` inside of your Controller class in order for the [Authorize] and [AllowAnonymous] to work properly.
{{% /notice %}}

That's it, that's all. You're done. Go forth and test the auth flow by visiting the home page, registering for a new account, and logging into and out of an existing account. Then add this to any other ASP.NET project you're working on!

