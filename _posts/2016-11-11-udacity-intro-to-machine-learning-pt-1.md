---
layout: post
title:  "Udacity Intro to Machine Learning, part 1"
date:   2016-11-11 21:00:00 
categories: udacity, machine learning
---

I decided to take Udacity's Intro to Machine Learning course because it helped me to check two of the boxes I needed for the self-driving car nanodegree program application (machine learning and Python - which is the language the course exercises use). Honestly, I wasn't sure what to expect. I had heard the term before, but I still didn't know what exactly machine learning *is*.

Well, turns out: machine learning is pretty damn cool. The Udacity course is easy to follow, really engaging, and downright fun. It's still my favorite Udacity course so far (of the four I've finished, to this point). I had even unknowingly employed a sort of dumb, quasi-, proto- machine learning of my own once before. 

Ok, so, what is it? Machine learning is the subfield of computer science that "gives computers the ability to learn without being explicitly programmed." (Arthur Samuel, 1959 - from wikipedia) How can that be possible? Well, with data. Lots of data. The more data the better. A machine learning algorithm can take the mountains of data and create a model that allows it generalize to new situations it hasn't encountered before. 

In the introductory demonstration, instructor Katie Malone hands co-instructor Sebastian Thrun a variety of toy animals and tells him whether or not each animal belongs to a particular group (acerous versus non-acerous) without telling him what the term means. In the end Sebastian has two groups of toy animals. Katie then hands him another animal and tells him to determine which group it belongs to. He gets it wrong (acerous = *not* having horns), but they're both pretty confident that with enough data he probably could have figured it out.

The **features** of the animals were the inputs to Sebastian's mental algorithm - size, number of legs, tail length, color, etc. - and the group each animal belongs to (acerous/non-acerous - the output of the algorithm) were the **labels**. Given the features of a new, unlabeled animal, Sebastian should be able to determine its label (with a certain amount of confidence). In this example having horns or antlers was the only feature that had any actual bearing on the classification, but a more typical machine learning model might apply a combination of features in different amounts to arrive at a formula to classify new inputs.

You can find my code for the exercises and projects in this course [here](https://github.com/jeremy-shannon/Intro-to-Machine-Learning-Udacity)

(to be continued...)
