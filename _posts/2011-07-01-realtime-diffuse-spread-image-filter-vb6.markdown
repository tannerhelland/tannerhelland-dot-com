---
author: tanner_h
date: 2011-07-01 23:23:35+00:00
excerpt: A software-based "diffuse filter" - random displacement of image pixels within
  a specified radius - was used in a number of SNES, Genesis, and DOS games to simulate
  an explosion effect.  Today's project provides the source code for generating a
  diffuse effect in real-time.
layout: post
link: http://www.tannerhelland.com/3601/realtime-diffuse-spread-image-filter-vb6/
slug: realtime-diffuse-spread-image-filter-vb6
title: Real-time Diffuse (Spread) Image Filter 
redirect_from:
 - /3601/realtime-diffuse-spread-image-filter-vb6
---

![One brand of camera diffusion lenses](images/camera_diffuse_filters.jpg)

In traditional photography and film, a diffusion filter is used to soften light from a flash or stationary lamp.  Specialized lenses are available for this purpose (see the image above), but the effect can be cheaply replicated by smearing petroleum jelly over the light ([seriously](http://en.wikipedia.org/wiki/Diffusion_filter)) or by shooting through a sheet of nylon.

In image processing, a diffusion filter often means something else entirely.  Photoshop's "Diffuse" filter randomly rearranges pixels within a set radius.  (GIMP can do the same thing, but their effect is more accurately titled "Spread.")  This effect can be animated for a cheap explosion effect - something a number of SNES, Genesis, and DOS games used to great effect.

This project demonstrates a simple, real-time method for replicating such an effect.  All code is commented and reasonably optimized, and an animated "special effect" version is provided for those interested.  Unlike Photoshop, this routine allows you to specify separate horizontal and vertical max random distances, as well as the ability to wrap pixels around image edges.

![LittleBigPlanet mini poster](images/LBP-600x375.jpg)

Here's the original image (a poster for the Playstation 3 game "LittleBigPlanet").

![](images/LBP_diffuse_5-600x375.jpg)

Here is the same image with a diffuse filter applied (max distance = 5).

![](images/LBP_diffuse_50-600x375.jpg)

...and here is the image again, but with max distance = 50.

![](images/LBP_diffuse_50_wrap_pixels-600x375.jpg)

...and one more example.  This time, edge wrapping has been enabled.  Note the bleed of planet pixels at the top and black pixels at the bottom.

**[Download the source code from GitHub](https://github.com/tannerhelland/vb6-code/tree/master/Diffuse-effect)**

Similarly, you can [click here](https://github.com/tannerhelland/PhotoDemon/blob/master/Forms/Effects_Stylize_Diffuse.frm) to see how the function is implemented in [PhotoDemon](https://photodemon.org).