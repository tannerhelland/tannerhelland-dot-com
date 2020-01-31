---
author: tanner_h
date: 2008-12-24 22:41:38+00:00
excerpt: Adjusting an image's colors using a "curves" dialog should be familiar to any PhotoShop users out there.  Curves is similar in theory to both "Image Levels" and normal gamma correction, but it provides a much more powerful interface for adjusting an image's luminance and color balance.
layout: post
slug: image-curves-vb6
title: Real-time Image Curves (using cubic splines)
redirect_from:
 - /336/image-curves-vb6
 - /336/image-curves-vb6/
---

Adjusting an image's colors using a "curves" dialog should be familiar to any PhotoShop users out there.  Curves is similar in theory to both "[level adjustments](2008/12/24/image-levels-vb6)" and standard gamma correction, but it provides a much more powerful interface for adjusting luminance and color balance.

This project provides results very similar to Photoshop's, and it allows the creation of more spline knots (32 instead of 16).  The cubic spline code on which I based my code was taken from Jason Bullen's excellent "Simple Cubic Spline Curve Plot" ([available at Planet Source Code](http://www.planetsourcecode.com/vb/scripts/ShowCode.asp?txtCodeId=11488&lngWId=1)).

![Believe-it-or-not, this is a legitimate application of calculus.  Who knew such a thing existed? :) ](images/curves_sample.jpg)

The code is well-commented and very fast.

**[Download the sample app and source code from GitHub](https://github.com/tannerhelland/vb6-code/tree/master/Curves-effect)**

For a more advanced version of this tool, check out [the source code for the Adjustments > Curves tool](https://github.com/tannerhelland/PhotoDemon/blob/master/Forms/Adjustments_Curves.frm) in [PhotoDemon, my open-source photo editor](https://photodemon.org).  PhotoDemon's version of the tool allows you to adjust each channel individually (red, green, blue) with an improved UI and faster underlying algorithm, as shown in the screenshot below.

[![PhotoDemon curves screenshot](images/PD_curves_screenshot.png)](images/PD_curves_screenshot.png)