---
layout: post
title:  "Udacity Self-Driving Car Nanodegree Project 9 - PID Control"
date:   2017-06-16 21:00:00 
categories: udacity, self-driving car, nanodegree, project, pid control
---

The ninth project for the Udacity Self-Driving Car Engineer Nanodegree Program and the fourth for Term 2, PID Control, reprised most of what I had learned on this very topic way back in November and December of last year when I took and blogged about [Udacity's Artificial Intelligence for Robotics course](http://jeremyshannon.com/2016/12/09/udacity-artificial-intellgence-for-robotics-pt-2.html). Here's what I had to say about it back then:

> The next topic was PID control. This unit took me back to Control Theory class back in my undergrad days. I probably best recall being blown away by the [analogs between control devices in electrical and mechanical applications](http://lpsa.swarthmore.edu/Analogs/ElectricalMechanicalAnalogs.html) - resistors, capacitors, and inductors behave analogously to dashpots (dampers), springs, and masses. And the principles apply to programming robotics, using proportional, integral, and differential (PID) controls to apply motion directly, counteract bias, and dampen ringing respectively. Fun stuff.

I guess I was keeping it brief back then. That's fine; [this video](https://youtu.be/4Y7zG48uHRo) does a far better job of explaining the concept than I did then or could do now. What's missing is a way to tune the P, I, and D parameters to get that controller working *juuuuuuust* right... unless you want to tune them by hand, ya psychopath.

In the AI for Robotics course and again in the Nanodegree lessons, we learned about a little trick Sebastian Thrun likes to call "Twiddle." It's a "local hill-climber" optimization routine that iterates through each parameter, makes a change (both positive and negative), and if it improves the controller we keep the change and try a larger change next time, otherwise we discard the change and try a smaller change next time. It eventually converges, after making smaller and smaller changes, to an optimum (but not necessarily *the* optimum) solution.

The project made use of our familiar simulator friend from [the Behavioral Cloning project](http://jeremyshannon.com/2017/02/10/udacity-sdcnd-behavioral-cloning.html), which transmitted cross-track error and other telemetry data to our own program. It was there that we implemented the PID controller to respond with steering and throttle commands. The rough spot, when compared to the mini-project in the AI for Robotics course (for which you could veer off as far as you want from the straight-line desired trajectory and Twiddle was fine with it), was the track itself which allowed very little room for error. Once the car drives off the track (and probably can't get back on) it's all over for that set of parameters and the Twiddle routine itself (at least this iteration). Bummer! I was stuck tuning the parameters manually until the car was able to drive around the track by itself. Then I was able to Twiddle to my heart's content. 

There was another problem, though: In AI for Robotics we could Twiddle and evaluate the error in only a hundred steps since the conditions were consistent (Sebastian suggests first letting the parameters settle in for a hundred steps before beginning the evaluation, but this simple version still converged in seconds). But in order to get a consistent error evaluation on the curvy simulator track, I didn't see any option aside from evaluating for a full lap around the track. What if a would-be better set of parameters were rejected because it had to contend with an especially sharp turn instead of a straight stretch of track? I set my evaluation length to around 2,000 steps and let the thing Twiddle the day away making 500 laps around the track.

Udacity also suggested we try to implement a PID controller for the throttle. It wasn't required, but I'd hate to get a reputation for shying away from a challenge (I'm looking at you, hiring managers!). The throttle controller worked mostly the same, but because a positive error on one side of the center line and a negative error on the other wouldn't make much sense where throttle is concerned I used the magnitude of the CTE. This also meant that I had to dispense with the I component of the controller, which would have grown indefinitely causing the car to eventually stop and reverse at full throttle indefinitely. I set a limit of 70% of full throttle for the controller, which worked nicely. I was able to complete a number of laps at 100% full throttle, but it always fell of the track at some point. 

I'll leave you with a video chronicling my journey; next time we'll be graduating to the more sophisticated Model Predictive Controller.

<a href="https://youtu.be/GJNoVgHcSCw"><img src="https://img.youtube.com/vi/GJNoVgHcSCw/0.jpg"></a>

*The source code for this project can be found [on my GitHub](https://github.com/jeremy-shannon/CarND-PID-Control-Project)*
