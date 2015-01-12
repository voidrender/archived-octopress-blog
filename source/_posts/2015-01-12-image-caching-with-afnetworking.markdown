---
layout: post
title: "Image Caching with AFNetworking"
date: 2015-01-12 13:09
comments: true
categories: iOS AFNetworking objective-c
---
[AFNetworking](http://www.afnetworking.com) is one of the most popular open-source networking frameworks for iOS.  You're probably already using it, but if you're not, you should consider it.  One of the lesser-known features of AFNetworking is the ability to easily load an image from a URL to be used in a `UIImageView`.

<!-- more -->

#Simple Image Caching
Start by importing the `UIImageView+AFNetworking` header and several useful methods will be added to the `UIImageView` class.

For simple in-memory caching, you can use the `setImageWithURL:` and `setImageWithURL:placeholderImage:` methods and the image will be retrieved from the in-memory cache, if the image exists, otherwise it will be fetched from the URL and stored in the cache.

{% codeblock lang:objc %}

[imageView setImageWithURL:[NSURL URLWithString:imageURL]];

// Or, with a placeholder image displayed while the image is being downloaded:
[imageView setImageWithURL:[NSURL URLWithString:imageURL]
          placeholderImage:[UIImage imageNamed:@"placeholder"]];

{% endcodeblock %}

#Disk Caching
If you need to cache the image for longer than the user's session, you can use the `setImageWithURLRequest:placeholderImage:success:failure:` method.  Set the caching policy on your `NSURLRequest` to whatever you need and you're good to go!

{% codeblock lang:objc %}

NSURLRequest *imageRequest = [NSURLRequest requestWithURL:[NSURL URLWithString:imageURL]
                                              cachePolicy:NSURLRequestReturnCacheDataElseLoad 
                                          timeoutInterval:60];

[imageView setImageWithURLRequest:imageRequest
                 placeholderImage:[UIImage imageNamed:@"placeholder"]
                          success:nil
                          failure:nil];

{% endcodeblock %}

Note that if you supply a success block, you will be responsible for setting the image within the success block.  If one is not provided, AFNetworking will set the image for you.

#Alternative

If AFNetworking isn't your thing, I highly recommend using the excellent [SDWebImage](https://github.com/rs/SDWebImage) instead.