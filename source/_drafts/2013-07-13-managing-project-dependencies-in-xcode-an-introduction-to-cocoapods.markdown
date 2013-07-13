---
layout: post
title: "Managing Project Dependencies in Xcode: An Introduction to CocoaPods"
date: 2013-07-13 08:08
comments: true
categories: Xcode cocoa touch iOS dependency-management
---
The open-source community for iOS is amazing.  There are so many high-quality, incredibly useful open-source projects out there now that it would be crazy to work on an iOS project without bringing in at least a few open-source projects.  However, manually managing each of the libraries that you bring in can be tedious at best.  Most of them are hosted on [GitHub](http://github.com), which has improved a lot in the last few years to streamline the process.  With [GitHub for Mac](http://mac.github.com), it's pretty easy to quickly clone a project straight from your browser, but you still have to move the appropriate files into *your* Xcode project.  And then you have to do it all again when the project is updated and you want to take advantage of the latest release.

#CocoaPods
[CocoaPods](http://cocoapods.org) is the best way to manage library dependencies with Xcode.  It's still in the alpha phase, but it's continually being improved.  With CocoaPods, you can easily manage what your project depends on, even specifying the specific version number.  This is all tracked in a file that is diffable, so you can keep this in your source repository and your whole team will automatically be in sync.  As an added bonus, you won't have to keep these projects in your source repository, so you can keep your repository's footprint light.

#Installation
If you're new to [Ruby](http://ruby-lang.org), you should consider using an environment manager like [rbenv](http://www.overacker.me/blog/2013/07/10/getting-started-with-rbenv/) to keep track of your Ruby environments.  It's not just for [Rails](http://rubyonrails.org/)--more and more command line tools are being written in Ruby.  I wrote a [simple guide](http://www.overacker.me/blog/2013/07/10/getting-started-with-rbenv/) to getting started with rbenv that will have you up and running in no time.

#Sample Project
