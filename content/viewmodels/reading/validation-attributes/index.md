---
title: "Validation Attributes"
date: 2023-02-24T08:57:18-06:00
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
Within the ViewModel or model of a C# web application, we can define validation rules using attributes. Validation attributes can be applied to model fields.

## Common Attributes

We’ll use only a few of these attributes, but you can find a full list in the [documentation](https://learn.microsoft.com/en-us/aspnet/core/mvc/models/validation?view=aspnetcore-6.0#built-in-attributes).


| Annotation  | Description | Syntax |
| ----------- | ----------- | ----------- |
| `[Required]`     | Specifies that a field cannot be null       | `[Required]`       |
| `[Range] `       | Specifies the range of potential values of a numeric field.        | `[Range(0,100)]`       |
| `[StringLength]` | Specifies the maximum length of a string field. Has additional optional parameters to specify the minimum length of a string field.       | `[StringLength(100)]`       |
| `[EmailAddress]` | Specifies that a string field should conform to email formatting standards.        | `[EmailAddress]`        |

{{% notice blue "Example" "rocket" %}}
To apply the validation rules of the example on the previous page to the fields of an `AddUserViewModel` class, we can use `[StringLength]` and `[Required]`.

   ```csharp{linenos=table,hl_lines=[],linenostart=1}
   [Required]
   [StringLength(12, MinimumLength = 3)]
   public string? Username { get; set; }

   [Reguired]
   [StringLength(20, MinimumLength=6)]
   public string? Password { get; set; }
   ```
{{% /notice %}}

## Defining Validation Messages

Each of these attributes takes an optional `ErrorMessage` parameter that allows you to define a user-friendly description to be used when validation fails.

{{% notice blue "Example" "rocket" %}}
To apply the validation rules of the example on the previous page to the fields of an `AddUserViewModel` class, we can use `[StringLength]` and `[Required]`.

   ```csharp{linenos=table,hl_lines=[],linenostart=1}
   [Required(ErrorMessage = "Username is required")]
   [StringLength(12, MinimumLength = 3, ErrorMessage = "Username must be between 3 and 12 characters long")]
   public string? Username { get; set; }

   [Required(ErrorMessage = "Password is required")]
   [StringLength(20, MinimumLength = 6, ErrorMessage = "Sorry, but the given password is too short. Passwords must be at least 6 characters long.")]
   public string? Password { get; set; }
   ```
{{% /notice %}}

We will see how to ensure these error messages are properly displayed in the next section, [Validating Models in a Controller]({{< relref "../controller-validation/" >}}).

## Applying Validation Attributes

To configure validation on the model-side, we begin by adding validation attributes to each field to which we want to apply constraints.

For our `AddEventViewModel` class: 

1. Add `[StringLength]` and `[Required]` to the `Name` property.

- Starting with the `[Required]` attribute, create an error message that informs a user they need to provide the name of an event.
   
- For the `[StringLength]` requirement, maybe put a max of 50 characters and minimum of 3.  A message to inform the user of these requirements could be nice.

2.  For the `Description` property, make it `[Required]` and have a longer `[StringLength]` than `Name`.

- Provide an error message for the `[Required]` statement that informs a user it is important to provide some description of the event.
   
- `[StringLength]` for `Description` should be longer than for `Name`.  However, you should set a limit on how many words a user can provide.  Make sure that you provide an error message that will inform them if they add too much.
   
   ```csharp{linenos=table,hl_lines=[],linenostart=8}
   [Required(ErrorMessage = "Name is required.")]
   [StringLength(50, MinimumLength = 3, ErrorMessage = "Name must be between 3 and 50 characters.")]
   public string? Name { get; set; }

   [Required(ErrorMessage = "Please enter a description for your event.")]
   [StringLength(500, ErrorMessage = "Description is too long!")]
   public string? Description { get; set; }
   ```

Not adding a `[Required]` attribute onto a property would make the field optional to the form submission.

The required `MaximumLength` and optional `MinimumLength` parameters for `[StringLength]` specify the maximum and minimum number of allowed characters, respectively. Omitting the minimum length requirement means that no min or max will be applied for the field. 



Each of our attributes also receives an `ErrorMessage` parameter. This parameter provides a user-friendly message to display to the user if the particular validation rule fails. We will see how to display these in a view a bit later.

Next, we add a new property to store a contact email for each event. This is a `string` named `ContactEmail`. Validating email addresses by directly applying each of the rules that an email must satisfy is _extremely_ difficult. Thankfully, there is an `[EmailAddress]` validation attribute that we can apply to our new field.

   ```csharp{linenos=table,hl_lines=[],linenostart=16}
   [EmailAddress]
   public string? ContactEmail { get; set; }
   ```

Before we can start up our application, we need to add a new input to our form in `Events/Add.cshtml` to take in the contact email for an event organizer. We want to provide the text a user will see for providing us with a contact email. The reflected value would not include the space between "Contact" and "Email".

   ```html{linenos=table,hl_lines=[],linenostart=14}
   <div class="form-group">
      <label asp-for="ContactEmail">Contact Email</label>
      <input asp-for="ContactEmail" />
   </div>
   ```
   
We also need to add a new column to the `Events/Index.cshtml` template to make `ContactEmail` visible.

   ```html{linenos=table,hl_lines=[],linenostart=20}
   <table class="table">
      <tr>
         <th>
            Id
         </th>
         <th>
            Name
         </th>
         <th>
            Description
         </th>
         <th>
            Contact Email
         </th>
      </tr>

      @foreach (var evt in Model)
      {
         <tr>
            <td>@evt.Id</td>
            <td>@evt.Name</td>
            <td>@evt.Description</td>
            <td>@evt.ContactEmail</td>
         </tr>
      }
   </table>
   ```

Now we can start up our application and test. Submitting an empty form at `/Events/Add` still results in an event being created, which may not be what you were expecting.

Rather than a bug, this is expected behavior. Validation involves both the model and controller, but we have not modified the controller in any way. Validation attributes simply define the validation rules that _should_ be used to check data. The responsibility of checking the data before saving a new event lies with the controller.

In the next section, we’ll modify the controller to properly check for valid data.

## Check Your Understanding

{{% notice green  "Question" "rocket" %}} 

True or False: When using `[StringLength]` you must provide both minimum and maximum length arguments.

<!-- ans: False, only maximum length is required. -->
{{% /notice %}}

{{% notice green  "Question" "rocket" %}} 

True or False: Adding validation attributes to a model ensures that bad data is not saved.

<!-- ans: False, server-side validation requires cooperation from attributes on the model, as well as controller logic -->
{{% /notice %}}