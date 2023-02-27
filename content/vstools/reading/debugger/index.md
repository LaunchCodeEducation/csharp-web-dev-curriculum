---
title: "Debugger"
date: 2023-02-14T19:56:25-06:00
draft: false
weight: 3
originalAuthor: Sally Steuterman # to be set by page creator
originalAuthorGitHub: gildedgardenia # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: # UPDATE ANY TIME CHANGES ARE MADE
---

Some of the features that you will find yourself leaning on the most as you further your career in tech is the Visual Studio debugging tools.

{{% notice blue "Note" "rocket" %}}

The links for each debugging feature below are for Windows users. Mac users will find that Visual Studio for Mac has the same exact features, but those features may look slighlty different or be in a slightly different location. We have provided some extra tips for Mac users at the end in case you haven't been able to locate these tools in your copy of Visual Studio for Mac.

{{% /notice %}}

Open up your [examples repo](https://github.com/LaunchCodeEducation/csharp-web-dev-examples) and find the `HelloMethods` project. Read through each item, make note of how the debugging tools work for each item, and practice using the tool on `HelloMethods`:

1. Right-click in the text editing window to add a [breakpoint](https://learn.microsoft.com/en-us/visualstudio/debugger/debugger-feature-tour?view=vs-2022#set-a-breakpoint-and-start-the-debugger) to your code.
1. Start debug mode with the run button as you might normally run your program.
1. Make note of the debugger panes and how you might make use of them:
   1. [Autos](https://learn.microsoft.com/en-us/visualstudio/debugger/autos-and-locals-windows?view=vs-2022) pane shows the values of parameters and variables on the line that the debugger is 
     currently sitting on, as well as the line above.
   1. [Locals](https://learn.microsoft.com/en-us/visualstudio/debugger/autos-and-locals-windows?view=vs-2022) pane shows the value of local variables and parameters within the program being debugged.
   1. Add variables, parameters, and expressions to the [Watch](https://learn.microsoft.com/en-us/visualstudio/debugger/debugger-feature-tour?view=vs-2022#set-a-watch) pane to monitor their values while debugging.
   1. [Call Stack](https://learn.microsoft.com/en-us/visualstudio/debugger/how-to-use-the-call-stack-window?view=vs-2022) pane displays the record of the methods that have been called in the program being debugged.
   - View a list of breakpoints in the *Breakpoints* pane. You may also disable and enable breakpoints from here.
1. Debugger [Code Stepping](https://learn.microsoft.com/en-us/visualstudio/debugger/navigating-through-code-with-the-debugger?view=vs-2022&tabs=csharp#code-stepping) Buttons:
   1. [Step over](https://learn.microsoft.com/en-us/visualstudio/debugger/debugger-feature-tour?view=vs-2022#step-over-code-to-skip-functions) button moves debugger to the next line to be executed within a method.
   1. *Step out* button brings the debugger out of the execution of a method.
   1. *Step into* button makes the debugger enter the method at which it is currently paused. Note that 
     you can't step into `System` defined methods, only those defined by your program.

1. Right-click on the breakpoint to set conditional logic for when you want the breakpoint to run.
1. Stop debug mode wth the stop button.

## Visual Studio for Mac Extra Tips

1. Your IDE may not default to *Debug* mode. To select for it, in the top menu, select *Debug > Start Debugging*.
1. To view the debugging panes, select *Debug* in the top menu and scroll down to *Windows*. Select 
   the items you wish to view, ie. *Breakpoints*, *Watch*, etc.
1. To add conditions to a breakpoint, right click on the breakpoint and select *Edit Breakpoint*. From 
   menu that opens, use the *Advanced Conditions* section to set your conditions for when you want the 
   breakpoint to be executed.
1. For more information on using the Debugger in Visual Studio for Mac, check out this [guide](https://learn.microsoft.com/en-us/visualstudio/mac/debugging?view=vsmac-2022).

## Check Your Understanding

{{% notice green "Question" "rocket" %}}

   True or False: Breakpoints on `Console.WriteLine()` are helpful because stepping into them reveals what is printed in the console.

{{% /notice %}}

<!-- False, The Visual Studio debugger tool does not allow us to step into ``Console.WriteLine()`` methods or any method defined by ``System``. -->

{{% notice green "Question" "rocket" %}}

   Define a *breakpoint*.

   1. A point in our code where the debugger will stop running and provide information about the current state.
   1. A point in our code that we anticipate will result in an exception or error.
   1. A point in our code where we include a print statement to see what's going on.
   1. A point in our code where we want to throw the computer out of a window because nothing works.

{{% /notice %}}

<!-- A point in our code where the debugger will stop running and provide information about the current state. -->