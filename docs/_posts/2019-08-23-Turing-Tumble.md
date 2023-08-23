---
layout: post
title: "Turing Tumble"
date: 2019-08-23 17:34:12 -0000
categories: CATEGORY-1 CATEGORY-2
---

Turing Tumble is a game I found in the raspberry pi shop where you have to solve problems by placing parts on a grid and then letting balls fall down. I spent hours in there solving some of the harder problems. Here are some videos of solutions to my favorite problems going from easy to hard.

1.) Addition of two registers
This is the easiest out of the three. You must consider both vertical blue arrow columns as registers. If the arrow is facing left it is a 0 and right it is a 1. The highest arrow is the 1's units column then 2 then 4 then 8. The aim is to add the two registers together with the answer being stored in the register on the right. The way it is implemented below is that every time a blue ball falls it subtracts one from the left-hand side and then causes a red one to fall which adds one to the right-hand side which then calls a blue ball again. This process repeats until the register on the left displays 0 which then causes the blue ball to be caught in the bowl. I will leave it up to the reader to work out how one is subtracted and added.
