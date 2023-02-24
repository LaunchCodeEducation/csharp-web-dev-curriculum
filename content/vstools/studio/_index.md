---
title: "Studio: If It Ain't Broke, Add a Breakpoint!"
date: 2023-02-14T19:56:25-06:00
draft: false
weight: 2
originalAuthor: Sally Steuterman # to be set by page creator
originalAuthorGitHub: gildedgardenia # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

On your machine, open up your copy of `SpinningDiscs` in Visual Studio.
The purpose of this studio is to talk about your current debugging strategies and how to make the most of the debugger tools discussed in this chapter.

Before we start practicing with debugging tools, go over with the group one error you encountered when working on your own version of last lesson's studio.
This could be the result of a typo or a logical error. 

1. What was the error?
1. How did you solve this error? What have been the strategies and tools you have been using so far to debug your code?
1. Could one of the debugging tools help you when addressing this error?
   For example, if you encountered an error where data was not being written onto a disc object, could you track the properties of the object with a debugging tool?

Now, checkout the [debugging branch](https://github.com/LaunchCodeEducation/SpinningDiscs-Studio/tree/debugging) of
the studio repo. Review the code and use the debugging tools in Visual Studio to practice assessing the program.

To get started, try the following:

1. Add `cd.Name` to the *Watch* pane to track the value of that property. Does it change?
1. Add a few breakpoints inside of `Program.cs` and make note of where you expect the program to break its execution. 
1. Add a breakpoint inside of some of the methods in `BaseDisc.cs`. Anticipate what you expect to see as the last line in the 
	*Call Stack* pane when the debugger stops.

After you look through the code and try out these tasks, take it one step further by answering these questions.

1. When would you use the *Call Stack* pane? If you run the app and it is already functioning, what shows up there? 
1. Would a conditional breakpoint make sense to use in the context of this app? Try changing one of the breakpoints you have already added to a conditional breakpoint and run your app! 

Once you have gone through the code, open up a piece of code you have been struggling with.
In what ways could making use of debugging tools help you figure out what is going on with the code?