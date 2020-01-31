---
author: tanner_h
date: 2012-12-28 20:16:17+00:00
excerpt: Dithering is still a surprisingly applicable technique, not just for practical reasons (such as preparing a full-color image for output on a non-color printer), but for artistic reasons as well.  Dithering also has applications in web design, where it is a useful technique for reducing images with high color counts to lower color counts, reducing file size (and bandwidth) without harming quality.  It also has uses when reducing 48 or 64bpp RAW-format digital photos to 24bpp RGB for editing.
layout: post
slug: dithering-eleven-algorithms-source-code
title: 'Image Dithering: Eleven Algorithms and Source Code'
redirect_from:
 - /4660/dithering-eleven-algorithms-source-code
 - /4660/dithering-eleven-algorithms-source-code/
---

## Dithering: An Overview

Today's graphics programming topic - dithering - is one I receive a lot of emails about, which some may find surprising.  You might think that dithering is something programmers shouldn't have to deal with in 2012.  Doesn't dithering belong in the annals of technology history, a relic of times when "16 million color displays" were something programmers and users could only dream of?  In an age when cheap mobile phones operate in full 32bpp glory, why am I writing an article about dithering?

Actually, dithering is still a surprisingly applicable technique, not just for practical reasons (such as preparing a full-color image for output on a non-color printer), but for artistic reasons as well.  Dithering also has applications in web design, where it is a useful technique for reducing images with high color counts to lower color counts, reducing file size (and bandwidth) without harming quality.  It also has uses when reducing 48 or 64bpp RAW-format digital photos to 24bpp RGB for editing.

And these are just image dithering uses - dithering still has extremely crucial roles to play in audio, but I'm afraid I won't be discussing audio dithering here.  Just image dithering.

In this article, I'm going to focus on three things:

  * a basic discussion of how image dithering works
  * eleven specific two-dimensional dithering formulas, including famous ones like "Floyd-Steinberg"
  * how to write a general-purpose dithering engine

_Update 11 June 2016: some of the sample images in this article have been updated to better reflect the various dithering algorithms.  Thank you to commenters who noted problems with the previous images!_

## Dithering: Some Examples

