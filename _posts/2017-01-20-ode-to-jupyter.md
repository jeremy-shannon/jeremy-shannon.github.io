---
layout: post
title:  "Ode to Jupyter"
date:   2017-01-20 21:00:00 
categories: jupyter, python, udacity
---

![Jupyter logo](https://avatars3.githubusercontent.com/u/7388996?v=3&s=200)

I'd just like to take a moment to profess my love of Jupyter. It's a... well, how the crap do I describe it? It's a really great way to share code, for one. It's an *incredible* teaching tool as well, and the folks over at Udacity have obviously caught on to this. [The first two projects of the Self-Driving Car Engineer Nanodegree were implemented as Jupyter notebooks](https://github.com/jeremy-shannon/CarND-LaneLines-P1/blob/master/P1.ipynb), as were the exercises for the Deep Learning course.

A Jupyter notebook is a document that exists in the browser and comingles blocks of markdown with blocks of code. Not only that, the code blocks can be executed from within the notebook and their output is displayed directly below. The notebook is actually run as a local server and accessed through the browser. Code blocks are actually executed in the background, but the output persists in the notebook. So when you're done all of your code and output is saved to the notebook, which can be shared as-is or exported to pdf, html, or other formats. This makes it great for sharing your *process* with others. Udacity makes great use of it by interspersing text blocks with project instructions and code blocks with starter code already filled in. 

It's not a perfect medium, by any means. Compared to using an IDE or text editor it can be a little clunky, and I certainly wouldn't want to use it to build anything remotely large. But for its intended purpose, it really shines. One caveat: it can get confusing because the code blocks are all being run in the same kernel. So, for instance, going back and running a earlier block can overwrite a value from a subsequent block, so it's important to be mindful of the state of the kernel. When in doubt, I've found it's always best to "Restart and Run All" but that can be a real pain in the ass if you have some long-running blocks of code. Regardless, I'm hooked.
