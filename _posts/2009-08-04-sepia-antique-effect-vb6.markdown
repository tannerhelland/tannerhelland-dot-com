---
author: tanner_h
date: 2009-08-04 02:23:31+00:00
excerpt: I'm guessing you've seen this style of image before - a sort of pseudo-antique
  filter than can make any image look like it was taken with a very old camera.  There
  are many ways to programmatically generate images like this.
layout: post
slug: sepia-antique-effect-vb6
title: Sepia / “Antique” Image Effect 
redirect_from:
 - /1138/sepia-antique-effect-vb6
 - /vb6/sepia-antique-effect-vb6
---

!["Antiquified" version of a BBT promo photo](images/Sepia_Big_Bang_Theory.jpg)

I'm guessing you've seen this style of image before - a sort of "antique" filter than can make any photo look like it was taken with a very old camera (or even a [daguerreotype](http://en.wikipedia.org/wiki/Daguerreotype)).  

There are many ways to programmatically generate images like this, and in this article I've put together one that does more than just make the image look "brown."  This filter involves several steps (fading, multiplicative brightness, and gamma correction, among others) and results in a conversion that not only adds a sepia coloring, but also gives an image a histogram more in keeping with older photos.

As with all graphics code on this site, the algorithm is fast enough to be applied in real-time.

**[Download the sample app and source code from GitHub](https://github.com/tannerhelland/vb6-code/tree/master/Sepia-effect)**

For a more advanced version of this effect, check out [the source code for the "antique" filter in PhotoDemon, my open-source photo editor](https://github.com/tannerhelland/PhotoDemon/blob/master/Forms/Effects_Stylize_Antique.frm).  Here's a screenshot of PhotoDemon's antique dialog, which provides multiple user-adjustable settings:

[![PhotoDemon antique filter](images/PD_antique_screenshot.png)](images/PD_antique_screenshot.png)