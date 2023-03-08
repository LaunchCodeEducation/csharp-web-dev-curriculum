---
title: "Installing Postman"
date: 2023-01-20T08:49:09-06:00
draft: false
weight: 75
originalAuthor: John Woolbright # to be set by page creator
originalAuthorGitHub: jwoolbright23 # to be set by page creator
reviewer: # to be set by the page reviewer
reviewerGitHub: # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: 03/08/23 # UPDATE ANY TIME CHANGES ARE MADE
---

When exploring and testing a web API, it is invaluable to have an interactive environment that allows you to fine-tune requests. For example, you may need to configure the HTTP method, headers, or body of the request -- all of which the browser does not allow you to do. Instead of testing in a browser, we can use tools made specifically for interacting with APIs. One of the most popular API tools in the industry is **Postman**. Postman is a cross-platform tool that puts you in full control of configuring and executing API requests. 

Installing Postman is easy thanks to its cross-platform nature. You can download the installer on [their downloads page](https://www.postman.com/downloads/). 

## Mac Users

1. Select the version that matches the type of chip your Mac has. If you are unsure if you have an Intel chip or the Apple chip, click on the apple in the upper left corner of your screen. Select **About This Mac**. Under *Processor* on the **Overview** tab, you will see the chip manufaturer.

![Postman installation page with two Mac options displayed](pictures/download-installer-mac.png?classes=border)

2. After installation, you can open the app. Postman will first prompt you to make an account, but if you are uncomfortable doing so, at the bottom of the screen is the option to sign up for an account later.

The main view of Postman is the launchpad view.

![Postman launchpad view for Mac, contains overview of initial actions a user can make with the software](pictures/launchpad-view-mac.png?classes=border)

You are ready to go!

## Windows Users

1. Select the **Windows x64** installer download then run the installer:

![Close up of webpage to install Postman, user selecting Windows x64 option](pictures/download-installer.png?classes=border)

Windows user should select the *Windows 64-bit* download option

2. After installation, if Postman does not open automatically, locate the download and open it manually. Making an account can be useful, but if you do not want to create one, select the link in grey at the bottom of the splash screen that reads: "Skip signing in and take me straight to the to the app":

![Postman splash screen for a new account](pictures/account.png?classes=border)

{{% notice blue "Note" "rocket" %}}
**Windows Users**: Once installed, you can right-click the Postman icon and pin it to your taskbar for easy access in the future:

![User pins the Postman application to their taskbar on Windows](pictures/pin-taskbar.png?classes=border)

Pinning the Postman application to your Windows taskbar could make your life easier
{{% /notice %}}

3. You can leave the launchpad view open for now. We will explore Postman after setting up our API server.

![Postman launchpad view, contains overview of initial actions a user can make with the software](pictures/launchpad-view.png?classes=border)

Now that Postman is installed, there are a lot of features of the software to explore