---
author: tanner_h
date: 2010-06-15 02:07:18+00:00
excerpt: Basic emboss and engrave filters are two of the simplest
  image processing features to implement. Both operate on the same principle - for
  each pixel, subtract the RGB values of one or more neighboring pixels in a particular
  direction. This leads to an image where low-contrast areas are all black, while
  high-contrast areas (edges) are varying colors of brighter intensity. 
layout: post
slug: generating-emboss-engrave-relief-filters-vb6
title: 'Emboss / Engrave / Relief image filters'
redirect_from:
 - /2225/generating-emboss-engrave-relief-filters-vb6
---

![](images/bayonetta_emboss.jpg)

*Sample emboss photo, using a promo image from the video game "Bayonetta"*

I've had this code ready for months, but I couldn't bring myself to post it until I added something more exciting than just "emboss" and "engrave."

Today is that day!

First, let me mention what emboss/engrave actually do.  These are two of the simplest image processing filters, and they can be efficiently implemented in pretty much any programming language.  They both operate on the same principle - for each pixel, subtract the RGB values of one or more neighboring pixels in a particular direction.  This leads to an image where low-contrast areas are all black, while high-contrast areas (edges) are varying colors of brighter intensity.  Most emboss/engrave filters add 127 to the RGB values so that uniformly contrasted areas are gray.  As a bonus feature, I've added a "color" option to this code, so you can emboss/engrave an image to any hue.  In the Bayonetta example above, the left side of the picture is embossed to something around #81a3fe.

Relief is a variation on emboss/engrave, where the base color is not artificially generated but is based off the current pixel.  This acts almost like a sharpen filter, but because the filter doesn't operate in all directions, it lends the image a more artificial look.  (Hence the "relief" moniker - on certain images, it looks like an image has been chipped out of stone and then painted.)  Try it on a photo - they tend to work best!

**[Download the sample app and source code from GitHub](https://github.com/tannerhelland/vb6-code/tree/master/Emboss-engrave-effect)**