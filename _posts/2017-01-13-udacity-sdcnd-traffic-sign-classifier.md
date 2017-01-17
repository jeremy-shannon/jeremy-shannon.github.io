---
layout: post
title:  "Udacity Self-Driving Car Nanodegree Project 2 - Traffic Sign Classifier"
date:   2017-01-13 21:00:00 
categories: udacity, self-driving car, nanodegree, project, deep learning, classifier
---

Project number two in the can! (I realize now that that sentence might sound like toilet humor, but I swear it was unintentional.)

I'm truckin' right along in my Udacity Self-Driving Car Engineer nanodegree program, as my personal mentor is well aware from our weekly check-ins. I feel bad for the guy because I honestly haven't had much need for him. I'm glad he's there, of course! But I guess the course content keeps everything pretty crystal clear, and the help from the community at large is a big heads-up to whatever obstacles might be coming my way (one benefit of being placed into a cohort that started later than others). It's good to know that Udacity has gone to great lengths to make sure I don't get stuck.

That's not to say that this thing is a cake walk by any means! I consider myself lucky that I really, truly enjoy it - that I'm *eager* to spend all of my me-time with my laptop open training a neural network. Otherwise, I think it would be easy to fall behind. Udacity estimated that students would need to devote ten hours a week to the curriculum, and it's hard to guage since I'm currently a week or two ahead of schedule and I'm sure it depends on your skill level coming in, but I'd be inclined to bump that number up at least fifty percent. We'll just have to see how the rest of the term goes, though. For now...

## Project 2: Traffic Sign Classifier

This unit was all about *deep learning*, and there was a boatload of learning and exercise material leading up to the project. I found myself glad that I'd taken Udacity's Intro to Machine Learning and Deep Learning classes ahead of starting the nanodegree. A hefty chunk of the Deep Learning course material made an encore appearance in the nanodegree, but I can't complain - the course was short and the material was dense so it was good to take a second look at it. So what is deep learning, anyway? That the million dollar question, my friend.

The truth is, the jury is still kind of out on deep learning. Why? Well, mostly because we haven't quite nailed down *how* it works. It just kind of does. At its core is a concept called a "neural network" which is a combination of basic units called "perceptrons," each of which simply takes a number of inputs, multiplys each input by a chosen weight and adds a chosen bias, and produces an output. A perceptron with a one-dimensional input will produce a line (think mx+b from algebra class), which can be used to fit data points with continuous outputs (think "line of best fit") or divide data points with discrete outputs (i.e. classes, like "short" versus "tall" if your input were height in inches, for example). Combine enough of these perceptrons in some configuration and you can come up with some pretty complex models for predicting the output of a given input. 

But how do you figure out what those weights and biases should be? Well, you let the computer do that for you (handy little things, ain't they!), and for that you need data. A lot of data. And not just that, the data needs to be labeled with the correct output. But then, if you configure your neural net sufficiently, the computer will magically (Really! ... OK, not really.) produce weights and biases that can correctly guess the output for an input it's never seen before. Super cool!

I tried to think of an analogy, and here's the best I could come up with: Think of a guitar player's setup, with the guitar and amp and a bunch of pedals to shape the sound of the guitar. Now imagine you're trying to replicate [Annie Clark](http://ilovestvincent.com)'s sound, and you've got the guitar and the amp and all the pedals set up the same way she does, but you can't tell from your crappy low-res photos what numbers all those knobs are dialed in to. What now? Deep learning would be like taking a recording, giving your computer the inputs (chords and notes being played) and the outputs (sounds coming out of the amp), and letting *it* figure out how to dial in all of those knobs. (Be warned, this analogy is very fragile and its feelings are easily hurt.)
