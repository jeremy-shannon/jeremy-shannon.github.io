---
layout: post
title:  "FBF: That Time Uncle Claude Saved my Bacon"
date:   2017-03-10 21:00:00 
categories: FBF, Shannon, sampling, aliasing
---

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

*In my Flashback Friday series I'm going to reach deep into my memory (what's left of it) for some wins. Who knows what I'll find in there?!*

![Claude Shannon](xxxxxxxxxx)

I like to call him Uncle Claude, but as far as I know we're not related. Too bad - [Claude Shannon](https://en.wikipedia.org/wiki/Claude_Shannon) was undisputably a badass. And now that I've gone and read just *half* of that Wikipedia article, I can say that even more confidently. He shot the shit Alan Turing, for god's sake! More importantly for the purposes of this blog post, he was "the father of information theory" and co-(co-co-co-co-)claimant of the [Nyquist-Shannon sampling theorem](https://en.wikipedia.org/wiki/Nyquist%E2%80%93Shannon_sampling_theorem).

This story takes place back in the early-to-mid aughts, when I was still feeling my way around being an electronics engineer working in automated testing. That means: plug a piece of electronics up to a (woefully antiquated) test station and fire up the program for that particular box. It'll poke it with five volts here, twenty there, maybe some three-phase 240 volts, and then make sure it reacts the way it's supposed to. My job was to devise and implement necessary changes to the test program, which in this particular instance I had already done. There was another test that kept failing, though - not *always*, but definitely *most* of the time. It wasn't one of my requirements, and while failing random tests wasn't unheard of given the condition of the equipment, I knew there was something up.

I hooked up my oscilloscope and checked it out, it was an 400Hz sine wave signal [amplitude modulated](https://en.wikipedia.org/wiki/Amplitude_modulation) by a 0.5Hz triangle wave. 

![true signal](xxxxxxxxxx)

The problem was that the station measured the peak voltage just a *little* lower than expected, but it looked fine to me on the scope. What was going on here? I banged my head on it for a few days. I looked up the history of problems with this test. This wasn't the first time anyone had encountered it - *twice* before engineers investigated it, only to have the problem magically fix itself (i.e. they gave up). 

Then I had a breakthrough. Call it tenacity if you want, but I freely admit it was luck. I had the signal on my scope, with the peak voltage displayed correctly. Then I just happened to dial the "SEC/DIV" knob (which changes the time scale and squishes/expands the signal horizontally) to a point where several periods of the signal were in view... **and the peak voltage dipped!** Aliasing!

Digging into the station documentation, I found that any measurement was based upon 1024 samples. Always. It would try to infer an appropriate sample width (or timeframe) to capture a representative signal from which to calculate measurements, but you could also specify the sample width manually. In the case of this test, the sample width was set to five seconds. This equates to a sampling rate of 204.8 Hz. That's not going to faithfully capture the 400Hz sine wave according to Uncle Claude! See how the signal constructed based on that sampling rate is aliased to hell and back:

![5-second sample width](xxxxxxxxxx)

I changed the sample width to two seconds (a sampling rate of 512 Hz) and see how much more faithfully it captures the signal:

![2-second sample width](xxxxxxxxxx)
