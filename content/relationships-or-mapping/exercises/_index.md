---
title: "Exercises"
date: 2022-12-15T09:16:07-06:00
draft: false
weight: 2
originalAuthor: John Woolbright # to be set by page creator
originalAuthorGitHub: jwoolbright23 # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: 12/15/22 # UPDATE ANY TIME CHANGES ARE MADE
---

## Major Concepts & Key Terminology

The learning objectives for this chapter are:

This chapter introduces the tools needed to create meaningful relationships using ORM. Let’s consider the different types of relationships at a conceptual level. In later sections, we will learn how to implement these relationships using EntityFrameworkCore.

## Content Links

{{% children %}}
Exercises: The Early Bird Gets the ORM.
=======================================

Now that we have gotten very familiar with our ``CodingEvents`` application, let's design some additional features.
As you work on your ``CodingEvents`` application, you may have been inspired by `Meetup <https://www.meetup.com/>`_.
One of the cool features that Meetup has is that people can sign up for accounts.
They can use their Meetup accounts to follow the events they are most interested in and keep track of their calendar of events.
To add similar features to ``CodingEvents``, you need to add a ``Person`` class.
For the exercises, answer the following questions about what your ``Person`` class would look like.

.. admonition:: Note

   You do not have to code anything to complete these exercises.
   This is mainly focused on using our design skills to add a new feature to your application.

#. You need to add a ``Person`` class to hold necessary info about users of our app. What fields and methods would this class hold?
#. Would you need to add any additional classes to ``Person`` to make the app work? If so, what classes would be necessary?
#. What kinds of relationships would ``Person`` have to the other classes you already created, such as the ``Event`` class?

As you dream up answers to these questions, write the answers down in a note or piece of paper. You are now going to write up some documentation for your app.

#. Add a ``README.md`` to your repository by navigating to the repository page on your GitHub profile.
   At the bottom of the page, there is a blue banner asking you to add a ``README.md``. Click the button to do so.
#. You should write three sections. The first should describe the purpose of the app. The second should describe the current state of the app.
   The third and final section should describe the future improvements you want to make to the app including your notes about the ``Person`` class.


