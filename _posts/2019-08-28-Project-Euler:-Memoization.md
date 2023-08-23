---
layout: post
title: "Project Euler: Memoization"
date: 2019-08-28 14:48:44 +0100
categories: puzzles programming
hidden: true
---

I wanted to talk about something I learnt that I found really interesting called memoization. Memoization is where recursive functions memorize what has been passed in and what was returned and therefore can sometimes avoid recursing parts that have already been found once. For Example:

![Memoization]({{ site.baseurl }}/files/Memoization/FibBasic.PNG)

This is a recursive function that calculates the nth Fibonacci number. Anything under 35 it can calculate in under 2 seconds. However, if you try to do anything above 35 it slows down tremendously and is useless. If you use memoization the function works fine. Memoization is an inbuilt python tool that can be used:

![Memoization]({{ site.baseurl }}/files/Memoization/fibMemo.PNG)

The function now works fine up until incredibly large values of n.

I then solved several Project Euler questions using this technique and will mention one specifically below:

[The question](https://projecteuler.net/problem=67) is if you have a triangle of numbers. By starting from the top and either moving one left or one right each time. What is the maximum amount of points you can accumulate? Please click question number for official instructions.


It is very easy to write a recursive function to do this however it takes too long. As soon as you add memoization to it completes the problem nearly instantly which I thought was amazing. Particularly because I think recursively coding is a very nice way to code, and sometimes the easiest way to complete a problem (if it runs in time). Which is why I think memoization is so amazing. As you can see below it is a lovely compact and clear solution:

![Memoization]({{ site.baseurl }}/files/Memoization/TriangleTraverse.PNG)