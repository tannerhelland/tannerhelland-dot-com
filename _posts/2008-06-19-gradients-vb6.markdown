---
author: tanner_h
date: 2008-06-19 22:34:55+00:00
layout: post
slug: gradients-vb6
title: 'Smooth linear color gradients'
redirect_from:
  - /47/gradients-vb6
  - /vb6/gradients-vb6
  - /47/gradients-vb6/
  - /vb6/gradients-vb6/
---

This program demonstrates how to create a smooth color gradient between any two colors. 

![gradient_screenshot](/images/gradient_Sample_ss.png)

While gradients are often used for visual effects, perhaps the most useful aspect of this project is the gradient algorithm itself.  This code uses [linear interpolation](https://en.wikipedia.org/wiki/Linear_interpolation), which is a staple of many other algorithms, both graphics and otherwise.  Keep a copy in your toolbox!

**[Download the sample app and source code from GitHub](https://github.com/tannerhelland/vb6-code/tree/master/Gradient-2D)**

For a much more advanced demonstration of image gradients, you might investigate [the gradient tool source code](https://github.com/tannerhelland/PhotoDemon/blob/master/Modules/GradientTool.bas) for my [open-source photo editor, PhotoDemon](https://github.com/tannerhelland/PhotoDemon/).  It supports other gradients shapes (radial, conical, spiral, and more) and is much faster than the simple version linked here.
