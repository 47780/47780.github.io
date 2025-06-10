---
layout: post
title:  "Durham, NC"
date:   2025-06-09 00:00:00 -0600
author: Leo
categories: meraki travel photography
---

I travelled to Durham, NC for work recently and had a pretty good time aside from having to deal with the idiosyncrasies of the Meraki platform. I shouldn't get too sidetracked on this, but it's just crazy how bad of an experience it almost always is to set up a simple Meraki network for a small office.
## Rant about network switches

I get the design choices, in theory it *should* make for a plug-and-play set up, but unfortunately the real world is far to disorganized for this. Almost every time we're setting up a new branch office, we are dealing with a different ISP, a different last mile provider, different hardware requirements that often don't get communicated, and the end result is that when the plug-and-play doesn't work, Meraki hardware turns into a pretty hunk of metal that is so limited in what it can do without internet access that I no longer even try to troubleshoot from the local web admin page the switches come with. 
There is no console access, not even in their catalyst models! If you plug in a console cable to one of those you get to see it post on the console and then it just hangs there because once it loads the Meraki image you're locked out of any console with no message letting you know what is going on. Don't ask me how long it took me to find this out. Nowadays, I just always bring a laptop and a fiber to copper converter.

## The photos

The reason I am putting together this post is primarily to show off some photos, and also because I have not updated my site in far too long. Ever since I got this site up and running I've wanted to try to use it as a place to share the things I enjoy on a platform that is not Instagram or Twitter. Something that had been holding me back though is that the photos out of my camera, even as jpegs are far too big for a website, and this site being hosted on Github doesn't particularly lend itself for storing lots of media. To solve this issue, I put together a basic webserver to just host the assets and the I would link them, I think I've used this in previous posts already. Some time after I got that running, I set up a Cloudflare to proxy the requests to my server and also do some catching on their edge network.
So far, this seems to be working okay, after I compress them a bunch and reduce the dimensions they are generally less than 2MB from the original jpegs at about 25MB and they preserve an impressive amount of detail.

I need to not get sidetracked again, but what is up with HEIC? I get that it has way better compression ratios compared to JPEG, but it looks it too. They straight up look like dog shit on any screen that is not an apple mobile device.

Anyway, here are some photos.

![Downtown Durham, NC](https://gonk.catorce.uno/files/hh32jk/downtown-durham.jpg "Downtown Durham, NC"")