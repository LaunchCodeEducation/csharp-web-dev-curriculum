---
title: "Task 2: Adding Employers"
date: 2023-01-05T13:58:39-06:00
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

## ViewModels

1. Create a new ViewModel called `AddEmployerViewModel` that has 2 properties: `Name` and `Location`.  For this application, an employer can only have one location.
1. Add validation to both properties in the ViewModel so that both properties are required. The depth of your validation is up to you.  
1. This class does not need a constructor.

## Controllers

`EmployerController` contains four relatively empty action methods. Take the following steps to handle traffic between the views and the model:
   1. Set up a private `JobDbContext` variable so you can perform CRUD operations on the database. Pass it into a `EmployerController` constructor.
   1. Complete `Index()` so that it passes all of the `Employer` objects in the database to the view. 
   1. Create an instance of `AddEmployerViewModel` inside of the `Add()` method and pass the instance into the `View()` return method.
   1. Add the appropriate code to `ProcessAddEmployerForm()` so that it will process form submissions and make sure that only valid `Employer` objects are being saved to the database.
      1. You want to add a new employer if the model is valid.  
      1. Else redirect users back to the form
   1. `About()` takes an id as a parameter.  It will create an `Employer` object by searching through the Employers table in `DbContext` until it finds the provided id.  It will pass the employer object to the view.
      1. Consider using the `.Find()` method to search the database.

## Views

The starter code comes with 3 views in the `Employer` subdirectory. Read through the code in each view.  You may have to add models or make sure naming is consistent between the controller and the view.  Make sure you are using your new `AddEmployerViewModel` and its validation where necessary.
1. `About` View: Use the Model to help populate the view 
1. `Add` View:  Use tag helpers to use the `AddEmployerViewModel`’s validation
1. `Index` View: Create a way to add a new employer on this View.

## Model

We need to create a `List` of `Job` objects named `Jobs` in the `Employer` model.  Make sure it has both a getter and a setter.

## Adding a Job

One important feature of your application is a form to add a new job. Two action methods in `JobController`, `Add()` and `ProcessAddJobForm()`, will work together to return the view that contains the form and handle form submission. In the `Job` subdirectory in Views, you will find an `Add.cshtml` file which contains the beginning of the form. Right now, the form only has one field for the job’s name. As you work on the application, you will add more fields to this form to add employer and skill info.

1. Create a new ViewModel called `AddJobViewModel`. You will need properties for the job’s name, the selected employer’s ID, and a list of all employers as `SelectListItem`.  Make sure that the name of a job is required.

   {{% notice blue Note "rocket" %}}
   This is different from the given ViewModel, `JobDetailViewModel`. `JobDetailViewModel` has properties for the selected employer’s info and the selected skill’s info. `AddJobViewModel` will have properties for all of the employers and skills in the database once you complete task 3. We need both ViewModels for the application. 
   {{% /notice %}}

1. Back in the `JobController`, find the `Add()` method.  
   1. This method needs to contain a list of Employer objects which it pulls from the Employers dbContext.
   1. This method needs to create an instance of the `AddJobViewModel` which is passed the list of employer objects.
   1. Pass an instance of AddJobViewModel to the view.  
1. In `Add.cshtml` view, add a new `<div class="form-group">` element to the form. Add the appropriate `<label>` and `<input>` tags to the new `<div>` element to create the form field to add employer information to the job. This field should be a dropdown menu with all of the employers in the database. In addition, add a link to the `<div>` element to add new employers. This way, if a user doesn’t see the employer they are looking for, they can easily click on the link and add a new employer to the database.

1. Back in the `JobController`, rename `ProcessAddJobForm()` to `Add()` and add the `[HttpPost]` attribute to designate this as your post handler.  
   1. This post handler needs to take in an instance of `AddJobViewModel` and make sure that any validation conditions you want to add are met before creating a new Job object and saving it to the database.
   1. If model is valid, redirect to the `“/Jobs”`.

## Create the One-to-Many Relationship

In the `JobDbContext`, we need to add the following to the `OnModelCreating()` method:

```csharp {linenos=table}
modelBuilder.Entity<Job>()
   .HasOne(p => p.Employer)
   .WithMany(b => b.Jobs);
```
This will create the many-to-one relationship between `Jobs` and `Employers`.

{{% notice blue "Progress Check" "Rocket" %}}
**Project Check:**
   - You should be able to add an employer.
   - You should be able to add a job with your new employer.
   - You should be able to create many new jobs for a single employer.

**Database:**  Check your data by adding employers to jobs. 
   - You should see employers in the `Employers` table.  
   - You should see Employer IDs in the `Jobs` table. 
   - You should see jobs in the `Jobs` table.

**Troubleshooting Tips**
   - If your database is not updating, try running a new migration followed by an update.

{{% /notice %}}

## Test It with SQL

Before you move on, try out your application now to make sure it runs as expected. You should be able to create Employer objects and view them both in the browser and in your database.
1. Open MySQL Workbench and make sure you have an `Employers` table and that it is empty. 
1. Start up your application – don’t forget to have your SQL server running – and go to the `Add` `Jobs` view.
1. You won’t be able to add a job yet, but you’ll see a link to `Add Employers` in the form. Click on it and proceed to check the functionality of the form that follows.
1. Be sure to test your validation requirements and error handling.

### SQL Task 2
In `queries.sql` under "Task 2”, write a query to list the names of the employers in St. Louis City.

{{% notice green Tip "rocket" %}}

If everything seems to work – that is, you are able to submit the form without any errors – but you don’t see your employers in the list after submission, here’s what you should check:
1. Is there any data in the `Employers` table? Check by going to MySQL Workbench and looking for the employer data within your schema.
1. If there’s data in the database, check that you are correctly querying for the list of all objects in the controller Are you calling for the proper list with `DbContext`?
1. Ensure you’re passing the list into the view.

{{% /notice %}}

You are ready to move onto [Task 3]({{< relref "../task-3/" >}}).