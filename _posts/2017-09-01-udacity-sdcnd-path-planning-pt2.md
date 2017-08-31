---
layout: post
title:  "Udacity Self-Driving Car Nanodegree Project 11 - Path Planning - Part 2"
date:   2017-09-01 21:00:00 
categories: udacity, self-driving car, nanodegree, project, path planning
---

![Path Planning cover image](https://github.com/jeremy-shannon/jeremy-shannon.github.io/blob/master/images/path_planning/pp_cover2.png?raw=true)

Last time, in [part 1](http://jeremyshannon.com/2017/08/25/udacity-sdcnd-path-planning-pt1.html) of this horror story, I told you about my first crack at the [Udacity Self-Driving Car Engineer Nanodegree's](https://udacity.com/drive/) Path Planning project. To review:

> This project again put the Udacity simulator to use, this time in a highway driving scenario. The goal is to drive the entire 4.32 mile length of the gently curvy, looping track at near the posted speed limit while navigating traffic and without any "incidents" which include: driving over the speed limit, exceeding limits on acceleration and jerk (i.e. the change in acceleration over time, which can make for an uncomfortable ride), driving outside of the lanes, and, of course, colliding with other cars. The simulator expects of us a list of (x,y) map coordinates, each of which our car will obediently visit at 0.02 second intervals (even if that means violating every law of physics). In return, the simulator provides us with telemetry data for our car (position, heading, velocity, etc.), sensor fusion data for the other cars (on our side of the highway), and whatever points of the last path the car hadn't already visited. We are also provided a .csv file that lists track waypoints. We can then use this data to determine a trajectory, convert it to a set of x and y points, and tack these points onto the end of however many points of the previous path we've decided to keep (this can help to account for latency between our planner and the simulator and, if you're like me, it can also serve to artificially smooth the transition to a new trajectory).

> My implementation, at least the first go-around, looked something like this: 

> 1. Interpolate the waypoints for a nearby portion of track (this helped to get more accurate conversions)
> 2. Determine the state of our own car (current position, velocity, and acceleration projected out a certain amount of time based on how much of the previous path was retained)
> 3. Produce a set of rough predicted trajectories for each of the other vehicles on the road (assuming a constant speed)
> 4. Determine the "states" available for our car (in this case, "keep lane," "change lanes to right," or "change lanes to the left")
> 5. Generate a target end state (position, velocity, and acceleration) and a number of randomized potential trajectories (with elements of the target state perturbed slightly) for each available state (these ["Jerk-Minimized Trajectories" (JMTs)](http://mplab.ucsd.edu/tutorials/minimumJerk.pdf) are [quintic polynomials](https://en.wikipedia.org/wiki/Quintic_function) solved based on our current initial and desired final values for position, velocity, and acceleration)
> 6. Evaluate each of these possible trajectories against a set of cost functions (rewarding efficiency and punishing things like collisions, higher average jerk, or exceeding the speed limit, for example)
> 7. Choose the best (i.e. lowest-cost) trajectory
> 8. Evaluate it at the next several 20-millisecond intervals
> 9. Tack those onto the retained previous path, and 
> 10. Return the new path to the simulator

So then Udacity released their walkthrough. There were no predictions, no quintic polynomials, no perturbed trajectories. In fact, the trajectories being sent to the simulator were "hand processed", so to speak. Each new point in the path is placed (using the very simple [spline library](http://kluge.in-chemnitz.de/opensource/spline/)) based on a curve that fits latitudinal (y) position against longitudinal (x) position and is evaluated at x points calculated based on desired velocity (which is hard-limited to prevent excessive acceleration and jerk). In other words, fit a curve from the end of the previous path to the desired location (say, the middle lane 30 meters ahead) and add points from that curve that satisfy motion constraints to the new path. If there's another car ahead we slow down to an arbitrary speed, and if there's no car in the next lane we move over there.

My first inclination was to trash all of my current code (maybe even poison it and set it on fire, while I'm at it) and duplicate the walkthrough code exactly. Hadn't I already invested enough time in this? But cooler heads prevailed and I decided to adapt quite a bit of my existing code. I kept the waypoint interpolation because, like I said, it helps to get more accurate conversions and it also handles problems at the wrapping point (where the distance along the track goes from 6945.554 meters to zero meters). It still calculates the "current" (or "planning") state of the car at the end of the retained previous path, determines available states and a target for each, generates a trajectory for each target and predictions for other cars, and evaluates trajectories based on cost functions and chooses the best.

I also made quite a few changes. No more randomized, perturbed trajectories. And rather than build the new path points by evaluating the jerk-minimized trajectory at the next 20-millisecond intervals, I employ a method similar to the walkthrough - creating a spline from the end of the previous points to the already-determined target and evaluating that at longitudinal points that satisfy motion constraints (thankfully my target velocity was also already being determined and corrected for any traffic in my lane), and converting those points into map coordinates. That made all the difference - my car was driving smoothly now. Praise be!

Now, bear in mind that I was still using the JMT and evaluating targets based on the costs calculated for their associated trajectories. These trajectories might not necessarily match what the spline produces in the end, but I simplified the cost functions and decreased the resolution on the trajectories (evaluating them at twenty points 0.2 seconds apart) in hopes that the difference between JMT and spline trajectories is negligible compared to the difference between the trajectories for different targets. Based on this image (which you may remember from [last time](http://jeremyshannon.com/2017/08/25/udacity-sdcnd-path-planning-pt1.html)) and the car's performance, that would appear to be the case.

![Sensor fusion data visualization](https://github.com/jeremy-shannon/jeremy-shannon.github.io/blob/master/images/path_planning/sensor_fusion_2.png?raw=true)

The cost functions I settled on in the final implementation are, in order of importance: collision cost (don't hit other cars, duh!), efficiency cost (go as fast as you can, within constraints of course), in-lane buffer cost (prefer lanes with more room to go full speed), not-middle-lane cost (we like to stay in the middle lane when we can, since it affords more options than other lanes), and buffer cost (try to keep some distance from other cars, in any direction). I ditched several cost functions that had to do with perturbing targets or constraining motion (since I limit that explicitly now). 

As an aside, I'd like to take a moment to express my fondness for cost functions. It's a concept that is relatively new to me and one that seems fairly unique to artificial intelligence. It's not too unlike machine/deep learning in the "don't be explicit - let the computer figure it out" sense, but it's more like another dimension of relenting control since you can turn a supervised learning application into a reinforcement learning application using cost functions instead of a more rigid, singular loss function. (That's how I see it, anyway.) Fascinating.

Anyway, the one other noteworthy change I made in my final implementation was to add some ADAS (as I like to call it) to the mix. The trajectories and cost functions worked great, but there was a problem that came up on the rare occasion that a car ended up too close and (I'm oversimplifying here, for sure) sort of occupied that space between the current position and the end of the previous path. I added flags for `car_just_ahead`, `car_to_left`, and `car_to_right` to override the planner and either automatically slow down or prevent a lane change as an available state.

Bingo! It was weaving in and out of traffic just like those assholes you encounter on a daily basis. You know the type.

I let it rip and came back a few hours later to this: 

![22 miles](https://github.com/jeremy-shannon/jeremy-shannon.github.io/blob/master/images/path_planning/screenshot.png?raw=true)

Twenty-two miles? I'd say it's working well enough to pass.

Oh, one more thing. You didn't think I was going to let you go without subjecting you to some incredibly stupid video, did you? This one is the stupidest yet... I couldn't be more proud.

<a href="https://www.youtube.com/watch?v=cIMZvQppt38"><img src="https://github.com/jeremy-shannon/jeremy-shannon.github.io/blob/master/images/path_planning/pp_youtube.png?raw=true"></a>

*The code for this project, as well as a short but more technical write-up, can be found on [my GitHub](https://github.com/jeremy-shannon/CarND-Path-Planning-Project).*