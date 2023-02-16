---
title: "Studio: Spa Day!"
date: 2023-02-09T12:48:24-06:00
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

After all of the hard work we have put into learning about Razor templates, it is time for a spa day. Let’s make an application to select some spa services.

Our application needs to do the following:

   1. Display the user’s name and skin type under their customer profile.
   1. Display the appropriate facial treatments for their skin type.
   1. Display the description of the spa’s manicures or pedicures depending on the user’s interest.

As always, read through the whole page before starting to code.

## Setup
Fork and clone the [starter code](LINK).

Once you have the project opened in your IDE, and run it and click the SpaDay link that appears in the upper left of the home page. You should see a small form at the `/Spa` route.

##  The Customer Profile

In `Controllers`, we have a controller called `SpaController`. Inside `SpaController` are three methods.

   1. `CheckSkinType()` method: Contains the logic to determine which facial treatments are appropriate for which skin type.

   1. `Index()` action method: Returns the `Spa/Index` view when `GET` requests are made to `/spa/`.

   1. `Menu()` action method: Returns the `Spa/Menu` view when `POST` requests are made to `/spa/`.

In `Views/Spa`, we have a Razor template called `Menu`. Inside `Menu.cshtml`, there are two `div` elements. Let’s add some children to the `div` with the `id`, `clientProfile`.

   1. Add an `h3` that says “Client profile”.

   1. Next, display the value of the `name` parameter from the form.


{{% notice green "Tip" "rocket" %}}
This is a two step process.

   1. In the controller, add a `ViewBag` property to hold the `name` value.

   1. In the view, use that `ViewBag` property to display the `name` in a `p` tag.
{{% /notice %}}

Run the application and head to `localhost:5001/spa` to see the results. When we fill out the form, we should see a new page with the client profile heading and name at the top.

## List All Appropriate Facial Treatments

To provide treatment suggestions, `SpaController.Menu()` uses the `CheckSkinType()` method and fills a list with facial treatments that benefit the user’s skin type. Now, we just need to use Razor to display the contents of the `appropriateFacials` list.

   1. Add the client’s `skintype` and the `appropriateFacials` list as a `ViewBag` property.

   1. Now, head back to `Menu.cshtml` and checkout the empty `div` with the `id`, `servicesMenu`.

   1. Pass in the `skintype` variable to the `<p>` tag.
   
      <!-- TODO: Link to loops chapter -->
   1. Iteratively add the values in `appropriateFacials` to an unordered list. If you need a quick reminder of the syntax, review the [@foreach section](LINK).

## Mani or Pedi?

We want to display a description for the nail service the user selects. Inside the `servicesMenu` div, use `@if` to determine if the value of `manipedi` is `"manicure"` or `"pedicure"`.

   1. If the value of `manipedi` is `"manicure"`, display this description:

      > Our manicure is a great way to spend 30 minutes of your day! We use shea butter hand cream and the finest gel polish.

   1. If the value of `manipedi` is `"pedicure"`, display this description:

      > Relax for 45 minutes in pure luxury! Our massage chairs and experienced nail techs are here to get your feet in shape for sandal season!

## End Result

After you are done with the studio, you should be able to fill out the form, click “Submit”, and see your profile page.

## Bonus Mission

1. Try adding an element to the bottom of the page with square shaped div elements. Each square should be a different color for different available nail polishes. At the base of the project is a folder called `wwwroot`. Inside of that is another folder called css. Modify the `site.css` file inside of it to get some CSS practice. There are already a number of style rules present so remember to be give your `div` elements class identifiers to give your elements specificity.

1. Modify the form to allow the user to select either a manicure or pedicure or both. If the user selects both, display both the manicure and pedicure descriptions in the `Menu` view.

1. Work with routes and paths to display the spa menu page on a separate route from the form.

