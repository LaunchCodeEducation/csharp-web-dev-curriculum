---
title: "Bootstrap"
date: 2023-02-09T12:48:24-06:00
draft: false
weight: 10
originalAuthor: Courtney Frey # to be set by page creator
originalAuthorGitHub: speudusa # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

Bootstrap is a commonly-used style library. It allows users to quickly apply its CSS style rules with class selectors. Style updates can add features or improve the usability of an application. For example, Bootstrap, and other styling libraries for that matter, use a standardized color scheme for items like clickable buttons. As the user of the helper library, you can apply the `btn btn-primary` classes to a button on your page and Bootstrap works behind the CSS scenes to render a blue button with white text in a legible font. For more customization, you could also choose which color you want all of the buttons labelled with `btn-primary` on your web page to be.

Straight out of the box, Bootstrap helps developers to get their web apps well-styled without needing to spend much time writing custom CSS rules. The library also does some of the work of applying user-experience best-practices. The button class `btn-danger` for example, is defaulted to appear red, a color most associated with danger.

Image of standard HTML buttons without CSS:

[IMAGE HERE]

Same buttons with Bootstrap:

[IMAGE HERE]

Bootstrap is already included in the given `_Layout.cshtml`, which means that as long as your view is using that layout, you can access Bootstrap styling.

## Bootstrap Layout
Much of what makes Bootstrap a powerfully helpful and time-saving style library is the layout logic it contains. In brief, Bootstrap uses a [grid system](https://getbootstrap.com/docs/4.4/layout/grid/) of elements labelled containers and rows that respond dynamically to the state of a web page. Grid elements are given a size label that dictates when an item will shift or change how it is rendered. Broadly speaking, the grid system helps developers write applications that work well on screens of various sizes. Once you play around with it, you’ll find that the grid layout can help you write apps that respond to more than just changes in window size.

## Bootstrap Tables
Bootstrap gives us some [table styling](https://getbootstrap.com/docs/4.4/content/tables/) that we can use to display events in CodingEvents. Some table styling is customizable, so read around Bootstrap’s site and explore adding different options to your table.

## Bootstrap Forms
Bootstrap offers a number of classes meant to decorate [form elements](https://getbootstrap.com/docs/4.4/components/forms/). `form-group` helps organize items within a form so that inputs and corresponding labels stay visually connected. form-control can be applied to any type of form input to give it the Bootstrap style and look.

## Check Your Understanding

{{% notice green "Question" "rocket" %}}
True/False: Style updates are considered refactoring, since they add no new features to a project, only make it look better.

<!-- ans: false, style contributes to user interaction and experience and updates are therefore not refactoring -->
{{% /notice %}}
