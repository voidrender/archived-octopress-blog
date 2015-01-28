---
layout: post
title: "The Death of FlightPath and the Future of iOS Usage Statistics"
date: 2014-02-09 15:11
comments: true
categories: ios data-collection usage-statistics flightpath testflight flurry tutorial guide
---
As a longtime user of [TestFlight](http://www.testflightapp.com) for both test build distribution and usage analytics, I was extremely disappointed to find that they have [cancelled their FlightPath beta program](http://imgur.com/fcYo5dt) for tracking usage statistics in your live app once distributed via the App Store.  It was great to be able to reuse the same checkpoint infrastructure to collect usage statistics.  Alas, they claim to be focusing more on their core product, which might be a good thing in the end.

As a replacement, I have started working with [Flurry](http://www.flurry.com), which provides a great deal of usage statistics, including an event infrastructure similar to TestFlight's checkpoint system.

Make sure to sign up for a free account and copy your application key.  Let's get started!

<!-- more -->

#Setting Up Flurry  
The Flurry SDK is available as a CocoaPod, so installing is a snap if you're using [CocoaPods](http://www.cocoapods.org).  (If you're not, you really should be.  Check out [this simple guide](../../../../2013/07/29/managing-project-dependencies-in-xcode-an-introduction-to-cocoapods/) I wrote to get started.)

Update your Podfile to include FlurrySDK:

{% codeblock Podfile %}
pod "FlurrySDK"
{% endcodeblock %}

and run `pod install`.

Next, update your app delegate to start a Flurry session when the app finishes launching.

{% codeblock AppDelegate.m %}
#include <Flurry.h>

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
   // Optionally enable crash reporting.
   // Note that you can't have more than one crash reporting tool in your app.
   [Flurry setCrashReportingEnabled:YES];
   // Start sending data to Flurry.
   [Flurry startSession:@"YOUR_KEY_HERE"];
   // ...
}
{% endcodeblock %}

#Tracking Usage with Events
The event system provided by Flurry is similar to TestFlight's checkpoints, but includes a few unique and really nice features.  In TestFlight, events are limited to just a name, but with Flurry you can also associate a dictionary of parameters associated with the event, or cause the event to be timed.

The syntax for logging an event is similar to logging a checkpoint in TestFlight.

###Simple Event Logging

{% codeblock SomeFile.m %}
[Flurry logEvent:@"SomeEventName"];
{% endcodeblock %}

###Event Logging With Parameters
If you'd like to associate some data with the event, there is another static method available.

{% codeblock SomeFile.m %}
NSDictionary *eventParameters = @{...};
[Flurry logEvent:@"SomeEventName" withParameters:eventParameters];
{% endcodeblock %}

###Timed Events

You can time an event and have the duration be reported by Flurry's events dashboard.

{% codeblock SomeFile.m %}
[Flurry logEvent:@"SomeEventName" timed:YES];
// ...
// End the timed event, and optionally add or update parameters.
[Flurry endTimedEvent:@"SomeEventName" withParameters:nil];
{% endcodeblock %}

###Timed Events with Parameters
Lastly, you can combine all three.

{% codeblock SomeFile.m %}
NSDictionary *eventParameters = @{...};
[Flurry logEvent:@"SomeEventName" withParameters:eventParameters timed:YES];
// ...
// End the timed event, and optionally add or update parameters.
[Flurry endTimedEvent:@"SomeEventName" withParameters:nil];
{% endcodeblock %}

*Note that it can take a few hours for events to show up after your first session, and that unlike TestFlight, Flurry events are synchronized when the app is paused or terminated.*

#Additional Features
Flurry passively tracks a lot of other information about your app, too.  Some of the neat metrics you get for free are:

* Sessions
* Active Users
* New Users
* Session Length
* Frequency of Use
* Benchmarks
* User Retention
* Version Adoption
* and many more

I plan to continue using TestFlight and Flurry side-by-side for a while, but may end up migrating completely to Flurry for events.  It certainly has more interesting and useful features than TestFlight's simple checkpoint logging.  If I end up using the two in parallel, I'll do a follow-up post on how to make that easier.