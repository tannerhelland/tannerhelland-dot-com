---
author: tanner_h
date: 2009-03-25 14:00:57+00:00
excerpt: As promised, here is the second half of my image histogram project.  In this project, I'll show you how to stretch a histogram, equalize individual channels, and - most useful of all - equalize an image's overall luminance.
layout: post
slug: image-histograms-2
title: Image Histograms - Part 2 – Stretching and Equalizing
redirect_from: 
 - /810/vb6-image-histograms-2
 - /810/vb6-image-histograms-2/
---

_This is the 2nd half of a two-part project.  Part 1 is available [here](2009/03/21/image-histograms-1)._

As promised, here is the second half of my histogram code project.  In this project, I'll show you how to stretch a histogram, equalize individual channels, and - most useful of all - equalize an image's overall luminance.

**Stretching a Histogram**

The most straightforward histogram function is referred to as "stretching."  Many images contain a combination of dark and bright colors, but unless an image takes advantage of the full luminance spectrum (by including colors ranging from pure black to pure white), it may appear "dim" or "washed out."  To improve an image like this, it is necessary to adjust the image's colors to better span all possible luminance values.

Stretching handles this by finding the darkest and lightest values in an image, then performing an automatic conversion between that color range (max - min) and the ideal color range (pure white - pure black).

As an example, here is an image that doesn't span the full brightness spectrum:

![Normal Clouds](images/cloudsnormal-600x449.jpg)

Notice how the top half of the histogram is empty?  The brightest pixels in this image are only a mid-level gray.

Here is the same image after running a stretch histogram algorithm:

![Stretched Clouds](images/cloudsstretched-600x449.jpg)

Notice how the histogram now stretches all the way to pure white?  Admittedly, this picture is not the best example of how stretching can be useful - but it's a good demonstration of what stretching *does*.

Stretching is a fast and simple function, but its usefulness is limited.  Take the following image, for example:

![Normal Tiger](images/normaltiger-600x449.jpg)

The colors in this tiger picture stretch all the way from pure black to pure white, but they seem to be more heavily concentrated toward the dark end of the luminance spectrum.  To really fix this picture, we need to redistribute its colors across the spectrum in a more equal way.

Enter equalization.

**Equalizing a Histogram**

Equalizing is a more complex and time-consuming function than stretching, but it is capable of fixing complex lighting problems that stretching alone cannot.

Here is the tiger image post-equalization:

![Equalized Tiger](images/equalizedtiger-600x449.jpg)

See how much more balanced the histogram has become?  As another example, here is the cloud picture from above after both stretching and equalizing:

![Stretched and Equalized Clouds](images/cloudsstretchequalize-600x449.jpg)

Equalizing has brought out details that weren't apparent in the original image, even after stretching.

Rather than going through the gory details of how histogram equalizing works, I'm going to refer you to [this excellent Wikipedia article](http://en.wikipedia.org/wiki/Histogram_equalization).  Here is an especially applicable comment from the article (emphasis mine):

> The above describes histogram equalization on a greyscale image. However, it can also be used on color images by applying the same method separately to the Red, Green and Blue components of the RGB color values of the image. 
>
> Still, **it should be noted that applying the same method on the Red, Green, and Blue components of an RGB image may yield dramatic changes in the image's color balance** since the relative distributions of the color channels change as a result of applying the algorithm. 
>
> However, **if the image is first converted to another color space - Lab color space, or HSL/HSV color space in particular - then the algorithm can be applied to the luminance or value channel without resulting in changes to the hue and saturation of the image**.

Because of this, I have supplied two equalizing algorithms in this project - one that equalizes any combination of color channels, and another that equalizes only luminance.  

**[Download the sample app and source code from GitHub](https://github.com/tannerhelland/vb6-code/tree/master/Histograms-advanced)**

For a more advanced exploration of image histograms, let me refer you to [the source code for my open-source photo editor, PhotoDemon](https://github.com/tannerhelland/PhotoDemon).  PhotoDemon provides a full Adjustments > Histogram menu, with advanced support for both global and local histograms.