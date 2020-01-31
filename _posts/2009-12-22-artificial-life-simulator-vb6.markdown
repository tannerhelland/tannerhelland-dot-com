---
author: tanner_h
date: 2009-12-22 06:09:11+00:00
excerpt: 'Here you have it: the largest, most complex programming project now available
  on tannerhelland.com. Originally a final project for a university bioinformatics
  course, this artificial life simulator has now been completely retooled as a full-blown
  lesson in evolution and population genetics.  As with most artificial life simulators,
  a set of simple artificial creatures compete for limited resources.  Each creature
  has a strand of pseudo-DNA that determines three basic attributes: size, speed,
  and range (how far it can see)...'
layout: post
slug: artificial-life-simulator-vb6
title: Artificial Life Simulator (in VB6)
redirect_from:
  - /1399/artificial-life-simulator-vb6/
  - /vb6/artificial-life-simulator-vb6/
  - /1399/artificial-life-simulator-vb6
  - /vb6/artificial-life-simulator-vb6
---

![This is what the Artificial Life Simulator looks like in action](images/Artificial_Life-600x467.png)

*Screenshot of the simulator in action*

**The Short Description:**

I wrote this little artificial life simulator as a final project for a university bioinformatics course.  It served as a fun (and informative!) lesson in evolution and population genetics.

As with most artificial life simulators, a set of simple artificial creatures compete for limited resources.   Each creature has a strand of pseudo-DNA that determines three basic attributes: size, speed, and range (how far it can see).  When the little critters reproduce (asexually, for better or worse), mutations may occur.  Over time, this leads to remarkable changes in gene frequency throughout the population.  Typically the creatures with a balance of speed and range tend to win out over bigger, slower creatures and smaller, faster ones.

The code is well-optimized, so it should run decently on any hardware.   As a bonus, the simulator can be surprisingly addicting - my longest simulation to date ran for over 500,000 cycles before all the creatures died.   For further analysis of a particular simulation run, all data can be saved to a tab-delimited text file compatible with any spreadsheet software.  (I did my final analysis in [LibreOffice](https://www.libreoffice.org/), the modern successor to OpenOffice.)

**The Long Description:**

Alongside the source code, I also wrote a full paper describing the artificial life simulator and its relationship to population genetics models.  

Unfortunately, due to repeat issues of plagiarism - where professors contacted me to let me know that one of their students attempted to pass off the project and paper as their own - I have since pulled the paper's text from this website.  

[This is why we can't have nice things](https://english.stackexchange.com/questions/417320/what-is-the-origin-of-the-phrase-this-is-why-we-cant-have-nice-things), etc.  

:(

**[Download the application and full source code from GitHub](https://github.com/tannerhelland/vb6-code/tree/master/Artificial-life)**