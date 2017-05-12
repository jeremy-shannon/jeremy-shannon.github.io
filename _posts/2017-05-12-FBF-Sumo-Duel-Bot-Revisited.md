---
layout: post
title:  "FBF: Sumo-Duel-Bot Revisited"
date:   2017-05-12 21:00:00 
categories: FBF, Sumo Duel Bot, Electronics, Audio amplifier, Leadership
---

*In my Flashback Friday series I'm going to sift through my memory for some wins. Who knows what I'll find in there?!*

![LM386](https://upload.wikimedia.org/wikipedia/commons/e/e6/LM386-Operational_amplifier.jpg)

This week I was invited back to my alma mater to help judge team presentations for their final project in Electronics class. Teams of two or three students had to: 

1. Implement a simple audio amplifier using an [LM386](https://en.wikipedia.org/wiki/LM386) (pictured above) - the quintessential cheap (under $1.00), low-power audio amplifier IC.
2. Design and implement their own discrete (i.e. out of transistors, resistors, and maybe a few capacitors and diodes) audio amplifier and evaluate its performance.
3. Using LabView and a [National Instruments myDAQ](http://www.ni.com/en-us/shop/select/mydaq-student-data-acquisition-device), create a unique software application that integrates with the audio amplifier circuit.

They were given ten minutes to present their solutions, and I don't think a single team escaped some sort of technical difficulty that cut into their time. Even the teams that soldered their circuits onto near-production grade PCBs and designed and 3D-printed enclosures for them had issues. If my memory serves, it was the same story four years ago when I did the same assignment. Demo days, man! My team got the highest score back then, which I credit mostly to potentiometers. (It became quickly apparent that the discrete circuit design would be a delicate balancing act between maximizing output gain while avoiding distortion. The pots (dozens of them) allowed me to dial in all of the resistances *just right* to get the best performance, and whenever I smoked a transistor I could just pop in a new one and quickly tune the circuit to it.)

Anyway, I asked the professor how the robot competition went this year and he told me that *he skipped it*. "The f*ck did you just say?!" I have such mixed emotions about it. "What is it about this bunch of slackers that earns them the right to avoid the *hazing* (frankly) that I was forced to endure?!" ...but also... "These poor sonsabitches! You're *depriving* them of one of the greatest experiences of their academic careers!" That's just how I felt. I would never be so effusive; I think my actual reaction was, "Huh." 

So in light of that, I'll take this opportunity to explore one of the aspects of the [Sumo-Duel-Bot project](http://jeremyshannon.com/2016/05/20/sumo-duel-bot.html) (my very first post to this blog, I encourage you to read it now for the backstory) that I may have learned the most from: leadership. 

At the beginning of the semester, we were given a quiz to test our knowledge of [BJTs](https://en.wikipedia.org/wiki/Bipolar_junction_transistor) and [MOSFETs](https://en.wikipedia.org/wiki/MOSFET). The students that scored highest (myself among them) were made team leaders, and the remaining students were assigned to teams based mostly on who knew whom. I'm typically one to demur to others who would prefer to be in control, so it was an opportunity to add to my leadership experience. I was lucky that our first assignment was relatively simple - build the infrared beacon for the sumo-duel-bot. This experience helped me to plan for designing and building the bot itself.

My first teammate I had known from previous classes we'd taken together. He was young (well, compared to the other two old guys on the team he was) and months away from graduating. He had other things going on in his life, obviously little interest in busting his butt on our robot, and a brand new girlfriend to top it all off. I get it. I've been there a time or two in my life. But even if I didn't begrudge him for it, I knew we wouldn't be able to count on him. I suggested he be responsible the design of the [H bridge](https://en.wikipedia.org/wiki/H_bridge) - a relatively simple piece of the overall design (and meanwhile ordered some commercial H bridges for backup).

My other teammate was a fascinating guy. He was an energy drink junkie who was overloaded that semester but still gung-ho about the robot and perfectly happy to spend the night in the lab from time to time, even if it wasn't really necessary. He was a hobbyist and a technician, and he knew a shit-ton about electronics. We would not have done as well as we did without him. I relied on his knowledge on a daily basis. The odd thing about him, though, was that he was kind of the born-to-lose type. He had test anxiety, and he'd often do an awesome job on a project only to psych himself out and blow it all when crunch time arrived. Since the bot was allowed to shoot projectiles after reaching the edge of the ring we riffed on possibilities for a turret that could quickly whip around and fire before the other bot had even begun to turn around. It was ambitious, and he ate it up. I was glad to have him assigned to something that could really make us, but not break us if it didn't work out. 

Meanwhile, I took the lead on the guts of the bot. It was a little bit of "if you want it done right do it yourself" but without the bitter aftertaste. What I wanted to avoid was what happened in a similar situation as an undergrad: Mr. Superstar guy decides he can do it all himself, while the rest of us are dismissed (happily at the time, which I regret) and don't even realize that he's crashing and burning until it's too late. We all get C's. No, I let our slacker guy know that we were going to need him in that final stretch, and he came through when it was time to start putting it all together.

That's another thing I wonder about: at the outset, my teammates outvoted me - they wanted to build our own bot from the ground up, even down to fabricating the chassis. I objected, but relented... maybe too easily. I would have rather built off of a toy RC car, which is what the team that beat us had done (and we had even helped them out several times along the way). All's well that ends well, though. The bot was slow and a little janky. The turret was a bust. But in the end we all came together and got it done. We still kicked ass. We all got A's. I learned a bit about leadership. Life goes on.
