---
layout: post
title:  "FBF: Display Station"
date:   2017-03-24 21:00:00 
categories: FBF, HP, display station, emulation, ncurses
---

[//]: # (Image References)
[im01]: https://github.com/jeremy-shannon/jeremy-shannon.github.io/blob/master/images/display_station/display_station.PNG?raw=true "Display Station"
[im02]: https://github.com/jeremy-shannon/jeremy-shannon.github.io/blob/master/images/display_station/old_test_station.jpg?raw=true "Old-Ass Test Station"
[im03]: https://github.com/jeremy-shannon/jeremy-shannon.github.io/blob/master/images/display_station/2645A.PNG?raw=true "2645A"
[im04]: https://github.com/jeremy-shannon/jeremy-shannon.github.io/blob/master/images/display_station/2645A_ad.PNG?raw=true "2645A Advertisement"

*In my Flashback Friday series I'm going to sift through my memory for some wins. Who knows what I'll find in there?!*

![Alt Text][im01]

Way back in the year 2014 I had the privilege of working on probably one of the most ambitious projects (at least as far as "organic" projects go - meaning no contractor involvement) I've ever encountered in my fifteen years of civil service - replacing the I/O terminal for one of those ancient electronics test stations that were once my bread and butter. Here's an idea of what it looked like (not the actual test station I'm referring to, but close enough):

![Alt Text][im02]

*What's up, man?*

And the I/O terminal... the inimitable (or *was* it?) Hewlett-Packard 2645A: 

![Alt Text][im03]

A real sight for sore eyes. Did I mention that the year was *2014*?! All of the other test stations I'd used up to this point were either replaced entirely with something modern, in the process of being replaced, or at least had their woeful CRT I/O terminals replaced with an LCD monitor and something that runs a semi-modern operating system. For whatever reason (mostly security concerns, I'd imagine) this one had to wait until it became absolutely necessary.

The project had actually started long before I moved to this particular organization, and a contractor had already failed to produce a working replacement. So the program manager took a chance on a scrappy team of civilian engineers... and hit pay dirt. By the time I came up to speed there was little left to do, but plenty to learn. It was my first real experience with Linux (the terminal emulation application was built on a custom locked-the-F-down version of [Gentoo](https://gentoo.org/)) and my first substantial practical application of C. It relied heavily on the [ncurses library](https://www.gnu.org/software/ncurses/) (which I took home and built a primitive "[Roguelike](https://en.wikipedia.org/wiki/Roguelike)" out of to help demonstrate to my nephew that it would, indeed, take a really long time to program GTA). My big feature was the "softkey menu" which opened a separate window where the user could define their own macros. Oh, and the user manual - I did that too.

Some of the more interesting things I recall from this project are:

- The OS was so tightly locked down that the only way to transfer and merge code from separate development stations was via CD-ROM.
- Serial port sniffing was essential every step of the way, and one of the idosyncrasies that I remember best was that the station would randomly transmit `ENQ`s, to which the terminal had to *immediately* respond with an `ACK` or else the whole thing went to hell.
- Last I'd heard, it still hadn't been fully fielded. *d'oh!*
 
I'll leave you with a relic from the golden age of advertising (in my opinion, anyway... probably because I was born then) - the late 1970's. Pay a visit to the [HP Computer Museum](http://hpmuseum.net/display_item.php?hw=240) to learn more - whoever runs that site is doing humanity a great service.

![Alt Text][im04]
