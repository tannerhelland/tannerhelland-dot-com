---
author: tanner_h
date: 2009-03-21 07:19:26+00:00
excerpt: Today's project demonstrates how to quickly and efficiently generate an image histogram.  Histograms are invaluable for understanding and implementing a multitude of image processing techniques - including brightness, contrast, levels, curves, equalizing, and more - so it's worth taking some time to experiment with them.  
layout: post
slug: image-histograms-1
title: Image Histograms – Part 1
redirect_from:
 - /747/vb6-image-histograms-1
 - /vb6/vb6-image-histograms-1
 - /747/vb6-image-histograms-1/
 - /vb6/vb6-image-histograms-1/
---

_This is the 1st half of a two-part project.  Part 2 is available [here](2009/03/25/image-histograms-2)._

I realized today that while I use image histograms in several of the projects on this site (particularly my [Real-Time Image Levels](341/image-levels-vb6) demo), I don't actually provide a stand-alone image histogram viewer.

...Until now!

Image histograms are very useful in image processing.  In fact, the most basic image processing algorithms - like adjusting brightness and contrast - are just image histogram processes.  Many other functions (including levels, curves, and more) can also be described as histogram operations.

So what is an image histogram, and why is it useful?

**What is a histogram?**

[Answers.com](http://www.answers.com) defines histograms as:

> A bar graph of a frequency distribution in which the widths of the bars are proportional to the classes into which the variable has been divided and the heights of the bars are proportional to the class frequencies.

I realize this definition is not entirely useful, but it is important to note that histograms are not used **only** in image processing.  Histograms are simply a type of graph - nothing more, nothing less.

A simpler way to define histograms is this: **a histogram is a bar graph that shows population by category**.  Categories are listed, in order, along the x-axis (or horizontally).  The population (or, alternatively, number of occurrences) of each category is listed along the y-axis (or vertically).  In this graph from the 2000 U.S. census, travel time of working Americans is shown as a histogram:

![histogram_demo](images/histogram_demo.png)

Simple, eh?

**So what is an Image Histogram?**

As you can imagine, an image histogram is a type of histogram that tells us something about an image.  In most cases, the categories in an image histogram are brightness levels (from black to white), while the "population" of each category is the number of pixels with that brightness.

To demonstrate, let's look at two different image histograms.

First, here is a histogram of a dark, cloudy image:

![dark_histogram](images/dark_histogram.jpg)

Notice how the image histogram is heavily weighted to the left?  Because this image is quite dark, the histogram shows much more pixels on the left side of the graph (the dark side) than it does on the right side of the graph (the light side).

Conversely, here is the histogram of a bright image:

![light_histogram](images/light_histogram.jpg)

While there are some dark regions in the center of the image (indicated by the spike on the far left of our histogram), the bulk of the image is lighter, and as a result the bulk of our histogram is shifted toward the right.

Now that you know what image histograms represent, try out the attached histogram code and see if you can predict rough histogram outlines before loading an image.  

**[Download the sample app and source code from GitHub](https://github.com/tannerhelland/vb6-code/tree/master/Histograms-basic)**

**[Continue to Image Histograms - Part 2](2009/03/25/image-histograms-2)**
