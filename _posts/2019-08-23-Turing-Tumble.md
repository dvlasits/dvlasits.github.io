---
layout: post
title: "Turing Tumble"
date: 2019-08-23 14:48:44 +0100
categories: puzzles
image: files/TuringTumble/photo.jpg
comments: false
---

Turing Tumble is a game I found in the raspberry pi shop where you have to solve problems by placing parts on a grid and then letting balls fall down. I spent hours in there solving some of the harder problems. Here are some videos of solutions to my favorite problems going from easy to hard.

1.) Addition of two registers
This is the easiest out of the three. You must consider both vertical blue arrow columns as registers. If the arrow is facing left it is a 0 and right it is a 1. The highest arrow is the 1's units column then 2 then 4 then 8. The aim is to add the two registers together with the answer being stored in the register on the right. The way it is implemented below is that every time a blue ball falls it subtracts one from the left-hand side and then causes a red one to fall which adds one to the right-hand side which then calls a blue ball again. This process repeats until the register on the left displays 0 which then causes the blue ball to be caught in the bowl. I will leave it up to the reader to work out how one is subtracted and added.

<iframe width="560" height="315" src="https://www.youtube.com/embed/PB-7Wrj7beo" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

2.) Creating a certain pattern

The challenge here is to end up with a pattern that goes 2 blue 1 red 4 blue 1 red 8 blue. This is accomplished by using gears. The gears are useful as you can set them up so that the first ball that goes down it goes right and every other one goes left. Now consider the 3 on the left as another register like above and the two on the right as another register. All the gears start so that the first one will go right then the rest left. This means initially the left 3 registers can be considered as just a 1 bit register of the one right on the top. Counting down from 1 to 0 and then hitting the gear causing a red one to fall which just subtracts one from the register on the right. The red one triggers another blue one where the top two registers can now be considered allowing 4 to go down then 1 red then 8 blue go down as now all 3 registers are involved and finally the red one gets caught as it has finished subtracting 1 from 2 3 times.

<iframe width="560" height="315" src="https://www.youtube.com/embed/PNk64LVherU" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

3.) Comparing two registers and displaying which one is bigger:

The aim of this one is to decide which register is bigger, the one on the left or on the right, however, I don't think I can explain this one here in a way that would be clear so I think you should watch it and see if you can work it out yourself.

<iframe width="560" height="315" src="https://www.youtube.com/embed/biM-GymXEP0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
