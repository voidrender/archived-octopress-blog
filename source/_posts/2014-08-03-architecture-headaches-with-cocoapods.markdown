---
layout: post
title: "Architecture Headaches with CocoaPods"
date: 2014-08-03 18:22
comments: true
categories: cocoapods ios xcode linker-errors
---
I recently inherited an iOS project from another developer.  This project was not using CocoaPods for dependency management, so naturally, I converted it to using CocoaPods as soon as I could.  When I first installed the pods, I received this warning in the console:

{% codeblock Terminal %}
[!] Found multiple values (`armv7`, `armv7s`) for the
architectures (`ARCHS`) build setting for the `Pods` 
target definition. Using the first.
{% endcodeblock %}
    
It seemed harmless enough, and the project built without problems for the iPhone simulator.  I carried on for a few weeks working on new features, and then I tried to build a version of the app targeting the iOS devices.  Suddenly, I had linker errors.

{% codeblock %}
"_OBJC_CLASS_$_FBSession", referenced from:
  objc-class-ref in MySourceFile.m
  ...
ld: symbol(s) not found for architecture armv7s
{% endcodeblock %}

I looked around for solutions, but of course with linker errors it's can be very difficult to find answers for a particular issue.  Finally, after many hours of searching, reading, and highly scientific trial and error, I decided to look into the multiple architecture warning from CocoaPods, and that's where I found my issue.  In this particular case, the Pods-* targets in my Pods project were targeting armv7 (which is pretty obvious from the CocoaPods warning, but a few weeks had passed), whereas my main app target architectures included both armv7 and armv7s, hence the linker error above.

The solution was to update the target architectures for the app to `$(ARCHS_STANDARD_32_BIT)` instead of manually specifying both `armv7` and `armv7s`.  Then, when running `pod install`, the `$(ARCHS_STANDARD_32_BIT)` is set for the Pods-* projects as well and everything is happy.

*Note: the reason armv7 and armv7s architectures had been specified for the app is that there is a dependency on a library that does not yet support 64-bit architectures.  It looks like `$(ARCHS_STANDARD_32_BIT)` is a much better way to handle that situation.*