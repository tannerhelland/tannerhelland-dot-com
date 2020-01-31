---
author: tanner_h
date: 2009-05-05 06:00:48+00:00
excerpt: The ability to create custom convolution filters is a mainstay of modern photo editors.  A robust matrix-based filter engine can be used to create many unique image effects by simply manipulating the matrices you supply to the engine.  In this project, I've provided a 5x5 custom filter engine with support for both scaling and biasing.  This is roughly identical to the custom filter engine provided by Photoshop...
layout: post
slug: custom-image-filters-vb6
title: Custom Image Convolution Filters
redirect_from:
 - /982/custom-image-filters-vb6
 - /982/custom-image-filters-vb6/
---

The ability to create custom filters is a mainstay of any quality graphics application.  A robust matrix-based filter engine can generate hundreds of unique effects by simply adjusting the matrices that get passed into the engine.

In this project, I've provided a 5x5 custom filter engine with support for scaling/weighting and biasing/offsetting.   This is identical to the custom filter engine provided by Photoshop, and mine is even slightly faster (at least for the screen-sized images I've been testing).

Besides being fast, the engine is also smart.   It is clever enough to estimate edge pixels correctly - even for scaled/weighted filters - and it will automatically validate all input values to make sure they're appropriate.

Finally, I've included 7 sample filters for you to play with, including blur, sharpen, emboss, engrave, grease, unfocus, and vibrate. Below, you can see how each filter looks on a promotional image from the TV show [_Castle_](http://abc.go.com/primetime/castle/index?pn=index).

Original:

![castle](images/castle.jpg)

Blur:

![castle_blur](images/castle_blur.jpg)

Sharpen:

![castle_sharpen](images/castle_sharpen.jpg)

Emboss:

![castle_emboss](images/castle_emboss.jpg)

Engrave:

![castle_engrave](images/castle_engrave.jpg)

Grease:

![castle_grease](images/castle_grease.jpg)

Unfocus:

![castle_unfocus](images/castle_unfocus.jpg)

Vibrate:

![castle_vibrate](images/castle_vibrate.jpg)

**[Download the sample app and source code from GitHub](https://github.com/tannerhelland/vb6-code/tree/master/Custom-image-filters)**

For a more advanced version of this tool, including auto-normalization for the divisor and offset values, you can [see the source code for this function](https://github.com/tannerhelland/PhotoDemon/blob/master/Forms/Effects_CustomFilter.frm) in my open-source photo editor, [PhotoDemon](https://photodemon.org).  Here's a screenshot of its Effects > Custom tool:

[![PD_custom_filter_screenshot.png](images/PD_custom_filter_screenshot.png)](images/PD_custom_filter_screenshot.png)