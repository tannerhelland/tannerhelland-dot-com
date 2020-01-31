---
author: tanner_h
date: 2009-01-23 06:00:27+00:00
excerpt: 'Color shifting is a very fast, very simple effect that can greatly simplify
  the work of game artists.'
layout: post
slug: color-shifting
title: Color Shifting (a cheap way to triple graphics variety)
redirect_from:
 - /474/color-shifting
 - /474/color-shifting/
---

Color shifting is a very fast, very simple effect that can greatly simplify the work of game artists.  Here's a demonstration (using a classic StarCraft Siege Tank):

![For the record, I imagine this image is © Blizzard Entertainment...](images/color_shifting_sample.jpg)

Color shifting is trivial to implement - all we do is shift the red, green, and blue values of each pixel to the right (or left).  For example, a right-shift could work like this:

  1. Red -> Green
  2. Green -> Blue
  3. Blue -> Red

Note that the direction of the shift is somewhat misleading (as Windows DIBs, for example, encode color bits in BGR order), but the direction isn't nearly as important as the effect - that without any extra work, we can generate two color variations on a source image.

Because gray-toned values have RGB values that are identical (or nearly identical), color shifting doesn't change the appearance of gray pixels.  This is evident on the siege tanks above, as the color shifting merely adjusted the subtle hues of the gray regions.

However, the colored portion near the front of the tank changes drastically.  This is expected, since a sharply colored region must have large variations in its RGB values.

In video games where the same unit is available for multiple teams, races, or guilds, color-shifting can turn one base image into at least three possible team colors.  And, because color shifting is such a low-cost function, it can be easily performed on the fly - saving your artists work, and saving file bloat from redundant images.

**[Download the sample app and source code from GitHub](https://github.com/tannerhelland/vb6-code/tree/master/Color-shift-effect)**