---
layout: post
title:  "Udacity Artificial Intelligence for Robotics, part 2"
date:   2016-12-09 21:00:00 
categories: udacity, artificial intelligence, robotics
---

Last time I covered the first half or so of the Udacity Artificial Intellgence for Robotics course, which focused pretty much exclusively on localization. This time I'm going to go into the remaining topics, including Search (which I would prefer to call "path planning"), PID Control, and Simultaneous Localization and Mapping, or SLAM. 

The unit on search went over steps to devise a plan to navigate a robot from one point on a map to another - through some sort of maze, for example. The lesson culminated in two widely-used search algorithms: A* and dynamic programming. A* is something I'd come across before when learning about video game programming and is pretty much how all those shitty AI monsters seem to find their way to you instead of eternally banging their heads against walls (although, I think we've probably all played a game or two where a baddie can't find its way around a wall, right?). It simplifies a brute force, exhaustive, beginning-to-end path iteration by combining it with a heuristic, end-to-beginning "cost" to reach the goal for each possible position. The algorithm iteratively finds the next cheapest step in terms of the steps already taken and the heuristic cost of the next step. Dynamic programming is similar, but assigns an optimal policy to each possible position (and orientation, if it applies). It allows the path to be planned from any point in the environment given the same goal position.

My favorite video from the entire course was included in this unit: [A* in Action](https://www.youtube.com/watch?v=qXZt-B7iUyw) - that car is finding its way through a maze it's never even seen before!

The next topic was PID control. This unit took me back to Control Theory class back in my undergrad days. I probably best recall being blown away by the [analogs between control devices in electrical and mechanical applications](http://lpsa.swarthmore.edu/Analogs/ElectricalMechanicalAnalogs.html) - resistors, capacitors, and inductors behave analogously to dashpots (dampers), springs, and masses. And the principles apply to programming robotics, using proportional, integral, and differential (PID) controls to apply motion directly, counteract bias, and dampen ringing respectively. Fun stuff.

Finally... SLAM. It turned out to be a bit more matrix magic, like Kalman filters. Honestly, this unit felt a bit oversimplified and it was hard to imagine how it would work in a real-world application, and I hope to learn a little more about it in the Self-Driving Car Nanodegree program. The Graph SLAM algorithm is a method for correcting noisy localization estimates (obtained, say, based on motion commands) with distance measurements to certain landmarks. It incorporates several iterations of motion and sensing, combining movements, measurements, and their uncertainties into matrices *omega* and *xi*. Then the estimated position *mu* is calculated simply by multiplying the inverse of *omega* and *xi*. 

You can find my code for the exercises and projects in this course [here](https://github.com/jeremy-shannon/udacity-AI-for-robotics)

Next time I'll share my final project for this course: Runaway Robot! Stay tuned!
