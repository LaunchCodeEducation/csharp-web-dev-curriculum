---
title: "Types of Relationships"
date: 2022-12-15T09:16:07-06:00
draft: false
weight: 1
originalAuthor: John Woolbright # to be set by page creator
originalAuthorGitHub: jwoolbright23 # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: 12/15/22 # UPDATE ANY TIME CHANGES ARE MADE
---

## Types of Relationships

<!-- TODO: Need to Correct Link here below to mysql-part-2 chapter/relationships -->
Just as database tables [can relate]() to each other, so can classes and objects. In fact, ORM translates relationships between objects into relationships between database rows.

This chapter introduces the tools needed to create meaningful relationships using ORM. Let's consider the different types of relationships at a conceptual level. In later sections, we will learn how to implement these relationships using EntityFrameworkCore.

For the examples below, we use four classes:

- `Event` - A class representing a coding event.
- `EventCategory` - A class representing categories of coding events.
- `EventDetails` - A class that encapsulates details about a single event, such as description, contact email, location, and so on.
- `Tag` - A piece of metadata labeling an event. You can think of these as topics that an event might include, such as C#, ASP.NET, or JavaScript. An event can cover many topics, so it can have many tags.

The first two of these are familiar to you from our ``CodingEvents`` app. The ``EventDetails`` and ``Tag`` classes are new.

### One-to-One

The simplest type of relationship is the **one-to-one relationship**. 

This occurs when each instance of type A may be related to only one instance of type B, and vice versa.

{{% notice blue "Note" %}}
In the following examples, arrows point in the direction of the relationship. If A points to B, then you can say that A *knows about* B.

While relationships in SQL are bidirectional, relationships in programming languages are unidirectional. In other words, if A knows about B, then B doesn't necessarily know about A.
{{% /notice %}}

![A single Event object on the left, with a double-sided arrow point to a single EventDetails object on the right](pictures/one-to-one.png?classes=border)

A one-to-one relationship between an ``Event`` object and an ``EventDetails`` object

An ``Event`` object should only have one collection of details, so it should only be related to one ``EventDetails`` object. 

Similarly, details about an event are specific to that event, so an ``EventDetails`` object should only be related to one ``Event`` object.

{{% notice blue "Examples"  %}}
The following pairs of things generally have one-to-one relationships:

1. `People / driver's licenses`
1. `States / capital cities`
1. `iPhones / serial numbers`

It is not *required* that each instance of type A be related to an instance of type B. For example, a person may not have a driver's license.
{{% /notice %}}

### One-to-Many and Many-to-One

A **one-to-many** relationship occurs when each instance of type A may be related to more than one instance of type B, but each instance of B can only be related to a single instance of type A.

![A single EventCategory object on the left, related to two Event objects on the right](pictures/one-to-many.png?classes=border)

A one-to-many relationship between `EventCategory` and `Event` objects

In this case, we say that A has a one-to-many relationship to B. A category can contain multiple items, therefore an `EventCategory` object may be related to multiple `Event` objects. But an event may only be in one category.

{{% notice blue "Examples" %}}
The following pairs of things generally have one-to-many relationships:

1. `Birth dates / people`
1. `States / U.S. Representatives`
1. `Model numbers / iPhones`
{{% /notice %}}

When discussing the inverse relationship, we say that B has a **many-to-one** relationship to A.

![Two Event objects on the left, related to a single EventCategory object on the right](pictures/many-to-one.png?classes=border)

A many-to-one relationship between `Event` and `EventCategory` objects

A many-to-one relationship operates in the opposite direction of a one-to-many relationship. 

The difference between the two is which side of the relationship *knows about* the objects on the other side. 

In C# terms, this will translate into a property on one class that references the other.

{{% notice blue "Examples" %}}
Many-to-one relationships are simply the opposite direction of one-to-many. Therefore, each of the following pairs has a many-to-one relationship.

1. `People / birth dates`
1. `U.S. Representatives / states`
1. `iPhones / model numbers`
{{% /notice %}}

### Many-to-Many

**Many-to-many** relationships occur when each instance of type A can be related to multiple instances of type B, and vice versa. 

![Three Event objects on the left, with various relationships to three Tag objects on the right](pictures/many-to-many.png?classes=border)

A many-to-many relationship between Event and Tag objects

An event can have multiple tags, and a tag may be associated with multiple events. Thus, we have a many-to-many relationship.

{{% notice blue "Examples" %}}
The following pairs of things generally have many-to-many relationships:

1. `Books / authors`
1. `Recipes / ingredients`
1. `Actors / movies`
{{% /notice %}}

### Check Your Understanding

{{% notice green "Question" %}}
Match the following pairs with the appropriate relationship type:

a. `car / manufacturer`

b. `car / title`

c. `car / driver`

d. `car / tire`
{{% /notice %}}

<!-- TODO: Add answers?: a. many-to-one, b. one-to-one, c. many-to-many, d. one-to-many --> 

{{% notice green "Question" %}}
`True/False`: Suppose two C# classes, A and B, are in a one-to-many relationship. Then class A must 
contain a property for instances of B and B must have a property for instances of A.

a. `True`

b. `False`
{{% /notice %}}

<!-- TODO: Add answers?: False, A one-to-many relationship may be present without B containing a property A. -->
