---
layout: post
title:  "Udacity Self-Driving Car Engineer Nanodegree Program Term 1 Retrospective"
date:   2017-03-31 21:00:00 
categories: udacity, self-driving car, nanodegree, deep learning, computer vision
---

[//]: # (Image References)
[im01]: https://github.com/jeremy-shannon/jeremy-shannon.github.io/blob/master/images/IMG_3687.PNG?raw=true "Term 1 Retrospective"

![Alt Text][im01]

I kind of can't believe I've already finished Term 1 of the Nanodegree. It feels like it flew by, but also like it's been my whole life. I think I prepared myself more than I realized at the time when I took Udacity's Intro to Machine Learning, Artificial Intelligence for Robotics, and Deep Learning courses - as well as the first few units of Intro to Computer Vision - in the weeks leading up to the start of my cohort. I just kept that pace going into the Nanodegree and it served me well - I finished all of the projects on time (or even a week or two early, including the extra challenges), blogged every step of the way, researched and compiled a list of companies (I'm up to 134!) in or around the self-driving car industry which I shared with my fellow students, kept abreast of autonomous vehicle news, listened to AI and ML podcasts, and helped out my fellow students any time I could. 

It's been a hell of a ride so far, and I'm already working on Term 2 thanks to Udacity allowing us December students who finished early to start Term 2 with the November cohort. I joined a team doing [the Udacity Didi Challenge](https://www.udacity.com/didi-challenge), and I'm still blogging (I promise!) and consuming all the AV/ML/AI/DL/what-have-ya news. I get the feeling that when Term 3 ends I won't know what to do with myself!

Anyway, Term 1... takeaways? Let's see...

- The pace wasn't quite grueling, but it was clear that it was more than many of us had anticipated. Udacity obviously underestimated when they said it should require around ten hours a week, but considering we were part of the inaugural group of students I didn't feel I had grounds for surprise or disappointment when it turned out to require far more than that. I'm just thankful that I had already resolved to devote every spare moment to it. 
- Term 1 was devoted to computer vision and deep learning. I didn't realize going in that these are widely considered two conflicting schools of thought - the old way (computer vision) and the new way (deep learning) of doing things. 
- The OpenCV computer vision library is your one-stop-shop for all of your computer vision needs. We used the hell out of that library all term, and it's incredibly powerful. It felt like magic when a few simple method calls identified highway lane lines in Project 1, but it felt like very-much-not-magic when any change to the environment caused the whole processing pipeline to break down. It became apparent that the computer vision approach would be incredibly difficult to implement in a way that responds well to all potential circumstances (e.g. rain, snow, night). 
- Deep learning - now *that* really *is* magic. Want your thing to work in the rain? Give it some rainy data. Night? Give it night data (or, hell - just darken your daytime data artificially). It'll figure it out. Here's the catch, though: collecting and preparing all of that data, then countless hours trying to find a model that works (hopefully there's already one out there you can borrow from) and tuning it to achieve acceptable results - it's no small task, for sure. And on top of that, you don't really get any feedback or clues when your solution takes a massive crap on itself. But for a *big* problem like, (oh... let's just say...) cars that drive themselves, it very well may be your best bet.
- [Project 3](http://jeremyshannon.com/2017/02/10/udacity-sdcnd-behavioral-cloning.html) was a real treat, and to me was the centerpiece of the first term (I imagine Udacity felt the same). It was exciting and frustrating at the same time. But, *wow*, what a cool project to have in my portfolio! I'm glad to see Udacity's getting some more mileage out of the simulator they developed for it in Term 2, too.
- Along the way I picked up all sorts of new skills: Python, Numpy, TensorFlow, Keras, OpenCV, Jupyter, AWS EC2, and probably a few others.

I've learned so much, and yet I feel like we've only scratched the surface. I suppose that's just the way it goes, though. Like Einstein said,

> The more I learn, the more I realize how much I don't know.  

*Check out my individual blog posts for each of the Term 1 projects:*
- [Project 1 - Finding Lane Lines](http://jeremyshannon.com/2016/12/23/udacity-sdcnd-finding-lane-lines.html)
- [Project 2 - Traffic Sign Classification](http://jeremyshannon.com/2017/01/13/udacity-sdcnd-traffic-sign-classifier.html)
- [Project 3 - Behavioral Cloning](http://jeremyshannon.com/2017/02/10/udacity-sdcnd-behavioral-cloning.html)
- [Project 4 - Advanced Lane Finding](http://jeremyshannon.com/2017/03/03/udacity-sdcnd-advanced-lane-finding.html)
- [Project 5 - Vehicle Detection](http://jeremyshannon.com/2017/03/17/udacity-sdcnd-vehicle-detection.html)

