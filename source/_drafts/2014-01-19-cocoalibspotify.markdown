---
layout: post
title: "CocoaLibSpotify Basics"
date: 2014-01-19 17:42
comments: true
categories: iOS, spotify
---
I recently started working with [CocoaLibSpotify](http://github.com/spotify/cocoalibspotify) and found it a tiny bit challenging to navigate at first.  The documentation is fairly comprehensive, but the sample projects included in the repository only show examples of a few simple scenarios.  The rest of the tasks one may want to perform must be gleaned from reading the documentation.  This is fine, but I would have liked a slightly more comprehensive guide to getting started.  I am hoping to provide such a guide in this post.
<!-- more -->

#Installation

Like most modern open-source iOS frameworks, CocoaLibSpotify is available as a CocoaPod.  Simply add CocoaLibSpotify to your Podfile:
{% codeblock Podfile %}
pod "CocoaLibSpotify"
{% endcodeblock %}
and run `pod install`.

#SPAsyncLoading & KVO

First, a word on working with the library.  A good chunk of the operations performed by CocoaLibSpotify are asynchronous.  To facilitate this, the library itself provides a mechanism (`SPAsyncLoading`) to execute a block when some asynchronous operation has been performed.  It's actually quite clever, as you'll see from examples later in this post.  Furthermore, Key-Value Observing can be used to monitor changes to fields throughout the API.

#Session Management

#Search

#Playback
