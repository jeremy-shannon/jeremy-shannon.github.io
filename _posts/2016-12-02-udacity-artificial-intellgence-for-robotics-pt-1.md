---
layout: post
title:  "Udacity Artificial Intelligence for Robotics, part 1"
date:   2016-12-02 21:00:00 
categories: udacity, artificial intelligence, robotics
---

Once I had completed the Udacity Intro to Machine Learning course, ahead of the Self-Driving Car Engineer Nanodegree program application deadline, I did't waste any time moving on the next course that I imagined would help prepare me: Artificial Intelligence for Robotics. My suspicions were quickly confirmed - the first lecture video includes the note "Welcome to Artificial Intelligence for Robotics, also called 'Programming a Robotic Car'!" and begins with **the man**, Sebastian Thrun himself, discussing his work in the DARPA Grand Challenge. Bingo.

The course began with an overview of localization and included three flavors: discrete histogram filters, Kalman filters, and particle filters. The idea of localization is that the robot is trying to figure out where it is in some known environment. All three methods have these two high-level algorithm steps in common: 1. measure and 2. update belief. Each also takes into account uncertainty in both measurement and motion.

The histogram filter breaks the environment into a certain number of discrete areas - I'll call them "bins". Most of the examples in the lessions were in one dimension, but later added a second. Each bin is given a starting probability, usually a uniform distribution indicating that the robot has no idea *where* the hell it is. From there the measurements a robot takes, in addition to its motion, update its belief probabilities (the probability associated with each bin). 

The Kalman filter is a bit more sophistocated in that it operates in continuous environments and can predict future states based on the robot's motion model like magic. Really, there might be some legit witchcraft going on here, but they claim it's all just linear algebra (I'm onto you, mathematicians!). I recall there being entire graduate-level courses in the School of Electrical and Computer Engineering dedicated to Kalman filters. I never took one, unfortunately. There are several matrices to populate - state transition, control-input, observations, process noise, uncertainty, etc. A few iterations of predict-and-correct involving a good bit of prescribed matrix math, and **bam!** You have a pretty accurate prediction of your location. 

The particle filter also operates in continuous environments, but it's a bit more of a shotgun, guess-and-check localization method. You basically take a massive number of random guesses at where you are and where you're heading (copies of your robot), then take a measurement and "resample", which means that bad guesses drop out and good guesses are duplicated (and better guesses are duplicated even more). This move-measure-resample sequence is repeated until the guesses converge and you're left with a bunch of copies of the absolute best guess. 

I'll wrap up the rest of this course in the next post. Until then!
