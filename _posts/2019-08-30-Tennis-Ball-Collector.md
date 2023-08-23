---
layout: post
title: "Tennis Ball Collector"
date: 2019-08-30 14:48:44 +0100
categories: robotics programming
---

This year I also worked on the code for a tennis ball collector here is a montage of it in action:

<iframe width="560" height="315" src="https://www.youtube.com/embed/zFFhGiJY3dc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

When the robot is on the concrete it is autonomously finding and picking up the tennis balls. It does this using a pixy camera on the front. First I tried to use a normal Pi-camera to find the tennis balls using a combination of the hough-circles algorithm in OpenCV and the colour however I couldn't process the frames fast enough for the robot to work well. I even tried threading the two processes of taking photos and analyzing but it wasn't good enough. I then tried the pixy camera to try and find the ball based off of just the colour. This worked very well on the concrete but ran into issues on the tennis pitch as the colour of the grass was too similar to the colour of the ball. The camera turns until seeing a ball and then drives towards the ball turning on the flywheels that shoot the ball up into the basket. It was also very interesting controlling the fly-wheels as they are brushless motors which meant a much more complicated controlling mechanism than normal motors. First, they needed to be calibrated and then they required a PWM to operate as well.

Showing off the development process

<iframe width="560" height="315" src="https://www.youtube.com/embed/c9xnYyBKsZs" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>