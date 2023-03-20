---
title: "Configuring Identity"
date: 2022-12-15T09:16:07-06:00
draft: false
weight: 5
originalAuthor: John Woolbright # to be set by page creator
originalAuthorGitHub: jwoolbright23 # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: 12/15/22 # UPDATE ANY TIME CHANGES ARE MADE
---

With Identity in place, we can start to configure the settings of the library to meet our authentication requirements. The first place to start with configuring Identity to fit the needs of the project is in `Program.cs`.

## `Program.cs`

Now that we are getting to configure our user, let's check out the code in `Program.cs`. Earlier you may have added the following:

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

This code is dictating the settings for account creation. Right now, for a user to create an account, they have to have the following:

1. They have to click a link to confirm their account.
1. Their password has to be more than 10 characters long.
1. Their password has to include an uppercase letter(s).
1. Their password does not have to include a number.
1. Their password does not have to include a special character such as a question mark.
1. Their password does not have to include lowercase letters.

These are just some basic requirements that can be changed to suit the needs of your application.
For a full list of the default settings for users' passwords and how we can change those settings, check out the [documentation](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.identity.passwordoptions?view=aspnetcore-6.0).

In `Program.cs`, we can also configure cookie settings, password hashers, user validation requirements, sign in settings and more.

## Additional Customizations

As you learn more about what Identity can do, you may find yourself wanting to customize it more and more to suit your needs!
Here are some examples of what you can do with it.

1. Customize user information
1. Customize user roles
1. Customize the UI
1. Add new settings to user passwords
1. Change the default settings around user sign-in

{{% notice blue "Note" "rocket" %}}
If you want to customize user data, it is best to do so when initially scaffolding the app.
[IdentityUser](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.identity.entityframeworkcore.identityuser?view=aspnetcore-1.1) has a number of properties that are important and relevant to storing user data.
However, when you read through the requirements you may notice that you need additional properties, such as the user's first and last name.
If you want to add custom properties, check out this [article](https://learn.microsoft.com/en-us/aspnet/core/security/authentication/add-user-data?view=aspnetcore-6.0&tabs=visual-studio) from Microsoft.
{{% /notice %}}
