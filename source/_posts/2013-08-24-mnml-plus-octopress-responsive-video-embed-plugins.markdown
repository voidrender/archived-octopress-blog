---
layout: post
title: "mnml+octopress responsive video embed plugins"
date: 2013-08-24 17:31
comments: true
categories: octopress, meta
---
I released a small update to the [mnml Octopress theme](https://github.com/ioveracker/mnml) recently to resolve an issue experienced by one of the users of mnml.  [Cole Nordin](http://www.cnordin.me) opened [an issue](https://github.com/ioveracker/mnml/issues/7) on GitHub which captures a common issue when embedding videos in posts wherein the video will not be resized with the window and therefore does not fit within the bounds of the screen on certain mobile devices.

To address this, I added CSS from the [octopress-responsive-video-embed](https://github.com/optikfluffel/octopress-responsive-video-embed) plugin to the theme.  (Unfortunately, I couldn't find a way to embed the plugin in the theme, so if you know of a way to do that please post in the comments below.)  When you need to embed a video, you can do it one of two ways.

#Use the embed-video-container div
You can take advantage of the CSS directly if you don't want to mess with plugins.  Simpily wrap your embed code in the embed-video-container div like this:

{% codeblock %}
<div class="embed-video-container">
    <iframe width="1600" height="1200" src="//www.youtube.com/embed/_QP5X6fcukM" frameborder="0" allowfullscreen></iframe>
</div>
{% endcodeblock %}

Or, if you'd like a markdown-friendly approach...
#Install the octopress-responsive-video-embed plugin
Copy youtube.rb from the [octopress-responsive-video-embed plugin](https://github.com/optikfluffel/octopress-responsive-video-embed) to your /plugins directory.  When you want to embed a youtube video, use the following markdown:
{% codeblock %}
{% raw %}
{% youtube _QP5X6fcukM %}
{% endraw %}
{% endcodeblock %}

Replace the video id with the video id you'd like to post, of course.  (Make sure not to confuse this with the [video](http://octopress.org/docs/plugins/video-tag/) plugin included with Octopress, which is used to embed mp4 files.)