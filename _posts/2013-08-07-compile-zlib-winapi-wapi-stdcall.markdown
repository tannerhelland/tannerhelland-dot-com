---
author: tanner_h
date: 2013-08-07 14:12:27+00:00
excerpt: This is not a full-blown article - just a quick HOWTO for people who require
  the latest version of zLib and want to use it from a language (like classic VB)
  that requires a standard WinAPI interface.  You must compile zLib yourself using
  the free 2012 version of Visual Studio Express...
layout: post
slug: compile-zlib-winapi-wapi-stdcall
title: How to compile zLib 1.2.8 (WINAPI / WAPI / STDCALL version)
redirect_from:
 - /5076/compile-zlib-winapi-wapi-stdcall
 - /5076/compile-zlib-winapi-wapi-stdcall/
---

This is not a full-blown article - just a quick HOWTO for people who require the latest version of zLib and want to use it from a language (like classic VB) that requires a standard WinAPI interface.

By default, zLib uses C calling conventions (CDECL).  Gilles Vollant has helpfully provided [an STDCALL version of zLib](http://www.winimage.com/zLibDll/index.html) in the past, but his site only provides version 1.2.5, which dates back to January 2012.  zLib is currently on version 1.2.8.

Gilles has contributed his WAPI fixes to the core zLib distribution so that anyone can compile it themselves.  To do this, you will need to download:

  * The latest version of the zLib source code ([http://zlib.net/zlib128.zip](http://zlib.net/zlib128.zip) at the time of this writing).
  * The express version of Visual Studio 2012, freely downloadable from [http://www.microsoft.com/visualstudio/eng/products/visual-studio-express-products](http://www.microsoft.com/visualstudio/eng/products/visual-studio-express-products)

Once both of those are downloaded (and updated, as VS 2012 will require you to install several service packs), follow these steps to compile zLib yourself:

  1. Extract the entire zLib file and navigate to the /contrib/masmx86 folder.  Open the "bld_ml32.bat" file in a text editor.

  2. Add the "/safeseh" switch to both lines in that file (e.g. "ml /safeseh /coff /Zi /c /Flmatch686.lst match686.asm").  Then save and exit.

  3. Navigate to the /contrib/vstudio/vc11/ folder.  Open the zlibvc.sln file in your newly installed Visual Studio 2012 Express.

  4. In the Solution Explorer (top-right by default), right-click "zlibstat" then select "Properties" at the bottom.

  5. Go to Configuration Properties -> C/C++ -> Preprocessor, and in the Preprocessor Definitions line remove “ZLIB_WINAPI;” (don't forget to remove the trailing semicolon).

  6. Now, we need to fix a recently introduced problem that relies on Win8 functionality.  In the Solution Explorer, navigate to zlibvc -> iowin32.c.  Double-click to open the file.

  7. Find the line of text that reads "#if WINAPI_FAMILY_PARTITION(WINAPI_PARTITION_APP)".  Change this line to "#if WINAPI_FAMILY_ONE_PARTITION(WINAPI_FAMILY_DESKTOP_APP, WINAPI_PARTITION_APP)".  (Thanks to [this link](http://stackoverflow.com/questions/17102770/using-the-windows-8-sdk-to-compile-for-windows-7/17113126#17113126) for this fix.)

  8. zLib uses a Version number declaration that can cause the build process to fail.  To fix this, go back to the Solution Explorer, then navigate to zlibvc -> zlibvc.def.  Double-click to open.

  9. Change the line that reads "VERSION 1.2.8" to read "VERSION 1.28".

  10. Finally, go to the Build -> Configuration Manager menu and change the Active Solution Configuration to "Release".

  11. Exit that window and press F7 (or click the Build -> Build Solution menu).  The project should successfully build.

  12. You can find your newly compiled zlibwapi.dll file in the /contrib/vstudio/vc11/x86/ZlibDllRelease/ folder.

