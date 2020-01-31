---
author: tanner_h
date: 2008-12-24 22:19:34+00:00
excerpt: Who doesn't love a classic tile-based game?  This demo is largely self-explanatory - click on the tile bar at the top (with either the left or right mouse button) to select a tile, then click on the large center window to draw that tile onto the map.  Scrolling and zoom are fully implemented, as are saving and loading map files.  
layout: post
slug: tile-based-editor
title: Building a simple 2D tile-based map editor
redirect_from:
 - /328/tile-based-editor
---

Who doesn't love a classic tile-based game?  I've seen many beginning programmers try to tackle a project like this, and unfortunately, they tend to use massive collections of image or picture controls to do it.  This is hugely overkill, as it's much faster to use a single surface and simply track tile indices yourself.

This demonstration of such a technique is largely self-explanatory.  Click on the tile bar at the top (with either the left or right mouse button) to select a tile, then click on the large center window to draw that tile onto the map.  Scrolling and zoom are fully implemented, as are saving and loading map files.  

[![screenshot](images/2d_map_editor.png)](images/2d_map_editor.png)

The included tile set isn't especially nice, but I hope it provides a good demo of how you might start work on a 2D game.

**[Download the sample app and source code from GitHub](https://github.com/tannerhelland/vb6-code/tree/master/Map-editor-2D)**