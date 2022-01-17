---
author: tanner_h
date: 2012-09-18 02:58:56+00:00
excerpt: While working on a "Color Temperature" tool for PhotoDemon,
  I spent an evening trying to track down a simple, straightforward algorithm for
  converting between temperature (in Kelvin) and RGB values.  This seemed like an
  easy algorithm to find, since many photo editors provide tools for correcting an
  image's color temperature in post-production, and every modern camera - including
  smartphones - provides a way to adjust white balance based on the lighting conditions
  of a shot.  Who knew that no one on the Internet had ever devised such a thing?
layout: post
slug: convert-temperature-rgb-algorithm-code
title: 'How to Convert Temperature (K) to RGB: Algorithm and Sample Code'
redirect_from:
 - /4435/convert-temperature-rgb-algorithm-code
 - /4435/convert-temperature-rgb-algorithm-code/
---

## Converting temperature (Kelvin) to RGB: an overview

If you don't know what "color temperature" is, [start here](http://en.wikipedia.org/wiki/Color_temperature).

While working on a "Color Temperature" tool for [PhotoDemon](https://photodemon.org), I spent an evening trying to track down a simple, straightforward algorithm for converting between temperature (in Kelvin) and RGB values.  This seemed like an easy algorithm to find, since many photo editors provide tools for correcting an image's color temperature in post-production, and every modern camera - including smartphones - provides a way to adjust white balance based on the lighting conditions of a shot.

![](images/camera_white_balance-300x235.jpg)

 Example of a camera white balance screen.  Image courtesy of [http://digitalcamerareviews2011online.blogspot.com](http://digitalcamerareviews2011online.blogspot.com/2011/08/understanding-white-balance-setting-on.html)

Little did I know, but it's pretty much impossible to find a reliable temperature to RGB conversion formula.  Granted, there are some algorithms out there, but most work by converting temperature to the XYZ color space, to which you could add your own RGB transformation after the fact.  Such algorithms seem to be based off AR Robertson's method, one implementation of which is [here](http://www.brucelindbloom.com/index.html?Eqn_XYZ_to_T.html), while another is [here](http://www.fourmilab.ch/documents/specrend/specrend.c).

Unfortunately, that approach isn't really a mathematical formula - it's just glorified look-up table interpolation.  That might be a reasonable solution under certain circumstances, but when you factor in the additional XYZ -> RGB transformation required, it's just too slow and overwrought for simple real-time color temperature adjustment.

So I wrote my own algorithm, and it works pretty damn well.  Here's how I did it.

## Caveats for using this algorithm

**Caveat 1**: my algorithm provides a high-quality approximation, but it's not accurate enough for serious scientific use.  It's designed primarily for photo manipulation - so don't try and use it for astronomy or medical imaging.

**Caveat 2**: due to its relative simplicity, this algorithm is fast enough to work in real-time on reasonably sized images (I tested it on 12 megapixel shots), but for best results you should apply mathematical optimizations specific to your programming language.  I'm presenting it here _without_ math optimizations so as to not over-complicate it.

**Caveat 3**: this algorithm is only designed to be used between 1000 K and 40000 K, which is a nice spectrum for photography.  (Actually, it's way larger than most photographic situations call for.)  While it will work for temperatures outside these ranges, estimation quality will decline.

## Special thanks to Mitchell Charity

First off, I owe a big debt of gratitude to the source data I used to generate these algorithms - Mitchell Charity's raw blackbody datafile at [http://www.vendian.org/mncharity/dir3/blackbody/UnstableURLs/bbr_color.html](http://www.vendian.org/mncharity/dir3/blackbody/UnstableURLs/bbr_color.html).  Charity provides two datasets, and my algorithm uses the [CIE 1964 10-degree color matching function](http://cvrl.ioo.ucl.ac.uk/database/text/cmfs/ciexyz64.htm).  A discussion of the CIE 1931 2-degree CMF with Judd Vos corrections versus the 1964 10-degree set is way beyond the scope of this article, but you can [start here](http://www.vendian.org/mncharity/dir3/blackbody/parameters.html) for a more comprehensive analysis if you're so inclined.

## The Algorithm: sample output

Here's the output of the algorithm from 1000 K to 40000 K:

![](images/Temperature_to_RGB_1000_to_40000.png)

The white point occurs at 6500-6600 K, which is perfect for photo manipulation purposes on a modern LCD monitor.

Here's a more detailed shot of the algorithm in the interesting photographic range, which is 1500 K to 15000 K:

![](images/Temperature_to_RGB_1500_to_15000.png)

As you can see, banding is minimal - which is a big improvement over the aforementioned look-up table methods.  The algorithm also does a great job of preserving the slightly yellow cast leading up to the white point, which is important for imitating daylight in post-production photo manipulation.

## How I arrived at this algorithm

My first step in reverse-engineering a reliable formula was to plot [Charity's original blackbody values](http://www.vendian.org/mncharity/dir3/blackbody/UnstableURLs/bbr_color.html).  You can download my whole worksheet [here in LibreOffice / OpenOffice .ods format (430kb)](files/Temperature_to_RGB_Worksheet.ods).

Here's how the data looks when plotted:

![](images/Raw_temperature_vs_RGB_chart.png)

*Mitchell Charity's original Temperature (K) to RGB (sRGB) data, plotted in LibreOffice Calc.  Again, these are based off the CIE 1964 10-degree CMFs.  The white point, as desired, occurs between 6500 K and 6600 K (the peak on the left-hand side of the chart). (Source: [http://www.vendian.org/mncharity/dir3/blackbody/UnstableURLs/bbr_color.html](http://www.vendian.org/mncharity/dir3/blackbody/UnstableURLs/bbr_color.html))*

From this, it's easy to note that there are a few floors and ceilings that make our algorithm easier.  Specifically:

  * Red values below 6600 K are always 255
  * Blue values below 2000 K are always 0
  * Blue values above 6500 K are always 255

It's also important to note that for purposes of fitting a curve to the data, green is best treated as two separate curves - one for temperatures below 6600 K, and a separate one for temperatures above that point.

From here, I separated the data (without the "always 0" and "always 255" segments) into individual color components.  In a perfect world, a curve could then be fitted to each set of points, but unfortunately it wasn't that simple.  Because there's a large disparity between the X and Y values in the plot - the x-values are all over 1000, and they are plotted in 100 point segments, while the y values all fall between 255 and 0 - it was necessary to transpose the x data in order to get a better fit.  For optimization purposes, I stuck to first dividing the x value (the temperature) by 100 across each color, followed by an additional subtraction if it led to a significantly better fit.  Here are the resultant charts for each curve, along with the best-fit curve and corresponding R-squared value:

![](images/Modified_Temperature_to_Red_plot.png)

![](images/Modified_Temperature_to_Green_plot.png)

![](images/Modified_Temperature_to_Green_plot_2.png)

![](images/Modified_Temperature_to_Blue_plot.png)

Apologies for the horrifically poor font kerning and hinting in those charts.  I love LibreOffice for many things, but its inability to do font aliasing on charts is downright shameful.  I also don't like having to extract charts from screenshots because they don't have an export option, but that's a rant best saved for some other day.

As you can see, the curves all fit reasonably well, with R-square values above .987.  I could have spent more time really tweaking the curves, but for purposes of photo manipulation these are plenty close enough.  No layperson is going to be able to tell that the curves don't exactly fit raw idealized blackbody observations, right?

## The algorithm

Using that data, here's the algorithm, in all its glory.

First, pseudocode:
    
	Start with a temperature, in Kelvin, somewhere between 1000 and 40000.  (Other values may work,
	 but I can't make any promises about the quality of the algorithm's estimates above 40000 K.)
	Note also that the temperature and color variables need to be declared as floating-point.

	Set Temperature = Temperature \ 100
	
	Calculate Red:

	If Temperature <= 66 Then
		Red = 255
	Else
		Red = Temperature - 60
		Red = 329.698727446 * (Red ^ -0.1332047592)
		If Red < 0 Then Red = 0
		If Red > 255 Then Red = 255
	End If
	
	Calculate Green:

	If Temperature <= 66 Then
		Green = Temperature
		Green = 99.4708025861 * Ln(Green) - 161.1195681661
		If Green < 0 Then Green = 0
		If Green > 255 Then Green = 255
	Else
		Green = Temperature - 60
		Green = 288.1221695283 * (Green ^ -0.0755148492)
		If Green < 0 Then Green = 0
		If Green > 255 Then Green = 255
	End If
	
	Calculate Blue:

	If Temperature >= 66 Then
		Blue = 255
	Else

		If Temperature <= 19 Then
			Blue = 0
		Else
			Blue = Temperature - 10
			Blue = 138.5177312231 * Ln(Blue) - 305.0447927307
			If Blue < 0 Then Blue = 0
			If Blue > 255 Then Blue = 255
		End If

	End If
    
In the pseudocode above, note that [Ln() means natural logarithm](http://en.wikipedia.org/wiki/Natural_logarithm).  Note also that you can omit the "If color < 0" checks if you will only ever supply temperatures in the recommended range.  (You still need to leave the "If color > 255" checks, though.)

As for actual code, here's the exact Visual Basic function I'm using in [PhotoDemon](https://photodemon.org).  It's not yet optimized (for example, the logarithms would be much faster via look-up table) but at least the code is short and readable:
    
    'Given a temperature (in Kelvin), estimate an RGB equivalent
    Private Sub getRGBfromTemperature(ByRef r As Long, ByRef g As Long, ByRef b As Long, ByVal tmpKelvin As Long)
    
        Static tmpCalc As Double
    
        'Temperature must fall between 1000 and 40000 degrees
        If tmpKelvin < 1000 Then tmpKelvin = 1000
        If tmpKelvin > 40000 Then tmpKelvin = 40000
        
        'All calculations require tmpKelvin \ 100, so only do the conversion once
        tmpKelvin = tmpKelvin \ 100
        
        'Calculate each color in turn
        
        'First: red
        If tmpKelvin <= 66 Then
            r = 255
        Else
            'Note: the R-squared value for this approximation is .988
            tmpCalc = tmpKelvin - 60
            tmpCalc = 329.698727446 * (tmpCalc ^ -0.1332047592)
            r = tmpCalc
            If r < 0 Then r = 0
            If r > 255 Then r = 255
        End If
        
        'Second: green
        If tmpKelvin <= 66 Then
            'Note: the R-squared value for this approximation is .996
            tmpCalc = tmpKelvin
            tmpCalc = 99.4708025861 * Log(tmpCalc) - 161.1195681661
            g = tmpCalc
            If g < 0 Then g = 0
            If g > 255 Then g = 255
        Else
            'Note: the R-squared value for this approximation is .987
            tmpCalc = tmpKelvin - 60
            tmpCalc = 288.1221695283 * (tmpCalc ^ -0.0755148492)
            g = tmpCalc
            If g < 0 Then g = 0
            If g > 255 Then g = 255
        End If
        
        'Third: blue
        If tmpKelvin >= 66 Then
            b = 255
        ElseIf tmpKelvin <= 19 Then
            b = 0
        Else
            'Note: the R-squared value for this approximation is .998
            tmpCalc = tmpKelvin - 10
            tmpCalc = 138.5177312231 * Log(tmpCalc) - 305.0447927307
            
            b = tmpCalc
            If b < 0 Then b = 0
            If b > 255 Then b = 255
        End If
        
    End Sub
    
This function was used to generate the sample output near the start of this article, so I can guarantee that it works.

## Sample images

Here's a great example of what color temperature adjustments can do.  The image below – a promotional poster for the HBO series True Blood – nicely demonstrates the potential of color temperature adjustments. On the left is the original shot; on the right, a color temperature adjustment using the code above. In one click, a nighttime scene can been recast in daylight.

![](images/True_Blood_Color_Temperature_Demo-600x450.jpg)

The actual color temperature tool in [PhotoDemon](https://photodemon.org) looks like this:

![](images/PhotoDemon_50_Color_Temperature_Tool.jpg)

Download it [here](https://photodemon.org/download) to see it in action.

## addendum October 2014

[Renaud Bédard](https://twitter.com/renaudbedard) has put together a great online demonstration of this algorithm (including a translation to GLSL).  [Check it out here](https://www.shadertoy.com/view/lsSXW1), and thanks to Renaud for sharing!

## addendum April 2015

Neil B has helpfully provided a better version of the original curve-fitting functions, which results in slightly modified temperature coefficients.  [His excellent article](http://www.zombieprototypes.com/?p=210) describes the changes in detail.

## addendum January 2020

David has [ported this code to Swift](https://github.com/davidf2281/ColorTempToRGB).

Tom Yaxley has [ported it to javascript](http://tommitytom.co.uk/colourtemp/).

Christophe Carpentier has [ported it to Java](https://github.com/Saucistophe/libs/blob/master/global-lib/src/main/java/org/saucistophe/utils/ColorUtils.java).

Mike D Sutton has [ported it to node.js](https://gist.github.com/EDais/1ba1be0fe04eca66bbd588a6c9cbd666).

Robert Atkinson has [re-fit the data using Mathematica](https://github.com/rgatkinson/ParticleDmxNeopixel/tree/master/ColorTemperature) (which offers much more powerful fitting features than LibreOffice, obviously!).

## addendum November 2020

[m-lima](https://github.com/m-lima) has [ported this code to Rust](https://github.com/m-lima/temperagb).

## addendum January 2021

[petrklus](https://gist.github.com/petrklus) has [ported this code to python](https://gist.github.com/petrklus/b1f427accdf7438606a6).  (Thank you to [nestorst](https://github.com/nestorst) for notifying me!)

## addendum March 2021

[teckel12](https://github.com/teckel12) has [ported this code to PHP](https://github.com/teckel12/kelvins2RGB).

## addendum October 2021

[Haroon Atcha](https://github.com/haroonatcha) has [ported this code to R](https://github.com/haroonatcha/Aquarium-Pi/tree/main/led_code).

## addendum January 2022
[Kiryl Ambrazheichyk](https://github.com/ibober) has [ported this code to C#](https://gist.github.com/ibober/6b5a6e1dea888c01c0af175e71b15fa4).
