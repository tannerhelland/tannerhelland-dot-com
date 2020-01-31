---
author: tanner_h
date: 2014-07-01 13:00:26+00:00
excerpt: I've already talked at length about converting a temperature (in Kelvin) to an RGB triplet.  But what if you simply want to adjust an image's temperature, without caring about the specifics of it?  This article is for you.  As a bonus, source code is also provided for tint adjustments.
layout: post
slug: simple-algorithms-adjusting-image-temperature-tint
title: Simple algorithms for adjusting image temperature and tint
redirect_from:
 - /5675/simple-algorithms-adjusting-image-temperature-tint
---

I've already talked at length about [converting a temperature (in Kelvin) to an RGB triplet](4435/convert-temperature-rgb-algorithm-code/).  But what if you simply want to adjust an image's temperature, without caring about the specifics of it?

Here's how:

    Given a temperature adjustment on the range -100 to 100,
     apply the following adjustment to each pixel in the image:
    
    r = r + adjustmentValue
    g = g
    b = b - adjustmentValue

As with any additive RGB adjustment, you'll need to manually clip the output values to the [0, 255] range.

Here's a sample of the output, as implemented in the latest development build of [my open-source photo editor](http://photodemon.org/).  Note the temperature slider at the bottom of the screen.  Because I find the -100 to 100 range to be a bit too strong, I actually divide the adjustment value by 5, thus limiting the actual adjustment value from -20 to 20:

![temp_tint_base_image](images/temp_tint_base_image-600x408.jpg)

Base image, courtesy of [http://en.wikipedia.org/wiki/Great_wall](http://en.wikipedia.org/wiki/Great_wall)

![Temperature at max value (+20)](images/temp_up-600x408.jpg)

Temperature at max value (+20).  Note the warmer tones.

![Temperature at min value (-20)](images/temp_down-600x408.jpg)

Temperature at min value (-20).  Note the cooler tones.

Pretty simple!

Because temperature and tint adjustments are usually provided together, here's the code for basic tint adjustments.  It's even simper than temperature:
    
    Given a tint adjustment on the range -100 to 100, 
     apply the following adjustment to each pixel in the image:
    
    r = r 
    g = g + adjustmentValue
    b = b 

Sample output, using the same sample image from above (note the tint slider at the bottom):

![Tint at max value (+20).  Hard to tell as the image is already very green, but the green has actually been ramped up further.](images/tint_up-600x408.jpg)

Tint at max value (+20).  Hard to tell as the image is already very green, but the green has actually been ramped up further.

![Tint at minimum value (-20).  Note the magenta color cast.](images/tint_down-600x408.jpg)

Tint at minimum value (-20).  Note the magenta color cast.

This might be the simplest image processing algorithm I've ever posted...  :)
