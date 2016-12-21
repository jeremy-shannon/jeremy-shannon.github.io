---
layout: post
title:  "Udacity Intro to Machine Learning, part 2"
date:   2016-11-18 21:00:00 
categories: udacity, machine learning
---

Machine learning algorithms can be broadly classified as either "supervised" or "unsupervised." The difference between the two is based simply upon whether or not the data has labels, and unsupervised algorithms basically serve to cluster data points (e.g. "You liked movie X so might I suggest movie Y? I've determined them to be quite similar."). The example from my previous post with the horny animals would be considered a supervised "classification" algorithm. Supervised algorithms can be considered either classification or "regression", depending on whether the labels are discrete or continuous. The animals were either acerous or non-acerous. Another supervised classification algorithm might determine whether a puppy is cute, ugly, or neutral, or the grade level at which a child makes snarky comments on Twitter - anything that categorizes inputs into a finite number of buckets, and all of the new data points will be placed into one of those buckets. 

Supervised regression algorithms have numeric labels that fit on a continuous scale. The classic example is a regression algorithm that determines the price of a home based upon inputs like square footage, number of rooms, location, location, and location. The algorithm attempts to fit a line or curve to the data upon which new data points can be interpolated (or extrapolated). The accidental, primitive machine learning algorithm I mentioned in my previous post involved Quest bars - super healthy (maybe?) protein bars with tons of fiber. Their deliciousness varies. I got a variety pack and decided to conduct a little experiment. I recorded some pertinent (in my mind) pieces of nutrition information and then gave each flavor a rating. Hardly rigorously scientific, but it was a fun exercise. Once I had compiled data for several flavors I ran the MS Excel CORREL function for each piece of nutrition data against my ratings. Apparently I'm a fan of calories, fat, protein, and (less so) sugar. But fiber and (especially) erythritol pretty much make me wanna puke. Who knew?! I was then able to use these insights to determine whether or not I would like flavors I hadn't tried before. Neat!

![Quest bar comparison chart](/images/questBars.png "Quest bar comparisons")

Anyway, once you have a mountain of data (preferably labeled) you choose an algorithm. For the course, SciKit-Learn is the machine learning library of choice. Probably the most difficult step in the entire process (throughout the length of the course) was just getting the library installed. SK-Learn's online documentation is fantastic, and implementing most of the algorithms was a breeze. Anyway, import the library for your algorithm of choice and train a model on the data. It's important to set aside some of your labeled data to test the model to determine how well it performs. There's a balance to be struck when fitting a model to the training data - a model that fits more accuarately to the training data may not generalize to the test data (and, later, to any new data). 

The course also goes into further detail on topics like feature scaling, text learning, feature selection, principle component analysis, validation, and evaluation metrics. I might touch on those topics in a future blog post, but for now I'm moving on. To sum it up, I liken traditional artificial intelligence to teaching a computer to, say, play a game by giving it an instruction manual. Meanwhile, machine learning would be more like teaching the computer how to play by simply playing and having the computer observe.

Instructor Katie Malone has an excellent podcast on the topic of machine learning and data science called [Linear Digressions](http://lineardigressions.com/). Anyone annoyed with mansplaining will find it refreshing, since Katie perpetually schools cohost Ben Jaffe in episode after episode, topic after topic. :)

You can find my code for the exercises and projects in this course [here](https://github.com/jeremy-shannon/Intro-to-Machine-Learning-Udacity)

Next time: Artificial Intelligence for Robotics!
