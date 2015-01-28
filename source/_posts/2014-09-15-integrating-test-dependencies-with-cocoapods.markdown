---
layout: post
title: "Integrating Test Dependencies with CocoaPods"
date: 2014-09-15 13:49
comments: true
categories: cocoapods ios xcode automated-tests how-to
---
Most Xcode projects should have some level of test coverage, and any time unit tests are involved it's nice to have a framework for generating mock objects.  However, we don't want to bloat our production app package with these test frameworks, so it's nice to link these libraries only with the test target.  Configuring this properly can be tricky, and the CocoaPods documentation isn't very clear on exactly how to accomplish this in the podfile.

The cleanest solution I've found to this problem involves specifying the pods for each target individually and using a Ruby function to import the common pods.  Here is a sample podfile that accomplishes this:

{% codeblock Podfile %}

platform :ios, '7.0'

def import_common_pods
   pod 'AFNetworking'
end

target 'MyAppTarget' do
   import_common_pods
end

target 'MyAppTestTarget' do
   import_common_pods
   pod 'OCMock'
end 

{% endcodeblock %}

Note that you may run into a few issues with this if you're  adding this to an existing project and the previous podfile did not explicitly specify the non-test target.  In that case, you may need to delete the old Pods.xcconfig and libPods.a files then regenerate your workspace with `pod install`.

#Update
As of CocoaPods 0.34, there's a cleaner solution built-in:

{% codeblock Podfile %}
source 'https://github.com/CocoaPods/Specs.git'

platform :ios, '7.0'

pod 'AFNetworking'

target "MyAppTestTarget", :exclusive => true do
   pod 'OCMock'
end 

{% endcodeblock %}
