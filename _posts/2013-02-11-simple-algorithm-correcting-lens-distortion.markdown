---
author: tanner_h
date: 2013-02-11 03:37:16+00:00
layout: post
slug: simple-algorithm-correcting-lens-distortion
title: A simple algorithm for correcting lens distortion
redirect_from:
 - /4743/simple-algorithm-correcting-lens-distortion
---

One of the new features in the development branch of [my open-source photo editor](https://photodemon.org) is a simple tool for correcting lens distortion.  I thought I'd share the algorithm I use, in case others find it useful.  (There are very few useful examples of lens correction on the Internet - most articles simply refer to existing software packages, rather than explaining how the software works.)

Lens distortion is a complex beast, and a lot of approaches have been developed to deal with it.  Some professional software packages address the problem by providing [a comprehensive list of cameras and lenses](http://www.dxo.com/intl/photo/news/DxO-Optics-Pro-new-lens-camera-combinations55) - then the user just picks their equipment from the list, and the software applies a correction algorithm using a table of hard-coded values.  This approach requires way more resources than a small developer like myself could handle, so I chose a simpler solution: a universal algorithm that allows the user to apply their own correction, with two tunable parameters for controlling the strength of the correction.

![This is what PhotoDemon's new lens correction tool looks like.](images/PhotoDemon_Lens_Correction_Tool-600x343.png)

*PhotoDemon's new lens correction tool in action.*

The key part of the algorithm is less than ten lines of code, so there's not much work involved.  The effect is also fast enough to preview in real-time.

Before sharing the algorithm, let me demonstrate its output.  Here is a sample photo that suffers from typical spherical distortion:

![This lovely demonstration photo comes from Wikipedia, courtesy of Ashley Pomeroy](images/Panotools5618-600x400.jpg)

This lovely demonstration photo comes from [Wikipedia, courtesy of Ashley Pomeroy](http://en.wikipedia.org/wiki/File:Panotools5618.jpg)

Here's the same image, as corrected by the algorithm in this article.  (Pay special attention to the lines on the floor and the glass panels on the right.)

![Note the straight lines on both the floor and the glass panels on the right.  Not bad, eh?](images/Fixed_by_PhotoDemon_Panotools5618-600x400.jpg)

Not bad, eh?

My use of simple bilinear resampling blurs the output slightly; a more sophisticated resampling technique would produce clearer results.

A key feature of the algorithm is that it works at any aspect ratio - rectangular images, like the one above, are handled just fine, as are perfectly square images.

Anyway, here is the required code, as pseudocode:
   
    input:
        strength as floating point >= 0.  0 = no change, high numbers equal stronger correction.
        zoom as floating point >= 1.  (1 = no change in zoom)
    
    algorithm:
    
        set halfWidth = imageWidth / 2
        set halfHeight = imageHeight / 2
        
        if strength = 0 then strength = 0.00001
        set correctionRadius = squareroot(imageWidth ^ 2 + imageHeight ^ 2) / strength
    
        for each pixel (x,y) in destinationImage
            set newX = x - halfWidth
            set newY = y - halfHeight
    
            set distance = squareroot(newX ^ 2 + newY ^ 2)
            set r = distance / correctionRadius
            
            if r = 0 then
                set theta = 1
            else
                set theta = arctangent(r) / r
    
            set sourceX = halfWidth + theta * newX * zoom
            set sourceY = halfHeight + theta * newY * zoom
    
            set color of pixel (x, y) to color of source image pixel at (sourceX, sourceY)
    

That's all there is to it.  Note that you'll need to do some bounds checking, as sourceX and sourceY may lie outside the bounds of the original image.  Note also that sourceX and sourceY will be floating-point values - so for best results, you'll want to interpolate the color used instead of just clamping sourceX and sourceY to integer values.

I should mention that the algorithm works just fine without the zoom parameter.  I added the zoom parameter after some experimentation; specifically, I find zoom useful in two ways:

  * On images with only minor lens distortion, zooming out reduces stretching artifacts at the edges of the corrected image
  * On images with severe distortion, such as true fish-eye photos, zooming-out retains more of the source material

As there is not a universally "correct" solution to these two scenarios, I recommend providing zoom as a tunable parameter.  To give a specific example of the second circumstance, consider [this fish-eye photo from Wikipedia, courtesy of Josef F. Stuefer](http://nrm.wikipedia.org/wiki/File:Fisheye_photo.jpg):

![Severe distortion like this is difficult to correct completely.](images/Fisheye_photo-600x600.jpg)

Severe distortion like this is difficult to fully correct.

If we attempt to correct the image without applying any zoom, the image must be stretched so far that much of the edges are lost completely:

![This is hardly the same photo.  Note also the visible stretching at the edges.](images/Fisheye_photo_corrected_no_zoom-600x600.jpg)

This is hardly the same photo.  The pier at the bottom has been completely erased!

By utilizing a zoom parameter, it is possible to include more of the image in the finished result:

![Much more of the photo can be preserved by adding a simple zoom parameter to the algorithm.](images/Fisheye_photo_corrected_with_zoom-600x600.jpg)

Use of a zoom parameter allows us to preserve much more of the photo.  When correcting severe distortion like this, you might want to apply a sharpening algorithm to the final image.  (This sample image has no sharpening applied.)

Again, I only use a simple resampling technique; a more sophisticated one would produce clearer results at the edges.

If you'd like to see my actual source code, check out [this GitHub link](https://github.com/tannerhelland/PhotoDemon/blob/master/Forms/Effects_Distort_CorrectLens.frm).  I also include an optional radius parameter, which allows the user to correct only a subset of the image (rather than the entire thing), but other than that the code is roughly identical to what you see above.

Enjoy!

P.S. For a great discussion of fish-eye distortion from a pro photographer's perspective, check out [http://photo.net/learn/fisheye/](http://photo.net/learn/fisheye/)
