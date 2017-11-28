---
layout: post
title:  "Udacity Self-Driving Car Nanodegree Final Project, Part 1 - The Git Master"
date:   2017-11-28 21:00:00 
categories: udacity, self-driving car, nanodegree, project, final, capstone, system integration, git
---

![Capstone pt2 cover image](https://github.com/jeremy-shannon/jeremy-shannon.github.io/blob/master/images/capstone/capstone_pt2_cover.png?raw=true)

*This is Part 2 of my account of the [Udacity Self-Driving Car Engineer Nanodegree](https://udacity.com/drive) program's final project. Read Part 1 [here](http://jeremyshannon.com/2017/11/08/udacity-sdcnd-capstone-pt1.html).*

I left off last time right at the starting gate. I'd gone through the lesson material and the final project description and instructions. The next step was to browse through a shared spreadsheet and find a team with an open slot, or create a new team if there were no open slots. (If nothing else had tipped me off so far in the past year, I could definitely tell that Nanodegree students are my kind of people from this spreadsheet - all slots had been filled on all teams all the way down to the bottom of the list, just like you'd wish people would fill seats at a theater.) I filled the fourth slot on the last team listed on the page, Team Bacon. Sounds like my kind of team - nobody's taking themselves too seriously on Team Bacon, that's for damn sure.

I e-mailed my five new teammates, who happened to be scattered across the United States and Europe, and we set up our first conference call. We discussed the project and made sure we were all on the same page and understood what needed to be done. Then it was time to volunteer for tasks. If I may remind you of the project block diagram:

![Capstone ROS graph](https://github.com/jeremy-shannon/jeremy-shannon.github.io/blob/master/images/capstone/capstone_ros_graph.png?raw=true)

The tasks available were:

- Waypoint Updater node (first pass)
- DBW node
- Traffic Light Detector node

(read more about these in [Part 1](http://jeremyshannon.com/2017/11/08/udacity-sdcnd-capstone-pt1.html))

Typical of me, I waited for others to choose their tasks before volunteering for whatever might be left (if we've ever been to an office potluck together, you'd have surely noticed me waiting for the line to dwindle down to nearly nothing before queueing up myself; I might miss out on some hashbrown casserole, but I don't really mind). I had assumed all along that I'd be handling the vehicle controls in the DBW node, mostly because computer vision and machine learning seemed so popular among other Nanodegree students. To my surprise, two of my teammates immediately signed up for the DBW node. The team leader then chose the Waypoint Updater node, and another teammate chose the Traffic Light Detector node. I decided I would help out with the Waypoint Updater node to start with, since it was the first order of business, then move on to help with the Traffic Light Detector node afterward. 

We created our team repo on GitHub, cloned the Udacity starter code, and we were off. Each team created a branch in which to implement their feature. By the time I was ready to start work on the Waypoint Updater node, I'd found that my team leader (because he was several time zones ahead of me) had already finished the first pass at it. What?! Not only that, but a good chunk of the DBW node was complete as well. My teammates were ready to merge their changes into the master branch and they either hadn't done such a thing before or they were going to bed (the Europeans, anyway). It was up to me, and the only such experience I'd had was while messing around with branching and merging in Team Foundation Server. All of my work projects had only ever been in individual repositories, if there were any sort of central repository at all! I'd figure it out, though. Here I was, Team Bacon's... Git Master! (How cool does that sound?)

A lot of my merging happened right there in the GitHub web interface, mostly because I was away from home at the time. I was surprised at how easy it was to merge whenever there were no conflicts. Just press the button and it was done. This was useful any time Udacity made changes to the upstream repo, as well. I could easily do comparison between our repo and the upstream Udacity repo and initiate a pull request from right there.

![GitHub Merge](https://github.com/jeremy-shannon/jeremy-shannon.github.io/blob/master/images/capstone/github_merge.png?raw=true)

Sometimes, though, GitHub would throw up its hands and tell me I needed to merge conflicts else ware. My first stop was Visual Studio Code. I'm a fan of Visual Studio Code. I know a lot of purists cringe at the thought of using any sort of GUI git interface, but I like it and I think it's a good option for those of us who don't live on the command line on a daily basis. Not that I can't hang with the command line, but I feel like I spend more time looking up what I need to do that way. VS Code's merge tool was simple and effective and I enjoyed it... while it lasted.

![VS Code Merge](https://github.com/jeremy-shannon/jeremy-shannon.github.io/blob/master/images/capstone/vscode_merge.png?raw=true)

I don't know what I did, but at some point I broke it and VS Code's merge tool was all jacked up (as my toddler might say). I went to the trusty command line and it gave me a new merge option - the Mac OS default merge tool. I think it was called OpenDiff. Apparently it's not especially popular, judging by the lack of recent screenshots available on Google image search, but it got the job done.

![osX OpenDiff Merge](https://github.com/jeremy-shannon/jeremy-shannon.github.io/blob/master/images/capstone/osx_merge.png?raw=true)

It might seem like small potatoes, but I feel like this was a great learning experience and probably a skill that will serve me extremely well in the future. Though I'll probably dispense with the "Git Master" moniker... publicly, anyway.

Next time: Traffic Light Detector node!

*The code for this project can be found on [my GitHub](https://github.com/jeremy-shannon/CarND-Capstone).*