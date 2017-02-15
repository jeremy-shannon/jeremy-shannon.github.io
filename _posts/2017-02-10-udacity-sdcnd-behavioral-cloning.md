---
layout: post
title:  "Udacity Self-Driving Car Nanodegree Project 3 - Behavioral Cloning"
date:   2017-02-10 21:00:00 
categories: udacity, self-driving car, nanodegree, project, behavioral cloning, deep learning
---

![Confused Car](https://github.com/jeremy-shannon/jeremy-shannon.github.io/blob/master/images/behavioralCloning.PNG?raw=true)

*This is a friendlier depiction of my experience; if you'd like to get technical go [here](https://github.com/jeremy-shannon/CarND-Behavioral-Cloning-Project)*

Teaching a car to drive - sounds easy, right? I mean, it couldn't be any tougher than teaching a teenager (as long as she's been paying attention). And really, that's what it comes down to: as long as you've shown the car what it needs to learn, it can learn. Incredible!

## Introduction

The object of this project was to apply deep learning principles to effectively teach a car to drive autonomously in a simulator. The simulator includes both training and autonomous modes, and two tracks - I'll refer to these as the "test track" (i.e. easy mode) and the "challenge track" (i.e. hard mode). In training mode, you put your gaming skills to the test driving the car around the test track (like a normal person, dammit!) and recording it. You then use the captured data to train a [convolutional neural network (CNN)](http://www.wildml.com/2015/11/understanding-convolutional-neural-networks-for-nlp/), which produces a model - the "rules of the road" for the car to drive itself in autonomous mode. The challenge of this project was getting the model to generalize well enough to drive itself on the test track *and* a track it's never seen (i.e. the challenge track). 

## Approach

Thankfully, we didn't have to start from scratch - Udacity suggested using a working CNN and provided a link to the [nVidia model](https://images.nvidia.com/content/tegra/automotive/images/2016/solutions/pdf/end-to-end-dl-using-px.pdf).

<img src="https://github.com/jeremy-shannon/CarND-Behavioral-Cloning-Project/raw/master/images/nVidia_model.png?raw=true" width="400px">

Udacity provided a dataset that can be used alone to produce a working model. However, students were encouraged (and let's admit, it's more fun) to collect our own. Particularly, Udacity encouraged including "recovery" data while training. This means: let approach the edge of the track, then **quick! hit "record" and steer the car back toward the center!** This was a bit tricky, but it gave the model a chance to learn recovery behavior. It's easy enough for experienced humans to drive the car reliably around the track, but if the model has never experienced being too close to the edge and then finds itself in just that situation it won't know how to react.

The captured training images don't fit right into the CNN, so some preprocessing was required (I included cropping, resizing, blur, and a change of color space). Then I introduced some "jitter" (random brightness adjustments, artificial shadows, and horizon shifts) to sort of keep the model on its toes, so to speak. This helped it to generalize to the challenge track. Here's a sample of the data that was fed to the CNN for training:

<img src="https://github.com/jeremy-shannon/CarND-Behavioral-Cloning-Project/raw/master/images/sanity-check-take-4.gif?raw=true">

Because the test track includes long sections with very slight or no curvature, the data captured from it tended to be heavily skewed toward low and zero turning angles. This created a problem for the neural network, which then became biased toward driving in a straight line and was easily confused by sharp turns. Here's the original distribution of the training data (the x-axis corresponds to steering angles and the y-axis is the data point count for that angle range; the black line represents what would be a uniform distribution):

<img src="https://github.com/jeremy-shannon/CarND-Behavioral-Cloning-Project/raw/master/images/data_distribution_before_3.png?raw=true" width="400px">

I dropped a bunch of those data points in the middle, and the result looked like this:

<img src="https://github.com/jeremy-shannon/CarND-Behavioral-Cloning-Project/raw/master/images/data_distribution_after.png?raw=true" width="400px">

At this point, the model performed very well - driving reliably around the test track multiple times. It also drove the challenge track quite well, until it encountered an especially sharp turn. I tried a few things to help it out:

1. More aggressive cropping (inspired by [David Ventimiglia's post](http://davidaventimiglia.com/carnd_behavioral_cloning_part1.html?fb_comment_id=1429370707086975_1432730663417646&comment_id=1432702413420471&reply_comment_id=1432730663417646#f2752653e047148))
2. Cleaning the dataset one image at a time (inspired by [David Brailovsky's post](https://medium.freecodecamp.com/recognizing-traffic-lights-with-deep-learning-23dae23287cc#.linb6gh1d) describing his competition-winning model for identifying traffic signals) 
3. Further model adjustments (L2 regularization, ELU activations, adjusting optimizer learning rate, etc.)
4. Model checkpoints (something of a buy-one-get-X-free each time the training process runs)

But in the end, the distribution of the data was to blame. At one point, I had decided I might be throwing out too much of my data, so I tried keeping a lot (still not nearly all) of the data I had been dropping:

<img src="https://github.com/jeremy-shannon/CarND-Behavioral-Cloning-Project/raw/master/images/data_distribution_after_3.png?raw=true" width="400px">

This made the car drive *badly* on the challenge track. 

OK, so what happens if I swing that pendulum the other direction?

<img src="https://github.com/jeremy-shannon/CarND-Behavioral-Cloning-Project/raw/master/images/data_distribution_after_4.png?raw=true" width="400px">

*Bingo.*

## Results 

See for yourself.

[![Self-Driving!](https://img.youtube.com/vi/oiOOqJdW9Y4/0.jpg)](https://www.youtube.com/watch?v=oiOOqJdW9Y4)

Here's the final CNN architecture:

<img src="https://github.com/jeremy-shannon/CarND-Behavioral-Cloning-Project/raw/master/images/model_diagram.jpeg?raw=true" width="400px">

## Conclusion and Discussion

This project - along with most every other exercise in machine learning, it would seem - very much reiterated that it really is *all about the data*. Making changes to the model didn't have the impact that changing the fundamental makeup of the training data had. 

I could pretty easily spend hours upon hours tuning the data and model to perform optimally on both tracks, and I fully plan to revisit this project when time permits. One thing I would like to improve is my distribution flattening scheme. As it is, a very large chunk of data is thrown out, never to be seen again. I find this bothersome, and I feel that wasting data like this (even if it is mostly zero/near-zero steering angles) is a missed opportunity to train a model that can better generalize. I'd also like to revisit more aggressive cropping and shrinking the neural net. Another nanodegree student achieved good model performance in a neural net with only 52 parameters. Such a small neural net is desirable because it greatly reduces training time and can produce near real-time predictions, which is very important for a real-world self-driving car application.

I enjoyed this project thoroughly and I'm very pleased with the results. Training the car to drive itself, with relatively little effort and virtually no explicit instruction, was extremely rewarding.


*Again, for the technical version go [here](https://github.com/jeremy-shannon/CarND-Behavioral-Cloning-Project)*
