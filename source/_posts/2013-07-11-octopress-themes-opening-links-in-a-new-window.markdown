---
layout: post
title: "Octopress Themes: Opening Links in a New Window"
date: 2013-07-11 14:00
comments: true
categories: 
---
I just rolled out a change to the [mnml](https://github.com/ioveracker/mnml) theme to cause links to be opened in a new window.  If you're looking to do the same thing for your [Octopress](http://octopress.org) theme, it requires a simple change to the `/source/javascripts/octopress.js` file.  Open that file and add the following to the [$(document).ready()](http://learn.jquery.com/using-jquery-core/document-ready/) function:

``` javascript
$(document).ready(function(){
    // You probably already have some code here.
    // Just add this to the end of the function.
    $('a').each(function() {
        var a = new RegExp('/' + window.location.host + '/');
        if(!a.test(this.href)) {
            $(this).click(function(event) {
                event.preventDefault();
                event.stopPropagation();
                window.open(this.href, '_blank');
            });
        }
    });
});
```
You could also do this in any web app that uses [jQuery](http://jquery.com), of course.

(Hat-tip to [Addri Kodde](http://www.adrikodde.nl/blog/2012/octopress-links-new-window/) for posting a snippet about this.)