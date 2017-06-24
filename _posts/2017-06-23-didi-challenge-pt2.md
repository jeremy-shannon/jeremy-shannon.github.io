---
layout: post
title:  "DiDi Just Hear You Say Challenge? (Part 2)"
date:   2017-06-23 21:00:00 
categories: udacity, didi challenge, object tracking, point cloud, ROS
---

*This is part two of a (probably) two-part series reflecting on my experience in the [Udacity DiDi Challenge](https://www.udacity.com/didi-challenge)*

[Last time](http://jeremyshanon.com/2017/06/09/didi-challenge-pt1.html) I told you about my lovely, gradually won accomplishments in the first, oh, month-and-a-half working on the challenge. This time, though, is all about those frantic final days, hours really, before the close of Round 1. I knew that at any point if I hit a roadblock it was probably curtains for the ol' Transformers, but otherwise my plan was to keep my head buried in ROS for the next 72-or-so hours. I left you with this nail-biter... a real cliffhanger, for sure:

![cars and non-cars](https://github.com/jeremy-shannon/jeremy-shannon.github.io/raw/master/images/didi_pt1/car_noncar.png?raw=true)

Those are some samples of the "car/non-car" dataset that my LiDAR data processing node spat out. The plan was to build some sort of classifier to determine whether a given sample was a car and, if so, add data for that car to a tracklet (XML) file. The minimum goal was to just get on the leaderboard. A fellow teammate had already submitted some tracklets of his own and gotten a zero score, so any score whatsoever was going to be a big win for us. 

Udacity had already released some template code for generating tracklet data written in Python, and all of my experience with machine learning and deep learning was in Python, so I decided my best bet was to create another ROS node in Python to consume the sample image data coming from the LiDAR node. The problem now was that I couldn't just pass those images along by themselves - each frame coming from the LiDAR generates multiple clusters, and I wanted to transmit the X and Y pose of the cluster along with the sample image. This meant that I would have to create a custom message packaging the two data items together. Thankfully [the ROS wiki](http://wiki.ros.org/ROS/Tutorials/DefiningCustomMessages) has plenty of documentation covering it. Here's the whole of the code for my custom message (`img_with_pose.msg`):

``` 
Header header
sensor_msgs/Image img
geometry_msgs/Pose2D pose
```

That, plus some simple changes to `package.xml` and `CMakeLists.txt`, not to mention a crash course in [CV Bridge](http://wiki.ros.org/cv_bridge/Tutorials/UsingCvBridgeToConvertBetweenROSImagesAndOpenCVImages), had me up and running with my custom message. I disabled the code for visualizing the point cloud (which, dammit, means no more cool animated gifs of point clouds like last time - bummer!) and saving the samples to png files, just to keep things running at full steam. So now my LiDAR node was consuming LiDAR data and sending out flattened, top-view image samples with an X-Y pose attached. It was time to build a classifier and tracklet generator. 

I had previously done some work with image classification and deep learning in Python, so I decided to start with the tracklet code. If I couldn't get that working there wouldn't be much point in doing the classifier anyway. And I figured I could generate a tracklet that includes data for *all* of the clusters just to see if the leaderboard would accept it, then use the classifier to limit it to just cars afterwards. I almost didn't submit this "all the clusters" tracklet, figuring it would surely get a zero score. The "unlabeled" test ROSbag data was about twenty-six seconds long, and at a LiDAR frame rate of 10 Hz, that means any single object should have no more than 260 or so poses in the tracklet. Well, this tracklet had 765 poses. My teammate encouraged me to submit it, though, and good thing! It got us a (paltry, I admit) score - we were on the leaderboard! Party time!

At this point it was only a few hours from the end of Round 1 and the closing of the leaderboard. I quickly threw together a convolutional neural net based on the [LeNet architecture](http://yann.lecun.com/exdb/lenet/) (since my data sort of loosely resembled the handwritten letters in the [MNIST dataset](http://yann.lecun.com/exdb/mnist/)). The first try achieved 80% validation accuracy - good enough for now, with time running so short! I fought it a bit, but got the model loaded into my Python ROS node and generated a tracklet with eighty object poses. That seemed more reasonable than 765, if maybe a little on the low side. I submitted it, aaaaand...

Zero. *sad trombone music* 

Not just that, we were off the leaderboard! Crap! I quickly threw the "all the clusters" tracklet back together and resubmitted it to get us back on. By this time it was past midnight, less than an hour from the deadline, and I was fading. I threw in the towel, accepting a 45th place finish for Round 1. Not bad, really, considering it was out of a reported 2,000+ teams that signed up.

Looking back, I believe the problem was in my tracklet generation. I think it was front-loading the poses to the first 80 frames, when I should have been keeping track of which frames contained a detection and probably interpolating for frames between detections. Also, there were very likely several frames at the beginning and end of the bag data for which the object car wasn't in the LiDAR frame, so I would have to take that into account. I would also have to find a way to counteract false positives. I'll never be sure what score I might have achieved with the Round 1 submissions closed, but I'd like to someday adapt some of the other Udacity template code to evaluate my generated tracklets on the training data. No matter how accurate I might be able to get it, I'm going to call my time with the DiDi Challenge a "Mission Accomplished" because I did just what I had set out to do: I learned a ton about ROS, I worked with point cloud data, and I did my team kinda proud. 

*Feel free to [check out the code on GitHub](https://github.com/jeremy-shannon/ROS-examples).*

