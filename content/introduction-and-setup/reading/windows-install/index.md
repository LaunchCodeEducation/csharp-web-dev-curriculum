---
title: "Windows Users: Visual Studio Community Edition"
date: 2022-12-15T09:16:07-06:00
draft: false
weight: 2
originalAuthor: Sally Steuterman # to be set by page creator
originalAuthorGitHub: gildedgardenia # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: Courtney Frey # update any time edits are made after review
lastEditorGitHub: speudusa # update any time edits are made after review
lastMod: 2022-06-05T16:16:07-06:00 # UPDATE ANY TIME CHANGES ARE MADE
---

Before you start the installation guide, read through each step below. You will find the recommended features to install listed in each step.

{{% notice orange "Warning" "rocket" %}}
Allow at least **an hour** for the installation process.
{{% /notice %}}

## Installation Steps

### Prerequisites

Before you start installing anything, make sure that you can install this on your computer.

### Install Visual Studio

Walk through the installation process by following Microsoft’s [Install Visual Studio](https://learn.microsoft.com/en-us/visualstudio/install/install-visual-studio?view=vs-2022) guide.

Here are some things you should keep in mind as you install Visual Studio:

1. Download the *Community* version of Visual Studio 2022.
1. In Step 4, select the following **Workflows**: 
   1. ASP.NET and web development
   1. .NET desktop development

   No other workloads are required for this course. 

1. In Step 5, if it's not already selected, select the following **.NET 6.0 Runtime (Long Term Support)**. You do not need to select any other Individual components for this course.

1. Step 7 is optional. You do not need to change Visual Studio's install location.

Once you have installed Visual Studio, we recommend you take the IDE tour below before moving on to the next. 

## A Tour of Your New IDE

Microsoft has created a [walkthrough](https://learn.microsoft.com/en-us/visualstudio/ide/quickstart-ide-orientation?view=vs-2022) of the Visual Studio 2022. We recommend you read through this to learn the location of key components within your new IDE.

{{% notice blue "Note" "rocket" %}} 
 As you follow along, make sure that you create a **_Console Application_** project and NOT a _Console App (.NET Framework)_ project.
{{% /notice %}}

## Troubleshooting Your Install

If you need to troubleshoot your install, first check out the [documentation](https://learn.microsoft.com/en-us/visualstudio/install/troubleshooting-installation-issues?view=vs-2022). If this does not help, check out the below sections and consult your TA if something is still off.

### Missing or Wrong Components?

If you realize (or worry) that you did not install Visual Studio correctly, the [Modify Visual Studio Guide](https://learn.microsoft.com/en-us/visualstudio/install/modify-visual-studio?view=vs-2022) can help you make any needed modifications. This includes changing your workloads or individual components.

You need .NET 6.0 (Long Term Support) at the very minimum.
 
### Already have Visual Studio on Your Computer?

If you don’t have this most recent version of Visual Studio installed, you will need to update it. The [Update Visual Studio Guide](https://learn.microsoft.com/en-us/visualstudio/install/update-visual-studio?view=vs-2022) can help you update your old version of VS to the latest. At the time of this writing, the current version for the course is 2022.

Updating can also help you keep any of your workloads, extensions, or other installed packages up to date.
