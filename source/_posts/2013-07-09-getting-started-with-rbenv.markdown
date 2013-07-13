---
layout: post
title: "Managing Ruby Environments on OS X: Getting Started with rbenv"
date: 2013-07-10
comments: true
categories: ruby osx rbenv homebrew guide bash
---
If you've done any development on OS X, chances are you've run into various apps and tools that require different versions of Ruby.  Manually installing and maintaining multiple versions of Ruby is a pain.  Fortunately, there are tools to make this process easier.  Rbenv is a lightweight, focused tool that helps you manage different versions of Ruby and switch between them as needed.  You can even set the specific Ruby version for your app to keep your team on the same page.

#Installation

There are several paths to installing rbenv.  The simplest is to use [homebrew](http://mxcl.github.io/homebrew/).  (If you don't have homebrew, it's easy to install.  Go [here](http://mxcl.github.io/homebrew/).)

First, make sure your homebrew is up-to-date.

```
brew update
```

Then, install rbenv and ruby-build.

```
brew install rbenv
brew install ruby-build
```

Once it is done installing, you need to update your profile.  This is generally ~/.bash_profile.  Open it in your favorite editor, and add the following line.

```
eval "$(rbenv init -)"
```

Now execute that in your current bash session by using `source`.

```
source ~/.bash_profile
```
Rbenv will be setup and ready to use.

#rbenv Basics
The only installation of Ruby that you will have in rbenv at this point is the system version.  If you type the following command, it will show you what versions are installed.

```
rbenv versions
```

This will show an asterisk next to the version rbenv is currently using.  To install a new version of Ruby, use the `rbenv install` command.  For example, to install Ruby 2.0.0-p247:

```
rbenv install 2.0.0-p247
rbenv rehash
```

This will install version 2.0.0-p247 under ~/.rbenv/versions/.  The `rehash` command tells rbenv about the new executables.  You should use this command any time you install a new version of Ruby or install a gem that includes commands.  (You can read about the rehashing process [here](https://github.com/sstephenson/rbenv#understanding-shims).)  You can use this version globally by using the `global` command:

```
rbenv global 2.0.0-p247
```

Or, if you'd like to specify that this version should be used in a specific directory, use the `local` command:

```
rbenv local 2.0.0-p247
```

This will create a file named .ruby-version in the current directory that states the version of Ruby to use while in this directory.  Rbenv looks for this file when you use Ruby commands.  This provides the ability to ensure everyone on your team is using the same version of Ruby when developing your app.

That's it, you're up and running with rbenv!  For additional details and advanced features of rbenv, check out the official [GitHub repository](https://github.com/sstephenson/rbenv).

