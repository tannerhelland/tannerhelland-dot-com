---
author: tanner_h
date: 2008-06-19 20:55:08+00:00
layout: post
slug: screen-capture-vb6
title: How to capture the screen in VB6
redirect_from:
  - /44/screen-capture-vb6
  - /vb6/screen-capture-vb6
---

There are multiple ways to capture the screen in VB6. I recommend the following method for several reasons:

  1. It's reliable.  These APIs offer consistent results across all modern Windows versions.
  2. It's simple.  Each API call serves a logical purpose, and I've detailed those below.
  3. It's fast.  The code can easily be modified to operate on a timer system, for example.

You can download the sample project, or simply copy-and-paste this code into any blank form:
    
    'Screen Capture Demo by Tanner Helland (published 2008, updated 2012)
    ' http://www.tannerhelland.com
    
    'This call gives us the hWnd (window handle) of the screen
    Private Declare Function GetDesktopWindow Lib "user32" () As Long
    
    'This call assigns an hDC (handle of device context) from an hWnd
    Private Declare Function GetDC Lib "user32" (ByVal hWnd As Long) As Long
    
    'BitBlt lets us draw an image from a hDC to another hDC (in our case, from an hDC of the screen capture
    ' to the hDC of a VB picture box)
    Private Declare Function BitBlt Lib "gdi32" (ByVal hDC As Long, ByVal x As Long, ByVal y As Long, _
      ByVal nWidth As Long, ByVal nHeight As Long, ByVal hSrcDC As Long, ByVal xSrc As Long, _
      ByVal ySrc As Long, ByVal opCode As Long) As Long
    
    'ReleaseDC will be used to release the screen's hDC once the screen capture is complete.
    Private Declare Function ReleaseDC Lib "user32" (ByVal hWnd As Long, ByVal hDC As Long) As Long
    
    'This sample project copies the screen when the form loads; you could also place this code in
    ' a command button (or any other input)
    Private Sub Form_Load()
    
        'First, minimize this window
        Me.WindowState = vbMinimized
        
        'Get the hWnd of the screen
        Dim scrHwnd As Long
        scrHwnd = GetDesktopWindow
        
        'Now, assign an hDC to the hWnd we generated
        Dim shDC As Long
        shDC = GetDC(scrHwnd)
        
        'Determine the size of the screen
        Dim screenWidth As Long, screenHeight As Long
        screenWidth = Screen.Width \ Screen.TwipsPerPixelX
        screenHeight = Screen.Height \ Screen.TwipsPerPixelY
        
        'Copy the data from the screen hDC to this VB form
        BitBlt FormScreenCapture.hDC, 0, 0, screenWidth, screenHeight, shDC, 0, 0, vbSrcCopy
    
        'Release our hold on the screen's hDC
        ReleaseDC scrHwnd, shDC
        
        'Set the picture of the form to equal its image
        FormScreenCapture.Picture = FormScreenCapture.Image
        
        'Restore the window
        Me.WindowState = vbNormal
    
    End Sub
    
**[Download the sample app and source code from GitHub](https://github.com/tannerhelland/vb6-code/tree/master/Screen-capture)**
