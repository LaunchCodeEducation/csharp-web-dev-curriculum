---
title: "NuGet"
date: 2023-02-14T19:56:25-06:00
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

**NuGet** is a package management tool for .NET software. 
NuGet allows you to use external code sources without including the codebase itself. You can make 
use of compiled libraries that other developers have already built. You can choose to use a 
specific version of a package hosted by NuGet, and update that version as need be. 

As with MSBuild, we will only scratch the surface of the utility of a .NET package manager. That 
said, it is still a good idea to get [familiar with these tools](https://learn.microsoft.com/en-us/nuget/what-is-nuget). As your programs grow larger, 
MSBuild and NuGet will help to maintain a robust codebase.

NuGet packages are readily available within the IDE itself. Perhaps you have noticed the 
*Dependencies* directory that is created in our projects? 

To browse available NuGet packages:

#. Right-click on that directory
#. Select “Manage NuGet Packages” from the dropdown menu
#. The resulting window will show you a catalog of software packages you may add to your project

### Managing NuGet Packages

The following documentation can help you become more familiar with downloading and managing NuGet packages.

**Windows Users:** [Follow this guide](https://learn.microsoft.com/en-us/nuget/consume-packages/install-use-packages-visual-studio).

**Mac Users:** [Use this guide](https://learn.microsoft.com/en-us/visualstudio/mac/nuget-walkthrough?toc=%2Fnuget%2Ftoc.json&view=vsmac-2022).

## Check Your Understanding

{{% notice green "Question" "rocket" %}}

   Select which item best describes the job of NuGet.

   1. NuGet compiles your C# programs to be deployed in different conditions.
   1. NuGet is a marshmallow-like confection found in many candy bars.
   1. NuGet is a package manager for .NET programs.
   1. NuGet allows you to download dependency library source code into your solution.

{{% /notice %}}

<!-- c, NuGet is a package manager for .NET programs. -->

{{% notice green "Question" "rocket" %}}

   True or False: NuGet and MSBuild share responsibilities and only one is needed to deploy a C# app.

{{% /notice %}}
<!-- False, While NuGet gives you access to the dependencies you need for your application, 
   MSBuild can configure how those dependencies are used in different executable environments. -->