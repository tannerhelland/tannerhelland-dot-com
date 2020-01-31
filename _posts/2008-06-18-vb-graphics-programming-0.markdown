---
author: tanner_h
date: 2008-06-18 02:31:04+00:00
layout: post
slug: vb-graphics-programming-0
title: 'VB Graphics Programming: An Introduction'
redirect_from:
  - /39/vb-graphics-programming-0/
  - /vb6/vb-graphics-programming-0/
---

To any VB 6.0 users still out there:

In my experience, many VB programmers seem to believe that fast graphics programming is impossible in VB.  Most complain that PSet and Point (or GetPixel and SetPixel) just aren't fast enough for their needs, and they feel like they have to switch to an alternate language for any serious graphics-related coding.

This is most definitely not the case, and I hope by the end of these tutorials to have you feeling quite differently.

Using some creativity and efficient coding, you can use VB6 to do almost anything that C++, java, DirectX or OpenGL does - and almost always as fast (and in some cases faster!).  The code for DIB sections, the ultimate end of these tutorials, is not well-documented anywhere else on the net, so I have set out to clearly explain how extremely fast graphics-related code can be used inside Visual Basic without a lot of extra work or overly-cryptic API calls.

Also, unlike other programming tutorials, this series of articles will explain not only how to do fast graphics but how fast graphics work. You will first learn about pure VB routines for graphics processing; next comes the basic API routines of GetPixel and SetPixel/V; third comes the more advanced GetBitmapBits, SetBitmapBits, and DIB sections; the last tutorial will cover additional optimizations for the real speed demons out there. By the end of this series of tutorials you will be able to effectively write any graphics application you can dream up using nothing but VB6 and the Windows API.

But before we jump into the code, it's probably good to clarify a little bit about graphics programming in general.

**General Graphics Programming Stuff**

Graphics programming (hereafter referred to as GP) is, in my opinion, the most far-reaching aspect of programming. Every Windows, Linux, and Mac program that has been written in the last twenty years has utilized graphics in some way. Because of the popularity of GUI-based operating systems, every programmer has been forced to learn at least the fundamentals of GP, because any program they write must include little picture boxes, have nice buttons and toolbars, load with a pretty splash screen, etc.

Now it's true that some programs don't use many graphics routines - but every program you own uses some graphics.  Next time you turn on your computer, start thinking about all of the GP involved in simple, everyday routines, like clicking on your start bar, the animated folder that appears when you copy a file, that progress bar at the bottom of a window. You'll quickly be amazed at how many GP techniques are utilized within every program you run.

As you can imagine, a lot could be said about graphics programming.  I do not intend to talk about EVERYTHING graphics related, so here's the part of GP that this set of tutorials will cover: per-pixel image interface routines.  Basically, we're going to discuss how to get a picture's pixel information, how to transfer it into a data structure we can use (arrays), and how to put those pixels back onto the screen once we're done with them. We'll go from the easiest and slowest ways to the fastest and most advanced ways available to you, the common VB6 programmer.

What this tutorial will not cover is how to do specific image editing routines (please refer to the numerous source code examples on the internet for that), how to write graphics-based dlls or ocxs, or how to use DirectX. There are resources for each of these if you are interested; my goal is simply to outline the standard Windows API methods for per-pixel image interfacing.

Are you excited?  You should be!  On to the tutorials!

**[Continue to Part 2: Pure VB Pixel Routines](2008/06/17/vb-graphics-programming-1)**
