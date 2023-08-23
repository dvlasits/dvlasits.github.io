---
layout: post
title: "Project Euler: Diophantine Equations"
date: 2019-09-10 14:48:44 +0100
categories: puzzles programming
published: false
---

Project Euler is a great website for solving problems you can read up on it [here](https://projecteuler.net/): 

I have had a lot of fun doing Project Euler problems and wanted to show off some of my favourite ones and the maths 
behind them.

Lets look at [Question 110:](https://projecteuler.net/problem=110)

1/x + 1/y = 1/n

What is the first n so that the number of distinct solutions to this Diophantine equation (Only integer solutions) 
is greater than 4 million.

My Solution:

Rearranging the equation you get

xy - nx - ny = 0

which you can then factorise:

(x - n)(y - n) = n^2

So the number of solutions is equal to the number of pairs of factors of n^2. N can be written as its prime factors with each prime having an even power. You can calculate the number of factors of a number if you take the exponents of all the primes add 1 to each and multiply together. This works because for each prime it can have from 0 - the exponent number and therefore multiplying gives all possible combinations. Therefore if you calculate number of factors/2 and ceiling it you get the number of factor pairs and therefore the number of distinct solutions.


As the number of factors depends solely on the exponents n^2 must be "top heavy" i.e the prime factorization of it must be the highest exponent for two and decreasing or staying the same as you go down. 


I, therefore, tried to recursively implement a function that would start with nothing. Would then fire off itself with varying even exponents for two and then each function would do varying even exponents for 3 making sure it was smaller than or the same to previous exponents. It would then calculate the number of factors using the method decided above. If it was over 4 million it would then calculate the value of the number and check if it was better than the minimum value calculated thus far. I then tried to run this code guessing the largest exponent wouldn't be bigger than 40 letting it run for a bit then taking the best value I got, however, I reached the recursion limit of python.


I therefore then re-coded the solution iteratively using a 2d array wherein each loop it would create several new arrays within the 2d array of the new exponent values. Check and then repeat. Getting an answer very quickly that I will not display to not completely ruin the fun of you.


You can check out my solution from Github [here.](https://github.com/dvlasits/Project-Euler/tree/master/110)