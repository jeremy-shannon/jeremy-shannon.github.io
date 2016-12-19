---
layout: post
title:  "Udacity Artificial Intelligence for Robotics, part 3"
date:   2016-12-16 21:00:00 
categories: udacity, artificial intelligence, robotics
---

This week I actually started the Self-Driving Car Nanodegree program (!!!), but I'm not quite ready to share anything I've learned just yet. Suffice it to say, so far it's ***awesome***! And thankfully the program begins with a quick bite to whet your appetite, a bit of an *amuse bouche* of a project: Finding Lane Lines, which I'll be able to share next week. For now, I'll wrap up my experience with the Artificial Intelligence for Robotics course - the final project: 

###Runaway Robot!

The premise behind the project is this:

> A robotics company named Trax has created a line of small self-driving robots designed to autonomously traverse desert environments in search of undiscovered water deposits.

> A Traxbot looks like a small tank. Each one is about half a meter long and drives on two continuous metal tracks. In order to maneuver itself, a Traxbot can do one of two things: it can drive in a straight line or it can turn. So to make a  right turn, A Traxbot will drive forward, stop, turn 90 degrees, then continue driving straight.

> This series of questions involves the recovery of a rogue Traxbot. This bot has gotten lost somewhere in the desert and is now stuck driving in an almost-circle: it has been repeatedly driving forward by some step size, stopping, turning a certain amount, and repeating this process... Luckily, the Traxbot is still sending all of its sensor data back to headquarters.

> In this project, we will start with a simple version of this problem and gradually add complexity. By the end, you will have a fully articulated plan for recovering the lost Traxbot.

The first part of the problem was to locate the Traxbot given a series of (I'll call them) GPS readings it sends back. We've established that the robot is moving in a circle, so with each reading there is a distance and change in heading angle, both of which remain constant, from the previous reading. All it really takes is three readings to establish what these values are and predict the fourth position. Piece of cake.

Then the problem was changed so that the readings being sent back had a certain amount of noise added to them. The home base only has these noisy readings to make predictions from, and the goal is to predict (within 1% tolerance) the actual position of the Traxbot. Not so easy this time, huh?!

This, to me, was the crux of the project, and it seemed ripe for a Kalman Filter. The example from the course lecture was built from a linear motion model, and the circular motion was definitely not linear. My first inclination was to convert to a polar coordinate system, for which circular motion would actually be a linear relationship between angular velocity and angular distance. I think it might have worked out, if the circle had been centered at the origin (or maybe not). But with the extra unknown center point (x0, y0) the Kalman Filter didn't converge. You can see a couple of attempts with polar coordinates (orange, yellow, gray), an attempt with cartesian coordinates (dark blue), and the actual Traxbot position (light blue) in the image below.

![Kalman Filter in polar coordinates](https://cdn-enterprise.discourse.org/udacity/uploads/default/original/3X/3/d/3d682e71f7cb352c604866953eca1ef9f6b42480.PNG)

Searching through the forums I came across others who had used insanely high degree motion models (position, velocity, acceleration, jerk, uhhh... I don't know what comes after jerk, but this person had accounted for it), which didn't work for me. I Googled around and found other solutions that claimed to work but didn't when I tried them out. It was becoming apparent that the Kalman Filter wasn't going to work, and that I'd need to learn the Extended Kalman Filter. 

So I did that.

And I found another person who had used the EKF, but with (I take it) the wrong motion model. I suppose maybe the bicycle motion model we learned in the lectures and the simpler Traxbot motion model are similar enough that they can both localize. And the EKF didn't turn out to be too difficult. It's basically the Kalman Filter with a few partial derivatives in the place of scalar coefficients (to grossly oversimplify it). The EKF localized pretty well!

The next two parts involved chasing down the Traxbot, first with a robot that can move faster than the Traxbot, then with one that moves slower. I found this part to be a bit easier than the localization. My algorithm basically extrapolated the Traxbot speed and turning angle to find the spot where my robot could intercept it and head there (with adjustments along the way). Here's a video of my final chase-bot (with a demonstration of a first-pass miss, which is probably bound to happen from time to time with the noise - but typically the chase-bot catches the Traxbot on the first pass)

<a href="http://www.youtube.com/watch?feature=player_embedded&v=8vvtMJwlV18" target="_blank"><img src="http://img.youtube.com/vi/8vvtMJwlV18/0.jpg" alt="Runaway Robot on YouTube" width="240" height="180" border="10" /></a>

The final part involved massive amounts of noise coming back from the Traxbot GPS readings, and my EKF failed miserably. I felt I had gotten what I wanted out of the course at this point, so I called it a day.

You can find my code for the exercises and projects in this course [here](https://github.com/jeremy-shannon/udacity-AI-for-robotics)

In the interim, after completing this course I also took the (short) Linear Algebra Refresher, (shorter) Deep Learning, and began the (looooong) Intro to Computer Vision courses from Udacity. It was good to get a little more practice with Python, an intro to Tensorflow, and a head start on some of the topics covered in the Self-Driving Car curriculum, but I'll save discussion on these topics for when they're covered in the nanodegree program. 

Until next time!
