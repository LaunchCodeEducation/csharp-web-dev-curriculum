---
title: "Windows Users: Visual Studio Community Edition"
date: 2022-12-15T09:16:07-06:00
draft: false
weight: 2
originalAuthor: Sally Steuterman # to be set by page creator
originalAuthorGitHub: gildedgardenia # to be set by page creator
reviewer: # to be set by the page reviewer
reviewerGitHub: # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

Before you start the installation guide, read through each step below. You will find the recommended features and functionality to install listed in each step.

{{% notice red "Warning" "rocket" %}}
Allow at least an hour for the installation process.
{{% /notice %}}

## Installation Steps

Walk through the installation process by following Microsoft’s [Install Visual Studio](https://learn.microsoft.com/en-us/visualstudio/install/install-visual-studio?view=vs-2022) guide.

1. Verify that your computer can run Visual Studio 2022.
1. Download the *Community* version of Visual Studio 2022.

   {{% notice orange "Note" "rocket" %}}
   Make sure you select Visual Studio 2022.
   You will see multiple options for software downloads, such as Visual Studio Code and Visual Studio for Mac, on this page. Do NOT select either of these options!
   {{% /notice %}}

1. Install the Visual Studio Installer
1. Chose your **Workloads**:

   1. Select the following packages from the Workloads pane:

      1. ASP.NET and web development
      1. Azure development
      1. Data storage and processing
      1. .NET core cross-platform development

      You may need to scroll down to find all of the recommended workloads.

   {{% notice orange "Note" "rocket" %}}
   Steps 5 - 7 are for customizing your Visual Studio. They are optional, and will use the default setting if applicable. This is perfectly acceptable and will work well for this course.

   If you do NOT want to customize your installation process skip to Step 8.
   {{% /notice %}}

1. *Optional*. Choose individual components

   {{% notice orange "Note" "rocket" %}}
   If you are customizing your **Individual components**, make sure that you are installing .NET 6.0 Runtime. This is a default setting. Do not uncheck the box.
   {{% /notice %}}

1. *Optional*. Install language packs
1. *Optional*. Select installation location
1. Start developing

## A Tour of Your New IDE

Microsoft has created a [walkthrough](https://learn.microsoft.com/en-us/visualstudio/ide/quickstart-ide-orientation?view=vs-2022) of the Visual Studio 2022. We recommend you read through this to learn the location of key components within your new IDE.

## Visual Studio Extensions

Extensions can help make your workflow smoother. These are usually add-ons that you can add or remove from your IDE as you grow in your coding skills.

### Connect to GitHub for Windows Users

In this course, we will continue to use GitHub and GitHub Classroom for code storage. Visual Studio has an extension for making it easier to connect with GitHub. Visit this page to download and install the [GitHub Extension for Visual Studio](https://visualstudio.microsoft.com/vs/github/).

## Troubleshooting Your Install

### Missing or Wrong Components?

If you realize (or worry) that you did not install Visual Studio correctly, the [Modify Visual Studio Guide](https://learn.microsoft.com/en-us/visualstudio/install/modify-visual-studio?view=vs-2022) can help you make any needed modifications. This includes changing your workloads or individual components.

### Already have Visual Studio on Your Computer?

If you don’t have this most recent version of Visual Studio installed, you will need to updated it. The [Update Visual Studio Guide](https://learn.microsoft.com/en-us/visualstudio/install/update-visual-studio?view=vs-2022) can help you update your old version of VS to the latest. At the time of this writing, the current version for the course is 2022.

Updating can also help you keep any of your workloads, extensions, or other installed packages up to date.