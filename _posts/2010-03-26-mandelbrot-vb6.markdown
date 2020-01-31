---
author: tanner_h
date: 2010-03-26 03:08:20+00:00
excerpt: Today's very cool project demonstrates a proof of concept implementation
  for rendering the famed Mandelbrot set (or "Mandelbrot fractal") using VB6.  It's
  a bit of a feat, since VB6 isn't exactly optimized for recursion-heavy calculations...but
  you know me.  I love making VB do things it was never meant to do...
layout: post
slug: mandelbrot-vb6
title: Drawing the Mandelbrot Set / Fractal (in VB6)
redirect_from:
 - /1494/mandelbrot-vb6
---

![](images/Mandelbrot_VB6-508x600.png)

*One possible view of the Mandelbrot set (generated with this project)*

Today's project demonstrates a proof of concept implementation for rendering the famed Mandelbrot set (or "Mandelbrot fractal") using VB6.  It's a bit of a feat, since VB6 isn't exactly optimized for recursion-heavy calculations...but you know me.  I love making old languages do things they were never meant to do!

I'm very happy with how the project turned out.  It may not be the fastest or prettiest or most accurate implementation (for example, at very high zoom-in you'll start to see noticeable quality degradation), but I've  deliberately kept the project as short and sweet as possible to maximize adaptability and learning potential.

To enhance the experience, I've added several user-controlled options to help you get a feel for how the rendering works.  First is the scroll-bar at the top of the screen, which allows you to preferentially set speed or accuracy as the program's objective.  (For those familiar with how the Mandelbrot set works, the scroll bar controls the "escape time" of the recursive function.)

Another neat option is a click-and-drag feature that allows you to draw new rendering boundaries.  This makes it simple to zoom as deep as you want into the fractal.

Finally, rather than a drab grayscale rendering, I've chosen a more purplish gradient.  The code can be easily modified to favor another color if you so choose.

The code is reasonably optimized, so a complete view should render within several seconds on most modern hardware.  If speed is a concern, note that the white areas of the image take the longest to process - so **minimizing** the amount of white you select will **maximize** render speed.  Also, due to the inherent limits of the "Double" type in VB6, if you zoom in really, really far the program may lock up.  (Simply click the close button to force-terminate the project if this happens.)

The download link can be found below these sample images.

![](images/Mandelbrot_VB6_4.png)

![](images/Mandelbrot_VB6_5.png)

![](images/Mandelbrot_VB6_6.png)

**[Download the sample app and source code from GitHub](https://github.com/tannerhelland/vb6-code/tree/master/Mandelbrot)**