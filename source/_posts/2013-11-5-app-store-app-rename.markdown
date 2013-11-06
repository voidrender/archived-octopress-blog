---
layout: post
title: "Renaming An App on the App Store"
date: 2013-11-5 17:38
comments: true
categories: ios appstore
---
Renaming an app on the iOS app store is a relatively simple thing to do.  The biggest point of confusion is that you cannot rename your app unless it is in an *editable state*.  You're probably going to want to change the display name for your app, so the easiest way to put your app in an editable state is to upload a new binary.

#Bundle Identifier

If you want to rename your Xcode project to reflect the new app name, you won't want your bundle identifier to change along with the project name since this is the unique identifier for your app on the device.  By default, the bundle identifier includes `${PRODUCT_NAME}` or a variant thereof, e.g. `${PRODUCT_NAME:rfc1034identifier}`.  You won't want the Bundle Identifier to change when you rename your project, so the first thing you'll want to do is copy your Bundle Identifier from iTunes Connect and paste that in the Bundle Identifier field in the info.plist file for your app.

#Rename Project

The fastest (and most thorough) way to rename your app is to simply rename the project in Xcode.  Slowly double-click on the project file in Xcode so that the name becomes editable and change the name.  After pressing enter, a dialog will pop up asking if you'd like to rename project content items.  You probably want to keep all of these in sync, so choose Rename.

#Upload Binary

Login to iTunes Connect and create a new version of your app.  When you edit the metadata for the new version of your app, you can now edit the name of the app.  Enter the new name for your app, create your new binary, and upload.  If you make it through the review process, your app will be ready to launch under a new name!  As long as you don't change the Bundle Identifier, existing users will receive the update.