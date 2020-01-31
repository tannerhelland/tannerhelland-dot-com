---
author: tanner_h
date: 2015-05-01 14:51:16+00:00
layout: post
slug: site-overhaul-coming
title: Site overhaul coming - apologies for broken links and other bugs
redirect_from:
 - /5790/site-overhaul-coming
---

[tl;dr](http://en.wikipedia.org/wiki/TL;DR): [Mobilegeddon](http://googlewebmastercentral.blogspot.com/2015/02/finding-more-mobile-friendly-search.html) (who thinks up these names?) has finally provided the kick I need to get this site overhauled.  Apologies in advance for things like messed up formatting and randomly broken links.

I first threw together tannerhelland.com on WordPress 2.0.  To give you an idea of what life was like back then (2006), the release notes for WP 2.0 included such amazing features as "rich editing" and "image uploading".  Be still my soul.

At the time, I was looking to move from a custom-built blog engine to something a little more maintenance-free.  I was experimenting with PHP for the first time, and as part of preparing for "Web 2.0", it seemed like a good language to know.  (Aren't buzzwords like "Web 2.0" hilarious in retrospect?)  So I hacked together a Frankenstein WordPress theme, then added a bunch of custom code to handle my typical blog posts, including automated download links for things like code samples and music.

In the years since, those custom code bits have come back to haunt me, especially with the underlying code being written by a PHP beginner.  I can't easily move to a new platform without dealing with my various custom link and formatting generators, and I keep putting off the task because I don't want the headache of fixing my old code.

But last week, I got a notification that the site had passed a million pageviews, which was kind of a fun symbolic mark... but also a reminder of "oh crap I am still terrible at this blog thing," as evidenced by a full year passing since I've posted anything new.  This is unfortunate, as I've been doing a lot of neat work on [my open-source photo editor](https://photodemon.org/), the kind of work I think would be helpful to talk about in more detail.  My latest project is parsing font files and converting glyphs to standard Windows GraphicsPath objects, which has been both fun and terrifying, and if my adventures could save some other poor soul the time and effort of reverse-engineering Stygian APIs like [Uniscribe](http://en.wikipedia.org/wiki/Uniscribe), I'd love to write more about it.

Anyway, all this, combined with the need for a responsive site design, has motivated me to finally deal with my terrible old WordPress code.  There's no easy way to do this, and I've coded long enough to know that things are going to break no matter how much testing I do, so thanks in advance for your patience with a semi-working site over the next few weeks.

I hope the end result is a much simpler, mobile-friendly site design, and even fewer barriers standing in my way of talking about weird (and hopefully interesting) new projects.  In the meantime, if you need to download a code sample or mp3 or anything else but the link is broken, you can let me know from the [PhotoDemon contact page](https://photodemon.org/about/) (which won't be affected by the current overhaul).
