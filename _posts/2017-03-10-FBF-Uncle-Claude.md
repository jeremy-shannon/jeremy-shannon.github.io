---
layout: post
title:  "FBF: That Time Uncle Claude Saved my Bacon"
date:   2017-03-10 21:00:00 
categories: FBF, Shannon, sampling, aliasing
---

[//]: # (Image References)
[im01]: /images/hml/ClaudeShannon.jpg "Claude Shannon"
[im02]: /images/hml/all_signals.PNG	"All Signals"
[im03]: /images/hml/all_signals_pt2s.PNG "All Signals - 0.2s Range"
[im04]: /images/hml/true_and_sampled_full.PNG	"True and Sampled Signals Together"
[im05]: /images/hml/true_and_sampled_pt2s.PNG	"True and Sampled Signals Together - 0.2s Range"
[im06]: /images/hml/true_signal_closeup.PNG "All Signals Together - 0.2s Range"
[im07]: /images/hml/true_signal_full.PNG "All Signals Together"

*In my Flashback Friday series I'm going to reach deep into my memory (what's left of it) for some wins. Who knows what I'll find in there?!*

![Alt Text][im01]

I like to call him Uncle Claude, but as far as I know we're not related. Too bad - [Claude Shannon](https://en.wikipedia.org/wiki/Claude_Shannon) was undisputably a badass (just *look* at him). And now that I've gone and read just *half* of that Wikipedia article, I can say that even more confidently. He shot the shit Alan Turing, for god's sake! More importantly for the purposes of this blog post, he was "the father of information theory" and co-(co-co-co-co-)claimant of the [Nyquist-Shannon sampling theorem](https://en.wikipedia.org/wiki/Nyquist%E2%80%93Shannon_sampling_theorem).

This story takes place back in the early-to-mid aughts, when I was still feeling my way around being an electronics engineer working in automated testing. That means: plug a piece of electronics (i.e. "box") up to a (woefully antiquated) test station and fire up the program for that particular box. It'll poke it with five volts here, twenty there, maybe some three-phase 240 volts, and then make sure it reacts the way it's supposed to. My job was to make changes to the test program as necessary to keep the production shop running. In this particular instance I had already made my changes and verified they worked. There was another test that kept failing, though - not *always*, but definitely *most* of the time. It wasn't one of my requirements, and while failing random tests wasn't unheard of given the condition of the equipment, I knew something was up.

I hooked up my oscilloscope and checked it out, it was a 400-Hz sine wave signal [amplitude modulated](https://en.wikipedia.org/wiki/Amplitude_modulation) by a 0.5-Hz triangle wave. 

![Alt Text][im07]

That's the wide-angle view; let's zoom in:

![Alt Text][im06]

The problem was that the station measured the peak voltage just a *little* lower than expected. But it looked fine to me on the scope! What was going on here? I banged my head against it for a few days. I looked up the history of problems with this test. This wasn't the first time anyone had encountered it - *twice* before engineers investigated it, only to have the problem magically fix itself (i.e. they gave up). 

Then I had a breakthrough. Call it tenacity if you want, but I freely admit it was luck. I had the signal on my scope, with the peak voltage displayed correctly. Then I just happened to dial the "SEC/DIV" knob (which changes the time scale and squishes/expands the signal horizontally) to a point where several periods of the signal were in view (you might say I zoomed *waay* out)... **and the peak voltage dipped!** I immediately knew what I was dealing with: aliasing!

Digging into the station documentation, I found the tidbit of info that confirmed my suspicions: any measurement was based upon 1024 samples. Always. It would try to infer an appropriate sample width (or timeframe) to capture a representative signal from which to calculate measurements, but you could also specify the sample width manually. In the case of this test, the sample width was set to five seconds. This equates to a sampling rate of 204.8 Hz (1024 samples / 5.0 seconds). That's not going to faithfully capture the 400-Hz sine wave according to Uncle Claude! He always told me growing up (c'mon, let me fantasize), "Jeremy, boy. You've always got to sample at *at least* twice the rate of the highest frequency of the signal you're trying to capture." See how the signal constructed based on that sampling rate is aliased to hell and back?

![Alt Text][im04]

![Alt Text][im05]

Yuck! That reconstructed signal is *not* like the original. Incidentally, this is the exact phenomenon that makes wheels or helicopter rotors seem to spin slowly, or backwards, or [not at all](https://www.youtube.com/watch?v=R-IVw8OKjvQ) in video.

I changed the sample width to two seconds (a sampling rate of 512 Hz) and see how much more faithfully it captures the signal:

![Alt Text][im02]

![Alt Text][im03]
