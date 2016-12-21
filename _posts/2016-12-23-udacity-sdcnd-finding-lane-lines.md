---
layout: post
title:  "Udacity Self-Driving Car Nanodegree Project 1 - Finding Lane Lines"
date:   2016-12-23 21:00:00 
categories: udacity, self-driving car, nanodegree, project
---

Here it is! My first post all about the Udacity Self-Driving Car Nanodegree program, and believe me - it's fantastic. I mean really, really amazing. Udacity is making nanodegrees great again. Bigly.

Seriously, though. That's no exaggeration. This is the best online course (or, should I say, collection of courses) I've taken so far. Yes, even better than Fire Safety Refresher Training. Really! The quality is top-notch (both video and written/supplemental material), the feedback is amazing, and the community they've built around it is incredibly helpful. (I wish that during my undergrad days I'd had an online forum I could go to and find that dozens of other students were having the same problem I was having.) It's so easy to become completely immersed in the subject material, and I'm so thankful that this program exists. Udacity has really outdone themselves and I can't possibly heap enough praise on them.

The program begins with a quick introduction, including a touching story from Udacity founder and "father of the self-driving car" Sebastian Thrun, as well as the Nova special "The Great Robot Race" which reminds us how dorky we all looked a short ten years ago. It all really hammers home how important this work is and how massive the impact will be.

The first project begins immediately afterward, wasting no time getting students' feet wet: reacclimating us to the learning process, and familiarizing us with the tools and project submission process. Udacity says, "In this first lesson, you'll get taste of some basic computer vision techniques to find lane markings on the road. We will be diving much deeper into computer vision in later lessons, so just relax and have some fun in this first week!" 

The lessons quickly get you from a raw dash cam image to one with a collection of lines overlaid on the right and left edges of the lane ahead, even if the lane markings are broken! I had just happened to learn about these techniques the previous week in the several lessons I had watched in the Udacity Intro to Computer Vision course, luckily enough. It's fairly easy to understand, though. The steps were:

1. Convert RGB to grayscale
2. Apply a slight Gaussian blur
3. Perform Canny edge detection
4. Define a region of interest and mask away the undesired portions of the image
5. Retrieve Hough lines 
6. Apply lines to the original image

All of this uses the OpenCV computer vision and image processing library, which makes the process incredibly simple. The only difficulty is in fiddling with the parameters of each function to produce the desired output. The Gaussian blur takes a kernel size - the bigger the blurrier. The Canny edge takes a high and low threshold - which determine a minimum difference in intensity to establish an edge and to form a contiguous extension of an established edge, respectively. The Hough transform takes a resolution for line position and orientation, a minimum number of points to establish a line, the minimum length of a line, and the maximum gap between points allowed for a line. Of course, tuning the Hough parameters proved to be the most time consuming since it has by far the most parameters.

This pipeline worked well enough, and it was possible to get lines (typically a small collection of lines) running along both the left and right edges of the lane. The next step for the project was to consolidate these collections of lines into a single line for each side of the lane, and to extrapolate that line to the bottom edge of the image and to a point of our choosing near the center of the image. This effectively kept the lines at a fairly constant length, and precluded having gaps between the first broken line and the bottom of the image.

At this point, the pipeline is applied to two videos and if it performs well enough the project can be considered complete, but Udacity tossed in a bonus challenge which, of course, I couldn't resist. The final video includes a more curvy patch of road, areas of shadows being cast onto the lane and other bits of discoloration, and (grrrr!) a bridge that is considerably lighter-colored than the rest of the road surface.

The bridge was especially difficult because there wasn't enough contrast between the solid yellow line on the left and the road surface to trigger a Canny edge using the pipeline as is. It's possible that fiddling with the existing parameters might have solved the problem, but someone in the nanodegree forum suggested converting to HSV (hue, saturation, value) colorspace to boost the yellow areas of the image and I decided to try it out. In the end my pipeline looked like this:

1. Convert RGB to grayscale
2. Darken the grayscale (to reduce contrast in discolored sections of road)
3. Convert RGB to HSV
4. Isolate yellow in HSV to produce a yellow mask
5. Also isolate white in HSV to produce a white mask
6. Combine yellow and white masks with bitwise OR
7. Apply combined mask to darkened grayscale with bitwise OR
8. Apply a slight Gaussian blur
9. Perform Canny edge detection
10. Define a region of interest and mask away the undesired portions of the image
11. Retrieve Hough lines 
12. Consolidate and extrapolate lines and apply them to the original image

And here's a video that demonstrates it:

<a href="http://www.youtube.com/watch?feature=player_embedded&v=xknesDIgOcA" target="_blank"><img src="http://img.youtube.com/vi/xknesDIgOcA/0.jpg" alt="Udacity Self-Driving Car Nanodegree project 1 - Finding Lane Lines" width="240" height="180" border="10" /></a>

It'll be a few more weeks until the next project is due, but I'm sure I'll have plenty to share in the intervening weeks.