Consider the following full-color image, a wallpaper of the famous "[companion cube](http://half-life.wikia.com/wiki/Aperture_Science_Weighted_Storage_Cube)" from _[Portal](http://en.wikipedia.org/wiki/Portal_%28video_game%29)_:

![This will be our demonstration image for this article.  I chose it because it has a nice mixture of soft gradients and hard edges.](images/Portal_Companion_Cube.jpg) 

This will be our demonstration image for this article.  I chose it because it has a nice mixture of soft gradients and hard edges.

On a modern LCD or LED screen - be it your computer monitor, smartphone, or TV - this full-color image can be displayed without any problems.  But consider an older PC, one that only supports a limited palette.  If we attempt to display the image on such a PC, it might look something like this:

![This is the same image as above, but restricted to a websafe palette.](images/Portal_Companion_Cube_websafe.png)

This is the same image as above, but restricted to a websafe palette.

Pretty nasty, isn't it?  Consider an even more dramatic example, where we want to print the cube image on a black-and-white printer.  Then we're left with something like this:

![At this point, the image is barely recognizable.](images/Portal_Companion_Cube_1bpp.png)

At this point, the image is barely recognizable.

Problems arise any time an image is displayed on a device that supports less colors than the image contains.  Subtle gradients in the original image may be replaced with blobs of uniform color, and depending on the restrictions of the device, the original image may become unrecognizable.

Dithering is an attempt to solve this problem.  Dithering works by approximating unavailable colors with available colors, by mixing and matching available colors in a way that mimicks unavailable ones.  As an example, here is the cube image once again reduced to the colors of a theoretical old PC - only this time, dithering has been applied:

![A big improvement over the non-dithered version!](images/Portal_Companion_Cube_websafe_dithered.png)

A big improvement over the non-dithered version!

If you look closely, you can see that this image uses the same colors as its non-dithered counterpart - but those few colors are arranged in a way that makes it _seem_ like many more colors are present.

As another example, here is a black-and-white version of the image with similar dithering applied:

![The specific algorithm used on this image is "2-row Sierra" dithering.](images/Portal_Companion_Cube_1bpp_2RowSierra.png)

The specific algorithm used on this image is "2-row Sierra" dithering.

Despite only black and white being used, we can still make out the shape of the cube, right down to the hearts on either side.  Dithering is an extremely powerful technique, and it can be used in ANY situation where data has to be represented at a lower resolution than it was originally created for.  This article will focus specifically on images, but the same techniques can be applied to any 2-dimensional data (or 1-dimensional data, which is even simpler!).

## The Basic Concept Behind Dithering

Boiled down to its simplest form, dithering is fundamentally about _error diffusion_.

Error diffusion works as follows: let's pretend to reduce a grayscale photograph to black and white, so we can print it on a printer that only supports pure black (ink) or pure white (no ink).  The first pixel in the image is dark gray, with a value of 96 on a scale from 0 to 255, with zero being pure black and 255 being pure white.

![Here is an example of the RGB values in the example.](images/0_92_255.png)

Here is a visualization of the RGB values in our example.

When converting such a pixel to black or white, we use a simple formula - is the color value closer to 0 (black) or 255 (white)?  96 is closer to 0 than to 255, so we make the pixel black.

At this point, a standard approach would simply move to the next pixel and perform the same comparison.  But a problem arises if we have a bunch of "96 gray" pixels - they all get turned to black, and we're left with a huge chunk of empty black pixels, which doesn't represent the original gray color very well at all.

Error diffusion takes a smarter approach to the problem.  As you might have inferred, error diffusion works by "diffusing" - or spreading - the error of each calculation to neighboring pixels.  If it finds a pixel of 96 gray, it too determines that 96 is closer to 0 than to 255 - and so it makes the pixel black.  But then the algorithm makes note of the "error" in its conversion - specifically, that the gray pixel we have forced to black was actually 96 steps away from black.

When it moves to the next pixel, the error diffusion algorithm adds the error of the previous pixel to the current pixel.  If the next pixel is also 96 gray, instead of simply forcing that to black as well, the algorithm adds the error of 96 from the previous pixel.  This results in a value of 192, which is actually closer to 255 - and thus closer to white!  So it makes this particular pixel white, and it again makes note of the error - in this case, the error is -63, because 192 is 63 less than 255, which is the value this pixel was forced to.

As the algorithm proceeds, the "diffused error" results in an alternating pattern of black and white pixels, which does a pretty good job of mimicking the "96 gray" of the section - much better just forcing the color to black over and over again.  Typically, when we finish processing a line of the image, we discard the error value we've been tracking and start over again at an error of "0" with the next line of the image.

Here is an example of the cube image from above with this exact algorithm applied - specifically, each pixel is converted to black or white, the error of the conversion is noted, and it is passed to the next pixel on the right:

![This is the simplest possible application of error diffusion dithering.](images/Portal_Companion_Cube_1bpp_1DErrorDiffusion.png)

This is the simplest possible application of error diffusion dithering.

Unfortunately, error diffusion dithering has problems of its own.  For better or worse, dithering always leads to a spotted or stippled appearance.  This is an inevitable side-effect of working with a small number of available colors - those colors are going to be repeated over and over again, because there are only so many of them.

In the simple error diffusion example above, another problem is evident - if you have a block of very similar colors, and you only push the error to the right, all the "dots" end up in the same place!  This leads to funny lines of dots, which is nearly as distracting as the original, non-dithered version.

The problem is that we're only using a _one-dimensional_ error diffusion.  By only pushing the error in one direction (right), we don't distribute it very well.  Since an image has two dimensions - horizontal and vertical - why not push the error in multiple directions?  This will spread it out more evenly, which in turn will avoid the funny "lines of speckles" seen in the error diffusion example above.

## Two-Dimensional Error Diffusion Dithering

There are many ways to diffuse an error in two dimensions.  For example, we can spread the error to one or more pixels on the right, one or more pixels on the left, one or more pixels up, and one or more pixels down.

For simplicity of computation, all standard dithering formulas push the error _forward_, never backward.  If you loop through an image one pixel at a time, starting at the top-left and moving right, you never want to push errors _backward_ (e.g. left and/or up).  The reason for this is obvious - if you push the error backward, you have to revisit pixels you've already processed, which leads to more errors being pushed backward, and you end up with an infinite cycle of error diffusion.

So for standard loop behavior (starting at the top-left of the image and moving right), we only want to push pixels _right_ and _down_.

![Apologies for the crappy image - but I hope it helps illustrate the gist of proper error diffusion.](images/how_to_dither.png)

Apologies for the crappy image - but I hope it helps illustrate the gist of proper error diffusion.

As for how specifically to propagate the error, a great number of individuals smarter than I have tackled this problem head-on.  Let me share their formulas with you.

(Note: these dithering formulas are available multiple places online, but the best, most comprehensive reference I have found is [this one](http://www.efg2.com/Lab/Library/ImageProcessing/DHALF.TXT).)

## Floyd-Steinberg Dithering

The first - and arguably most famous - 2D error diffusion formula was published by Robert Floyd and Louis Steinberg in 1976.  It diffuses errors in the following pattern:


           X   7
       3   5   1
    
         (1/16)


In the notation above, "X" refers to the current pixel.  The fraction at the bottom represents the divisor for the error.  Said another way, the Floyd-Steinberg formula could be written as:

   
               X    7/16
       3/16  5/16   1/16


But that notation is long and messy, so I'll stick with the original.

To use our original example of converting a pixel of value "96" to 0 (black) or 255 (white), if we force the pixel to black, the resulting error is 96.  We then propagate that error to the surrounding pixels by dividing 96 by 16 ( = 6), then multiplying it by the appropriate values, e.g.:


               X     +42
       +18    +30    +6


By spreading the error to multiple pixels, each with a different value, we minimize any distracting bands of speckles like the original error diffusion example.  Here is the cube image with Floyd-Steinberg dithering applied:

![Floyd-Steinberg dithering](images/Portal_Companion_Cube_FloydSteinberg.png)

Not bad, eh?

Floyd-Steinberg dithering is easily the most well-known error diffusion algorithm.  It provides reasonably good quality, while only requiring a single forward array (a one-dimensional array the width of the image, which stores the error values pushed to the next row).  Additionally, because its divisor is 16, bit-shifting can be used in place of division - making it quite fast, even on old hardware.

As for the 1/3/5/7 values used to distribute the error - those were chosen specifically because they create an even checkerboard pattern for perfectly gray images.  Clever!

One warning regarding "Floyd-Steinberg" dithering - some software may use other, simpler dithering formulas and call them "Floyd-Steinberg", hoping people won't know the difference.  [This excellent dithering article](http://www.efg2.com/Lab/Library/ImageProcessing/DHALF.TXT) describes one such "False Floyd-Steinberg" algorithm:


       X   3
       3   2
    
       (1/8)


This simplification of the original Floyd-Steinberg algorithm not only produces markedly worse output - but it does so without any conceivable advantage in terms of speed (or memory, as a forward-array to store error values for the next line is still required).

But if you're curious, here's the cube image after a "False Floyd-Steinberg" application:

![Much more speckling than the legit Floyd-Steinberg algorithm - so don't use this formula!](images/Portal_Companion_Cube_FalseFloydSteinberg.png)

## Jarvis, Judice, and Ninke Dithering

In the same year that Floyd and Steinberg published their famous dithering algorithm, a lesser-known - but much more powerful - algorithm was also published.  The Jarvis, Judice, and Ninke filter is significantly more complex than Floyd-Steinberg:


                 X   7   5 
         3   5   7   5   3
         1   3   5   3   1
    
               (1/48)


With this algorithm, the error is distributed to three times as many pixels as in Floyd-Steinberg, leading to much smoother - and more subtle - output.  Unfortunately, the divisor of 48 is not a power of two, so bit-shifting can no longer be used - but only values of 1/48, 3/48, 5/48, and 7/48 are used, so these values can each be calculated but once, then propagated multiple times for a small speed gain.

Another downside of the JJN filter is that it pushes the error down not just one row, but _two_ rows.  This means we have to keep two forward arrays - one for the next row, and another for the row after that.  This was a problem at the time the algorithm was first published, but on modern PCs or smartphones this extra requirement makes no difference.  Frankly, you may be better off using a single error array the size of the image, rather than erasing the two single-row arrays over and over again.

![Jarvis, Judice, Ninke dithering](images/Portal_Companion_Cube_JarvisJudiceNinke.png)

## Stucki Dithering

Five years after Jarvis, Judice, and Ninke published their dithering formula, Peter Stucki published an adjusted version of it, with slight changes made to improve processing time:


                 X   8   4 
         2   4   8   4   2
         1   2   4   2   1
    
               (1/42)


The divisor of 42 is still not a power of two, but all the error propagation values are - so once the error is divided by 42, bit-shifting can be used to derive the specific values to propagate.

For most images, there will be minimal difference between the output of Stucki and JJN algorithms, so Stucki is often used because of its slight speed increase.

![Stucki dithering](images/Portal_Companion_Cube_Stucki.png)

## Atkinson Dithering

During the mid-1980's, dithering became increasingly popular as computer hardware advanced to support more powerful video drivers and displays.  One of the best dithering algorithms from this era was developed by Bill Atkinson, a Apple employee who worked on everything from MacPaint (which he wrote from scratch for the original Macintosh) to HyperCard and QuickDraw.

Atkinson's formula is a bit different from others in this list, because it only propagates a fraction of the error instead of the full amount.  This technique is sometimes offered by modern graphics applications as a "reduced color bleed" option.  By only propagating part of the error, speckling is reduced, but contiguous dark or bright sections of an image may become washed out.


            X   1   1 
        1   1   1
            1
    
          (1/8)


![Atkinson dithering](images/Portal_Companion_Cube_Atkinson.png)

## Burkes Dithering

Seven years after Stucki published his improvement to Jarvis, Judice, Ninke dithering, Daniel Burkes suggested a further improvement:


                 X   8   4 
         2   4   8   4   2
    
               (1/32)


Burkes's suggestion was to drop the bottom row of Stucki's matrix.  Not only did this remove the need for two forward arrays, but it also resulted in a divisor that was once again a multiple of 2.  This change meant that all math involved in the error calculation could be accomplished by simple bit-shifting, with only a minor hit to quality.

![Burkes dithering](images/Portal_Companion_Cube_Burkes.png)

## Sierra Dithering

The final three dithering algorithms come from Frankie Sierra, who published the following matrices in 1989 and 1990:


                X   5   3
         2   4  5   4   2
             2  3   2
              (1/32)
    
                X   4   3
        1   2   3   2   1
              (1/16)

    
                X   2
            1   1
              (1/4)


These three filters are commonly referred to as "Sierra", "Two-Row Sierra", and "Sierra Lite".  Their output on the sample cube image is as follows:

![Sierra (sometimes called Sierra-3)](images/Portal_Companion_Cube_Sierra3.png)

![Two-row Sierra](images/Portal_Companion_Cube_Sierra2.png)

![Sierra Lite](images/Portal_Companion_Cube_SierraLite.png)

## Other dithering considerations

If you compare the images above to the dithering results of another program, you may find slight differences.  This is to be expected.  There are a surprising number of variables that can affect the precise output of a dithering algorithm, including:

  * Integer or floating point tracking of errors.  Integer-only methods lose some resolution due to quantization errors.

  * Color bleed reduction.  Some software reduces the error by a set value - maybe 50% or 75% - to reduce the amount of "bleed" to neighboring pixels.

  * The threshold cut-off for black or white.  127 or 128 are common, but on some images it may be helpful to use other values.

  * For color images, how luminance is calculated can make a big difference.  I use the HSL luminance formula ( [max(R,G,B) + min(R,G,B)] / 2).  Others use ([r+g+b] / 3) or one of the [ITU formulas](http://www.tannerhelland.com/3643/grayscale-image-algorithm-vb6/).  YUV or CIELAB will offer even better results.

  * Gamma correction or other pre-processing modifications.  It is often beneficial to normalize an image before converting it to black and white, and whichever technique you use for this will obviously affect the output.

  * Loop direction.  I've discussed a standard "left-to-right, top-to-bottom" approach, but some clever dithering algorithms will follow a _serpentine_ path, where left-to-right directionality is reversed each line.  This can reduce spots of uniform speckling and give a more varied appearance, but it's more complicated to implement.

For the demonstration images in this article, I have not performed any pre-processing to the original image.  All color matching is done in the RGB space with a cut-off of 127 (values <= 127 are set to 0).  Loop direction is standard left-to-right, top-to-bottom.

Which specific techniques you may want to use will vary according to your programming language, processing constraints, and desired output.

## I count 9 algorithms, but you promised 11!  Where are the other two?

So far I've focused purely on error-diffusion dithering, because it offers better results than static, non-diffusion dithering.

But for sake of completeness, here are demonstrations of two standard "ordered dither" techniques.  Ordered dithering leads to far more speckling (and worse results) than error-diffusion dithering, but they require no forward arrays and are very fast to apply.  For more information on ordered dithering, check out the [relevant Wikipedia article](http://en.wikipedia.org/wiki/Ordered_dithering).

![Ordered dither using a 4x4 Bayer matrix](images/Portal_Companion_Cube_Bayer4x4.png)

Ordered dither using a 4x4 Bayer matrix

![Ordered dither using an 8x8 Bayer matrix](images/Portal_Companion_Cube_Bayer8x8.png)

Ordered dither using an 8x8 Bayer matrix

With these, the article has now covered a total of 11 different dithering algorithms.

## Writing your own general-purpose dithering algorithm

Earlier this year, I wrote a fully functional, general-purpose dithering engine for [PhotoDemon (an open-source photo editor)](https://photodemon.org).  Rather than post the entirety of the code here, let me refer you to [the relevant page on GitHub](https://github.com/tannerhelland/PhotoDemon/blob/master/Forms/Adjustments_BlackAndWhite.frm).  The black and white conversion engine starts at line 350.  If you have any questions about the code - which covers all the algorithms described on this page - please let me know and I'll post additional explanations.

That engine works by allowing you to specify any dithering matrix in advance, just like the ones on this page.  Then you hand that matrix over to the dithering engine and it takes care of the rest.

The engine is designed around monochrome conversion, but it could easily be modified to work on color palettes as well.  The biggest difference with a color palette is that you must track separate errors for red, green, and blue, rather than a single luminance error.  Otherwise, all the math is identical.
