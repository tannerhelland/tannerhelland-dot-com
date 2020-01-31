---
author: tanner_h
date: 2009-05-02 04:09:13+00:00
excerpt: Edge detection (also called "boundary detection") is a fundamental problem in image processing.  The ability to accurately detect visible "edges" in an image makes possible everything from OCR to silly Instagram effects.  In this project, I've implemented six well-known edge detection algorithms.
layout: post
slug: edge-detection-vb6
title: Basic Image Edge Detection
redirect_from:
 - /952/edge-detection-vb6
 - /952/edge-detection-vb6/
---

Edge detection (also called "boundary detection") is a fundamental problem in image processing.  The ability to accurately detect visible "edges" in an image is what makes possible everything from OCR to silly Instagram effects.  In this project, I've implemented six well-known edge detection algorithms.

For those who have never used edge detection algorithms before, here are examples of various outputs:

Original image:

![Lost_TV](images/wa_lost-cast_02.jpg)

Prewitt method (horizontal):

![lost_1](images/lost_1.jpg)

Prewitt method (vertical):

![lost_2](images/lost_2.jpg)

Sobel method (horizontal):

![lost_3](images/lost_3.jpg)

Sobel method (vertical):

![lost_4](images/lost_4.jpg)

Laplacian method:

![lost_5](images/lost_5.jpg)

Hilite method:

![lost_6](images/lost_6.jpg)

As an additional reference, I've supplied two more edge detection filters using arbitrary convolution matrices.  I include these to show that there's nothing "magical" about edge detection - and in fact, depending on the purpose of your edge-detector, it may actually be worthwhile to use a custom approach instead of a well-known one.

Custom method 1:

![lost_7](images/lost_7.jpg)

Custom method 2:

![lost_8](images/lost_8.jpg)

**[Download the sample app and source code from GitHub](https://github.com/tannerhelland/vb6-code/tree/master/Edge-detection)**

For a more advanced exploration of image edge-detection, you might check out [the source code for the Effects > Edge menu](https://github.com/tannerhelland/PhotoDemon/tree/master/Forms) of my open-source photo editor, [PhotoDemon](https://photodemon.org).  It provides even more edge detectors, including variable shape and radii filters like a Range filter:

[![PD_range_filter_screenshot.png](images/PD_range_filter_screenshot.png)](images/PD_range_filter_screenshot.png)
