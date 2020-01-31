---
author: tanner_h
date: 2009-03-05 04:55:27+00:00
layout: page
slug: code
title: Code
redirect_from:
  - /programming-directory/
  - /category/vb6
  - /category/vb6/page/2
  - /category/vb6/page/3
  - /photodemon-contact
  - /photodemon
  - /category/vb6/feed
  - /category/vb6/graphics-tutorial
  - /category/vb6/graphics-vb6/page/2
  - /category/vb6/graphics-vb6
---

[All code on this site](https://github.com/tannerhelland/vb6-code) is provided free of charge, under [a permissive BSD license](https://github.com/tannerhelland/vb6-code/blob/master/LICENSE.md).  If you find the code helpful, please consider a small donation to help me support my family.  Even $1.00 helps.  Thank you!

<form action="https://www.paypal.com/cgi-bin/webscr" method="post" target="_top">
<input type="hidden" name="cmd" value="_s-xclick">
<input type="hidden" name="hosted_button_id" value="44MDJMBLH88G6">
<input type="image" src="https://www.paypal.com/en_US/i/btn/btn_donateCC_LG.gif" border="0" name="submit" alt="PayPal - The safer, easier way to pay online!">
<img alt="" border="0" src="https://www.paypalobjects.com/en_US/i/scr/pixel.gif" width="1" height="1">
</form>
<br />

## Full applications
    
  * [PhotoDemon - the fast, free, portable photo editor](https://photodemon.org)

## Small sample applications

All source code for the following projects is hosted in [a single GitHub repository](https://github.com/tannerhelland/vb6-code).  Feel free to clone the entire repository, or browse individual project pages below.

## Bioinformatics

  * [Hidden Markov Models, the Viterbi Algorithm, and CpG Islands](2009/08/17/hidden-markov-models-viterbi-algorithm-cpg-islands)
  * [Evolution and Artificial Life Simulators](2009/12/21/artificial-life-simulator-vb6)

## Games

  * [Basic game physics (velocity and acceleration)](499/game-physics-demo/)    
  * [Building a tile-based map editor](328/tile-based-editor/)
  * [Mathematically generated fire](640/mathematical-fire-code-2/)

## Graphics and Imaging

**Color-Depth Conversions**
    
  * [Seven grayscale conversion algorithms](3643/grayscale-image-algorithm-vb6/)
  * ["Colorizing" images](3552/colorize-image-vb6/)
  * [Image dithering: eleven algorithms and source code](4660/dithering-eleven-algorithms-source-code/)

**Fractals**
    
  * [Drawing the Mandelbrot Set / fractal](1494/mandelbrot-vb6/)

**Histogram-Related Image Processing**
    
  * [Image Histograms Part 1 (histogram generation)](747/vb6-image-histograms-1/)
  * [Image Histograms Part 2 (stretching and equalizing)](810/vb6-image-histograms-2/)
  * [How to build a "Curves" dialog](336/image-curves-vb6/)
  * [How to build a "Levels" dialog (input / output / midtone)](341/image-levels-vb6/)
  * [Real-time image contrast](2008/06/19/image-contrast-vb6)

**Basic Image Processing**
    
  * [Filling contiguous image regions (via ExtFloodFill)](649/fill-image-regions/)
  * [Screen capturing via the Windows API](2008/06/19/screen-capture-vb6)
  * [Smooth color gradients (linear, real-time)](47/gradients-vb6/)

**Advanced Image Processing (Including Filters and FX)**
    
  * [Image edge detection](952/edge-detection-vb6/)
  * [Correcting lens distortion](4743/simple-algorithm-correcting-lens-distortion/)
  * [Converting color temperature (K) to RGB](4435/convert-temperature-rgb-algorithm-code/)
  * [Building a custom image filter engine](982/custom-image-filters-vb6/)
  * [Variable alpha-transparency in real-time](490/image-blending-transparency/)
  * [Sepia / "Antique" color conversions](1138/sepia-antique-effect-vb6/)
  * [Blacklight effect](381/blacklight-vb6/)
  * [Color-shifting](474/color-shifting/)
  * [A collection of nature-inspired image filters](1118/nature-inspired-image-effects-vb6/)
  * [Emboss / engrave / relief filters](2225/generating-emboss-engrave-relief-filters-vb6/)
  * [Stained glass effect / polygon-based image randomization](2306/stained-glass-image-effect/)
  * [Diffuse (Spread) image filter](3601/realtime-diffuse-spread-image-filter-vb6/)

## Hardware Support
    
  * [How to use a scanner (or TWAIN-compatible digital camera) in VB6](4043/scanner-vb6/)

## Tutorials
    
  * [VB Graphics Programming: An Introduction](2008/06/17/vb-graphics-programming-0)
  * [VB Graphics Programming: Part 1 - Pure VB (PSet and Point)](2008/06/17/vb-graphics-programming-1)
  * [VB Graphics Programming: Part 2 - Beginning API (GetPixel and SetPixel)](2008/06/17/vb-graphics-programming-2)
  * [VB Graphics Programming: Part 3 - Advanced API (GetBitmapBits/SetBitmapBits and GetDIBits/StretchDIBits)](2008/06/17/vb-graphics-programming-3)
  * [VB Graphics Programming: Part 4 - Advanced Optimizations](2008/06/17/vb-graphics-programming-4)

## Why I use Classic VB for my code samples

In case you haven't noticed, I am a big fan of retro programming (_e.g._ using outdated programming languages to write modern pieces of software). While there are many good ways to practice retro programming, my favorite tool is Visual Basic 6.0.

...Yes, VB6. You can stop laughing now.

I was first introduced to Visual Basic in the form of VB 4.0, back in the era of choosing to compile a program as 16-bit or 32-bit. VB5 brought some much-needed improvements - including compiling to native code - and VB6 was largely a refinement of larger changes introduced in VB5. I continue to actively use VB6 on Windows 10.

When asked why I haven't switched to a more modern language, the answer is simple - I do most of my professional work in other, more "sophisticated" languages.  Java, C++, and Perl are especially prevalent in bioinformatics. 

But when I code as a hobby, I like to keep it as far removed from my paying work as possible. I suppose work on classic cars is a good analogy; there's something nostalgic about VB6, and I like that.

As an added bonus, VB code is practically pseudocode, making it easy to port VB functions to other languages. Even if you aren't familiar with specific VB semantics, it's hard to confuse the purpose of code like:
    
`luminance = (222 * red + 707 * green + 71 * blue) \ 1000`

In recent years, I've tried to add pseudocode descriptions to my most popular projects.  If you ever find a project with VB code you can't make sense of, [let me know](contact/) so I can post a language-agnostic pseudocode version on its project page.