---
author: tanner_h
date: 2013-09-18 06:44:03+00:00
excerpt: The latest nightly build of PhotoDemon includes a bunch of new and improved blur filters.  I thought it would be fun to speed-test four of its improved blur tools against two other free photo editors - GIMP and Paint.NET.  The results were surprising enough that I thought them worth sharing...
layout: post
slug: performance-photodemon-gimp-paintnet
title: 'Blur Filter performance: PhotoDemon vs GIMP vs Paint.NET'
redirect_from:
 - /5109/performance-photodemon-gimp-paintnet
 - /5109/performance-photodemon-gimp-paintnet/
---

**Note: this is an old article!  [PhotoDemon now has its own website at photodemon.org](https://photodemon.org).**

*(Before I begin: the PhotoDemon 6.0 beta should be live by the end of this week.  Sorry it took so long to prepare!)*

![See what kind of fun charts we get to discuss?  And here I thought the days of 17-minute photo editing actions died with the Pentium III...](images/Zoom.png)

*See what kind of fun charts we get to discuss?  And here I thought the days of 17-minute photo editing actions died with the Pentium III...*

The latest nightly build of PhotoDemon ([download it here](https://photodemon.org/download)) includes a bunch of new and improved blur filters.  Blur filters are among the most computationally demanding filters in a photo editor, because for each pixel in an image, a bunch of other pixels must also be examined in order to calculate the blur.  (Blurs generally work by averaging together groups of pixels.  Motion blur averages pixels in a line, radial blur averages pixels in an arc, and normal blur averages pixels in a box or circle shape.)

As a simple example, consider a basic blur with a 200 pixel radius, applied to a 10 megapixel digital photo.  For each pixel in the photo (all ten million of them), an area of 200 pixels in each direction must be averaged together.  Using a simple box blur, that means a box of 200 pixels left, right, up and down must be tallied (for a net area of 400 * 400, or 160,000 pixel comparisons) in order to calculate the blur.  Thus, such an algorithm would require:

    10,000,000 pixels * 160,000 calculations per pixel = 1.6 trillion calculations

Even on a modern processor, that's an enormous undertaking.  Fortunately, mathematicians and coders have developed many clever ways to optimize blur functions.  Many of these optimizations appear in the newest PhotoDemon build, so I thought it would be fun to speed-test four of PhotoDemon's blur tools against two other free photo editors: [GIMP](http://www.gimp.org/) and [Paint.NET](http://www.getpaint.net/).  The results were surprising enough that I thought them worth sharing.

A brief overview of each photo editor:

  * PhotoDemon: open-source, written in VB6, nightly build 893 (6.0 beta)
  * GIMP: open-source, written primarily in C, v2.8.6
  * Paint.NET: closed-source, written primarily in C# (and the .Net framework, per the name), v3.5.11

As benchmarking goes, this was very informal.  PhotoDemon reports timing automatically in nightly builds, but for GIMP and Paint.NET I had to resort to using a stopwatch.  Normally this is a terrible idea, but the algorithms involved take a very long time to run, so a stopwatch was sufficient for broad timing.  (10ths of a second don't matter much when an algorithm takes twenty minutes to finish...)

All tests were done on Windows 7 (64-bit), on my Core i5 650 (3.2ghz) desktop PC with 8gb of RAM.  My PC was middle-of-the-road when I bought it back in 2010, so I'd consider reasonably representative of an "average" PC.  All the tools in question appear to be heavily CPU-bound anyway, so it's doubtful newer processors or more cores would make a meaningful difference.

The test photo I used was a 10 megapixel photo, 3872x2592 specifically, in JPEG format.

With the exception of some very long timings (10+ minutes), all timings were checked twice to make sure results were representative.  Very long ones were only checked once due to the wait involved, though I did initiate a second attempt just to make sure my PC wasn't acting up.  (It wasn't.)

Here are the timing results for four separate blur types, with some notes on my implementation, and what I know or can potentially infer about GIMP and/or Paint.NET's implementations.

(Due to the large size of the images involved, I saw no reason to upload the output images of each test.  Anyone interested can easily reproduce this test on their own PC with images of their choosing.)

## Gaussian Blur

![Two notes - PhotoDemon used the "good" quality setting, which is a Gaussian estimation using a modified 3x box blur, and GIMP used the IIR method.](images/Gaussian.png)

*Two notes - PhotoDemon used the "good" quality setting, which is a Gaussian estimation using a modified 3x box blur, and GIMP used the IIR method.*

[Gaussian Blur](http://en.wikipedia.org/wiki/Gaussian_blur) provides an excellent starting point.  Gaussian blur works by averaging a square chunk of pixels, and giving pixels close to the center more weight than pixels far away.  It is the most common type of blur tool in photo editing software, probably because its results are aesthetically pleasing, and it is an easy blur function to optimize.

Instead of a naive approach, which would involve the 1.6 trillion calculations mentioned above, most photo editors implement Gaussian Blur using a [separable implementation](http://www.dspguide.com/ch24/3.htm), which cuts the calculations to a much more pleasant 8 billion calculations.  Unfortunately, 8 billion calculations is still a lot.  (PhotoDemon's "best quality" option on its Gaussian tool applies a pure Gaussian using separable kernels.  On large images, it's slow.  Very slow.)

An even faster approach takes advantage of a neat mathematical relationship between box filters and Gaussian filters: if you keep applying a box filter to a set of data, the result will eventually approach a Gaussian distribution.  ([Excellent charts available here, courtesy of Nghia Ho](http://nghiaho.com/?p=1159).)  The [Central Limit Theorem](http://en.wikipedia.org/wiki/Central_limit_theorem) shows that repeating a box blur three times results in a function that's ~97% identical to a true Gaussian.

PhotoDemon uses this as the basis for its three quality settings for Gaussian blur (good, better, and best).  Good is a 3x box blur approximation, Better is a 5x, and Best is a true Gaussian.  For the chart above, I used the "good" setting because it is by far the fastest.  (Note that there's a bit more to it than just repeating a box blur - how you calculate the box blur size matters; I use a variation of the W3 recommendation [available here](http://www.w3.org/TR/SVG11/filters.html#feGaussianBlurStdDeviationAttribute).)

Take-home message: GIMP's IIR implementation is excellent - very fast, and it produces a true Gaussian, no estimations.  PhotoDemon is surprisingly competitive for a single-threaded VB6 app.  Paint.NET's Gaussian is quite poor both in quality and final result.  Its resulting blur is muddier than a true Gaussian, and much slower than you'd expect for a box-blur approximation... so I honestly have no idea how they've implemented it.

## Motion Blur

![PhotoDemon used "Quality" mode instead of "Speed", meaning bilinear interpolation was applied to the rotated image.  No extra options are available for this tool in GIMP or Paint.NET.](images/Motion.png)

*PhotoDemon used "Quality" mode instead of "Speed", meaning bilinear interpolation was applied to the rotated image.  Also, "blur symmetrically" was checked.  No extra options are available for this tool in GIMP or Paint.NET.*

Motion blur is a bit more problematic than Gaussian blur, because it doesn't work in a square pattern.  A naive approach would have you use something like [Bresenham's algorithm](http://en.wikipedia.org/wiki/Bresenham%27s_algorithm) on each pixel, tracing a line at the specified angle and averaging interpolated values as you go.

A much better approach is to simply rotate the image by the requested angle, apply a (very fast) horizontal blur, then rotate the image back into place.  If you use a fast rotation algorithm (like the famous [3-shear technique](http://www.ocf.berkeley.edu/~fricke/projects/israel/paeth/rotation_by_shearing.html)), this can make motion blur very quick.

My PhotoDemon implementation does not use the fast 3-shear technique; it uses a naive, geometric rotation (reverse-mapped) with bilinear interpolation.  I expected this to make it quite a bit slower than comparable tools in GIMP and Paint.NET, but I was surprised to discover that both software packages are... well, pretty damn terrible.

Based on a brief perusal of [GIMP's source code](https://git.gnome.org/browse/gimp/tree/plug-ins/common/blur-motion.c?id=GIMP_2_8_0), they appear to use the naive Bresenham approach, which explains why it's so slow.

Once again, Paint.NET's execution time makes no sense to me.  For a software package that claims: "[extensive work has gone into making Paint.NET the fastest image editor available](http://www.getpaint.net/features.html)", methinks they need a bit more "extensive work" on this particular tool...

## Radial Blur

![As before, PhotoDemon uses the "quality" setting for bilinear interpolation.  Paint.NET was applied at quality setting 2 out of 5, the default setting.  (This results in a noticeably lower-quality image than PhotoDemon or GIMP.)  GIMP does not provide any additional options for this tool.](images/Radial.png)

*As before, PhotoDemon uses the "quality" setting for bilinear interpolation.  Paint.NET was applied at quality setting 2 out of 5, the default setting.  GIMP does not provide any additional options for this tool.*

And so we move to Radial Blur, where we find a surprising role reversal: Paint.NET gives a much better showing here, while GIMP turns in the worst performance yet.  Again, a brief look at [GIMP's source code for this function](https://git.gnome.org/browse/gimp/tree/plug-ins/common/blur-motion.c?id=GIMP_2_8_0) shows a questionable nested-loop approach to the problem.  Tracing an arc-like path for each pixel is a bad idea, and while bilinear interpolation is used to improve the output quality - same as PhotoDemon - the time required makes this tool pretty much unusable.

PhotoDemon's implementation is nothing particularly special, which makes its relative performance so surprising.  I use [a well-known trick](http://www.jhlabs.com/ip/blurring.html) where I convert the image to polar coordinates, apply a horizontal blur, then convert the image back to Cartesian coordinates.  A small amount of image quality is lost by the two coordinate conversions, but because we are blurring the image anyway, this doesn't matter much.  That said, for small angles (< 5 degrees), both GIMP and Paint.NET produce better-looking output.

At larger radii, however, PhotoDemon's is much better.  Both GIMP and Paint.NET produce [Moire patterns](http://en.wikipedia.org/wiki/Moire), presumably from sampling at discrete intervals, while PhotoDemon's output is clean and smooth.  This can probably be fixed in Paint.NET by using a higher quality setting, but quality setting 2/5 was already slow enough!

![The top-left corner of the image after PhotoDemon's radial blur.  Buttery smooth, and accurate edge handling.](images/PhotoDemon-radial-blur.jpg)

*The top-left corner of the image after PhotoDemon's radial blur.  Buttery smooth, and accurate edge handling.*

![Same corner, but from Paint.NET's radial blur.  Nasty Moire patterns, and problematic handling in the corner - from an algorithm that took 4x longer to run.](images/Paint-dot-Net-radial-blur.jpg)

*Same corner, but from Paint.NET's radial blur.  Nasty Moire patterns, and problematic handling in the corner - from an algorithm that took 4x longer to run.*

## Zoom Blur

![No, that huge green bar is not an error.  GIMP took a whopping 17 minutes to render a 200px zoom blur.  PhotoDemon's "traditional" mode was used to provide comparable output.  Paint.NET does not offer any specialized options for this tool.](images/Zoom.png)

*No, that huge green bar is not an error.  GIMP took a whopping 17 minutes to render a 200px zoom blur.  PhotoDemon's "traditional" mode was used to provide comparable output.  Paint.NET does not offer any specialized options for this tool.*

Last up is Zoom Blur, and we have a surprising winner!  Paint.NET's zoom blur implementation is excellent - great quality, very fast, and overall a huge improvement from their other blur tools.  I have no idea why Zoom Blur is significantly faster than their Gaussian Blur implementation at a comparable pixel size, so I can only assume that some kind of specialized optimizations have been added.  Nice work, Paint.NET team!

GIMP... I don't even know what to say.  It's possible that I triggered some sort of problem with GIMP's tile-based processing system, because there is no good way to explain a 17-minute processing time for such a straightforward function.  Even a naive implementation shouldn't take anywhere near that long.  Their implementation has loops nested five-deep (dear god), and while bilinear interpolation is used to improve output, that algorithm is so poorly written that I frankly think they should consider removing it completely.  Even at very low distances, rendering takes forever.  The original copyright date on the source file is 1997, so perhaps someone familiar with GIMP's internals should give this one a second look.

PhotoDemon uses the same trick here as with radial blur.  The image is converted to polar coordinates (with swapped x and y values compared to the radial blur conversion), a horizontal blur is applied, then the image is converted back.  Again, there is quality loss at low values, and both Paint.NET and GIMP provide better-quality output at very small radii.  To mitigate this, I provide a second style on that dialog, which uses an iterative image-sized alpha blend to generate a blur.  One of the neat things about that approach is that the image can be zoomed-out as well as zoomed-in.

![I doubt there is a legitimate use for zoom-blur-outward like this, but it wasn't any extra work to implement.](images/PhotoDemon-Zoom-Blur-screenshot-600x344.jpg)

I doubt there is a legitimate use for zoom-blur-outward like this, but it wasn't any extra work to implement...

## Conclusions

Blur algorithm performance is hugely variable in both GIMP and Paint.NET.  I'll admit - I find it a bit amusing that my little PhotoDemon project, written with a 15-year-old programming language and compiler, outperforms them so handily in multiple areas, despite my implementations being generally lazy, single-threaded, and heavily CPU-bound.  I also call "bullshit" on Paint.NET's claim about "extensive work going into making Paint.NET the fastest image editor available."  I think the Paint.NET team does great work, and their software is a wonderful improvement over many free and paid photo editors, but its performance is greatly lacking in a number of areas.

Then there is GIMP.  While I am very grateful for their software, and have learned to love its many quirks, there's no denying that whole swaths of its source code are in desperate need of a revamp.  I imagine there is no point revisiting items like blur until they complete their migration to [GEGL](http://www.gegl.org/) - perhaps then we will see big improvements in the performance of these various blur functions.

If there's a take-home message to all this, it's that algorithms will always be more important than programming languages.  A well-written algorithm in a "slow" language will often outperform a poorly written algorithm in a "fast" language.  VB6 may be forgotten and nearly dead, but I'm happy to see it staying competitive with the titans of the "free photo editor" world.  :)

If you read the article all the way to here, I hope you'll give PhotoDemon a look:

[https://photodemon.org/download/](https://photodemon.org/download/)

For a free, open-source photo editor, it has a lot of nice features, and I can empirically state that it outperforms GIMP and Paint.NET in at least a few areas!  (The current nightly build is pretty much how the next stable release (6.0) will look, minus a few minor bugfixes still to complete.)
