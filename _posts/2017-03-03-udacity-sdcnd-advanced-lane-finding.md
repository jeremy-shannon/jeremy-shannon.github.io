---
layout: post
title:  "Udacity Self-Driving Car Nanodegree Project 4 - Advanced Lane-Finding"
date:   2017-03-03 21:00:00 
categories: udacity, self-driving car, nanodegree, project, advanced lane-finding, computer vision
---

*Welcome to the mom version (Hi mom!); if jargon and mumbo jumbo is more your style then [by all means](https://github.com/jeremy-shannon/CarND-Advanced-Lane-Lines), otherwise enjoy!*

[//]: # (Image References)
[im01]: https://github.com/jeremy-shannon/CarND-Advanced-Lane-Lines/blob/master/output_images/01-calibration.png?raw=true "Chessboard Calibration"
[im02]: https://github.com/jeremy-shannon/CarND-Advanced-Lane-Lines/blob/master/output_images/02-undistort_chessboard.png?raw=true "Undistorted Chessboard"
[im03]: https://github.com/jeremy-shannon/CarND-Advanced-Lane-Lines/blob/master/output_images/03-undistort.png?raw=true "Undistorted Dashcam Image"
[im04]: https://github.com/jeremy-shannon/CarND-Advanced-Lane-Lines/blob/master/output_images/04-unwarp.png?raw=true "Perspective Transform"
[im05]: https://github.com/jeremy-shannon/CarND-Advanced-Lane-Lines/blob/master/output_images/05-colorspace_exploration.png?raw=true "Colorspace Exploration"
[im06]: https://github.com/jeremy-shannon/CarND-Advanced-Lane-Lines/blob/master/output_images/09-sobel_magnitude_and_direction.png?raw=true "Sobel Magnitude & Direction"
[im07]: https://github.com/jeremy-shannon/CarND-Advanced-Lane-Lines/blob/master/output_images/11-hls_l_channel.png?raw=true "HLS L-Channel"
[im08]: https://github.com/jeremy-shannon/CarND-Advanced-Lane-Lines/blob/master/output_images/12-lab_b_channel.png?raw=true "LAB B-Channel"
[im09]: https://github.com/jeremy-shannon/CarND-Advanced-Lane-Lines/blob/master/output_images/13-pipeline_all_test_images.png?raw=true "Processing Pipeline for All Test Images"
[im10]: https://github.com/jeremy-shannon/CarND-Advanced-Lane-Lines/blob/master/output_images/14-sliding_window_polyfit.png?raw=true "Sliding Window Polyfit"
[im11]: https://github.com/jeremy-shannon/CarND-Advanced-Lane-Lines/blob/master/output_images/15-sliding_window_histogram.png?raw=true "Sliding Window Histogram"
[im12]: https://github.com/jeremy-shannon/CarND-Advanced-Lane-Lines/blob/master/output_images/16-polyfit_from_previous_fit.png?raw=true "Polyfit Using Previous Fit"
[im13]: https://github.com/jeremy-shannon/CarND-Advanced-Lane-Lines/blob/master/output_images/17-draw_lane.png?raw=true "Lane Drawn onto Original Image"
[im14]: https://github.com/jeremy-shannon/CarND-Advanced-Lane-Lines/blob/master/output_images/18-draw_data.png?raw=true "Data Drawn onto Original Image"

Project number four for Term 1 of the Udacity Self-Driving Car Engineer Nanodegree built upon [the first project](http://jeremyshannon.com/2016/12/23/udacity-sdcnd-finding-lane-lines.html), more so than the [second](http://jeremyshannon.com/2017/01/13/udacity-sdcnd-traffic-sign-classifier.html) and [third](http://jeremyshannon.com/2017/02/10/udacity-sdcnd-behavioral-cloning.html) projects. While that might seem obvious because they both involve finding lane lines, the reason for this *under the hood* (har har) is that while projects two and three introduced us to the hot-ass newness of deep learning to damn near write our code for us, projects one and four rely on more traditional computer vision techniques to get very explicit about how we go from input to output. It's almost a let down - like trading a keyboard in for a pencil - but *people are saying* (do I sound presedential?) that companies still rely on these techniques, so it's definitely worth learning (and still fun and challenging) and the OpenCV library is the one doing all the heavy lifting anyway.

"So let's grab a dashcam find some lanes!" you're saying. Well, hold on just a second, Tex. You can't just start finding lanes all willy-nilly. For starters, that camera you're using? It distorts the images. You probably couldn't even tell, but it's true! Look:

![alt text][im02]

Thankfully this can be corrected (for an individual camera/lens) with a handful of photos of chessboards and the OpenCV functions `findChessboardCorners` and `calibrateCamera`. Check it out:

![alt text][im03]

I know - it looks almost the same to me too, but the distortion is most noticeable at the corners of the image (check out the difference in the shape of the car hood at the bottom). 

*Now* we can get to the fun stuff. The next step was to apply a perspective transform to get something of a birds-eye view of the lane ahead. Here's what it looks like:

![alt text][im04]

I probably went to greater lengths than necessary to get my perspective transform *juuuust right* (making straight lines perfectly vertical in the resulting birds-eye view), but since the transform is reversed according to the same rules it probably didn't matter much in the end. 

Next, I explored a few different color transforms and gradient thresholds to try to isolate the lane lines and produce a binary image with 1s (white) where a lane line exists and 0s (black) everywhere else. This was easily the most delicate part of the process, and very sensitive to lighting conditions and discolorations (not to mention those damn white cars!) on the road. I won't bore you with the details; suffice it to say this is where I spent most of my time on this project. In the end I combined a threshold on the B channel of the [Lab colorspace](https://en.wikipedia.org/wiki/Lab_color_space) to extract yellow lines and the L channel of the [HLS colorspace](https://en.wikipedia.org/wiki/HSL_and_HSV) to extract the whites. Here's what each of those looks like:

![alt text][im08]

![alt text][im07]

And here they are combined on several test images:

![alt text][im09]

Not too shabby!

Now, the clever bit: it would be unnecessary (and computationally expensive) to search the whole image to identify which pixels belong to the left and right lanes, so instead we computed a histogram of the bottom half of the binary image, like so:

![alt text][im11]

The peaks on the left and right halves give us a good estimate of where the lane lines start, so we can just search small windows starting from the bottom and essentially following the lane lines all the way to the top until all the pixels in each line are identified. Then a polynomial curve can be applied to the identified pixels and voilà!

![alt text][im10]

And not just that, but we can even more easily find pixels on consecutive frames of a video using the fit from a previous frame and searching nearby, like so:

![alt text][im12]

It's just a matter of coloring in the polynomial lines and a polygon to fill the lane between them, applying the inverse perspective transform, and drawing the result back onto the original image. We also did a few simple calculations and conversions to determine the road's radius of curvature and the car's distance from the center of the lane. Here's what the final result looks like:

![alt text][im14]

This is the pipeline that I applied to the video below, with a bit of smoothing (integrating information from the past few previous frames) and sanity checks to reject ouliers (such as disregarding fits that aren't within a certain distance apart).

Here's a [link to my video result](https://github.com/jeremy-shannon/CarND-Advanced-Lane-Lines/blob/master/project_video_output.mp4), and here's a [bonus video with some additional diagnostic information](https://github.com/jeremy-shannon/CarND-Advanced-Lane-Lines/blob/master/challenge_video_output_diag.mp4).

*Again, if it's the technical stuff you're into, [go here](https://github.com/jeremy-shannon/CarND-Advanced-Lane-Lines).*

