---
title: "Exercises"
date: 2023-02-24T08:57:18-06:00
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

Let’s practice adding more properties to our event objects and validating them. Create a new branch from the [viewmodels](https://github.com/LaunchCodeEducation/CodingEvents/tree/viewmodels).

Below, we describe some new properties for you to add to the `Event` class. For each property, consider the following factors:

1. What will you call your property?
1. What type of input should be added to capture the field’s information from the user?
1. Refer to the chapter content to find appropriate attributes to fit the necessary constraints.
1. What should the error message convey to the user?
1. What, if anything, will you need to update on the controller to account for the new property?

Event information to add:

1. Add a property to collect information about where the event will take place. This property should not be null or blank.


   {{% expand "Check your solution" %}}
   ```csharp{linenos=table}
   // In the Event class

   public string Location { get; set; }

      //  In the Event constructor
      public Event( ... string location)
         {

               Location = location;

         }
   ```

   This property should not be null or blank.

   ```csharp{linenos=table}
   // In the AddEventViewModel class

   [Required(ErrorMessage = "Location information is required.")]
   public string Location { get; set; }
   ```

   {{% /expand %}}

1. Add a property to collect information about the number of attendees for the event. Valid values for this property should be any number between zero and 100,000.


1. Add columns for the location and number of attendees to the `Events/Index.cshtml` view.

   {{% expand "Check your solution" %}}
   ```html{linenos=table}
   <!-- inside your table -->
      <th>
         Location
      </th>
      <th>
         Number of Attendees
      </th>
      @foreach (var evt in Model)
      {
         <tr>
               <td>@evt.Id</td>
               <td>@evt.Name</td>
               <td>@evt.Description</td>
               <td>@evt.ContactEmail</td>
               <td>@evt.Location</td>
               <td>@evt.NumberOfAttendees</td>
         </tr>
      }
   </table>
   ```
   {{% /expand %}}



## Bonus Mission

Add a property to collect information about whether an attendee must register for the event or not. For the purposes of validation practice, make this property only able to be marked as true.

{{% notice green "Tip" "rocket" %}} 

In order to do this, you need to add an additional property called IsTrue to `AddEventViewModel` with the following code:

```csharp{linenos=table}
public bool IsTrue { get { return true; } }
```

With `IsTrue` in `AddEventViewModel`, you can use a `[Compare]` attribute to compare the value of the `IsTrue` property which is always true and the value of the property you add for registration requirements. The [documentation](https://learn.microsoft.com/en-us/dotnet/api/system.componentmodel.dataannotations.compareattribute?view=net-6.0) has more information on how the `[Compare]` attribute.

{{% /notice %}}

