---
title: "Models in MVC"
date: 2023-02-20T17:39:54-06:00
draft: false
weight: 1
originalAuthor: Sally Steuterman # to be set by page creator
originalAuthorGitHub: gildedgardenia # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

In the previous chapter, you learned about Razor, which displays data and an
interface for a user. Before that, you learned about [controllers]({{% relref "../../../aspdotnet-controllers-and-routes" %}}). Remember that controllers
determine what data to send to the the views. This data needs to come from some source 
and take some shape. Cue the models.

## What is a Model?

A **model** represents the logic for accessing and storing the data used in an application. 
Properly constructed, models do not depend on any controllers or views. Models should be classes that 
are easy to reuse without modification.

Models are not the data itself, but rather the logic that moulds the data for a particular
purpose. They dictate how we want to handle the data in an application-specific way. The data used in 
an application is often sourced from a database or an external data service. Data is typically 
application-agnostic. It is the work of the models we write to shape raw data into useful 
application information. This shaping of data to for the needs of a program is part of what is referred 
to as the **business logic**.

Consider a physical address book (a model). The pages contain blank lines for names and addresses. 
Anyone (a controller) can pick up the book, retrieve the information, and write to the contact. 
The address book model does not depend on who picks it up and enters their contacts. The book just 
provides organization and storage logic. On the flip side, the same person can input the same contact 
data into a different book. So a model transforms raw information  into something useful for a particular 
application.

## MVC: Putting it Together

![Diagram of the MVC flow showing summaries of responsibilities for the three components](pictures/mvcOverviewDetail.png)

### Model

Shapes data to fit the needs of an application.

### View

Displays data to the user. Via events, the user interacts with the view and updates the program 
data. The view communicates with the controller but not the model.

### Controller

Directs the flow of information between the view and the
model. It does not store the data or determine how to display it for the
user. It passes information retrieved from the view to update the model. 
And it passes information retrieved from the model to update the view.

{{% notice green "Tip" "rocket" %}}

   Need further review? Check out [MVC for Noobs](https://code.tutsplus.com/tutorials/mvc-for-noobs--net-10488).

{{% /notice %}}

## Model vs. Controller

At this point, it might be tough to decide what code belongs in the model and what belongs in the 
controller. Here are some general guidelines. Any code that transfers data or responds to user 
actions belongs in the controller. Code that retrieves data from a database or organizes that 
data belongs with the model.

So far, `CodingEvents` handles all data inside of controller classes. However, most 
data manipulation should occur in model classes. So we need to make a distinction between these 
actions. For any manipulations that must occur regardless of a user's actions, that code belongs 
in the model. For changes that vary depending on a user’s input, that code belongs in the controller.

Model code defines the logic for processes that the user never needs to see.
These include:

1. The mechanics for storing data.
1. The mechanics for retrieving data.
1. The mechanics for organizing data.
1. Updating or manipulating the data independent of any controller or view
   actions.

Controller code handles *requests* made by the user. These include:

1. "Please retrieve this information from the model.",
1. "Please store this according to the rules of the model.",
1. "Please delete this item.",
1. "Please change this item.",
1. "Please display this.",
1. "Please modify this data in a novel way".

Remember, the controllers are the traffic cops. These classes direct information from one place to 
another. Like a model, a controller does not permanently store data. Instead, it either sends the 
information to the model for shaping or to the view for display.

## Check Your Understanding

{{% notice green "Question" "rocket" %}}

   If we use baking as an analogy for an MVC project, which of the
   following items best represents a model?

   1. The bread ingredients: flour, water, yeast, salt
   1. Mixing and shaping the ingredients together
   1. Baking the loaves into the final product
   1. Eating the bread

{{% /notice %}}

<!-- b, Mixing and shaping the ingredients together -->

{{% notice green "Question" "rocket" %}}

   If we use a library as an analogy for an MVC project, which of the
   following items best represents a model?

   1. The books on the shelves
   1. The Dewey Decimal storage system
   1. The librarians
   1. The book readers

{{% /notice %}}

<!-- b, The Dewey Decimal storage system -->