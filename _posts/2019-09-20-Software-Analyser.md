---
layout: post
title: "Software Analyser"
date: 2019-09-20 14:48:44 +0100
categories: puzzles programming
published: false
---

I am going to talk about an interesting part of my ongoing Computer Science Coursework as I am finding it fascinating. A part of my coursework needs to time code that calculates the runtime of each function.

![SoftwareAnalyser](/files/SoftwareAnalyser/SmallSmall.png)

My code attaches decorators to every function in the code it is analyzing which records the starting and stop time of each function in an array. That array is then deconstructed to work out how much total time is spent solely in one function not counting the time that another function within that function runs for. So a user can see exactly what parts of an algorithm are taking up the time. The code then outputs a graph such as the one below with the name and times spent in each function on the node and the number of times one function called another on the edges.

![SoftwareAnalyser](/files/SoftwareAnalyser/GraphLong.png)

Adding up all the times in each node would then tell you how much time the code takes. For example, you can see on the graph above that most of the time is taken inside Toggle and Turn even though Finding is called 300 times. My algorithm for working out the times works as follows:


Just before a function is run the time it starts is appended into an array along with a unique name for that instance of the function. When the function is finished the decorator then also appends the finish time of the function into the array along with the name so array might look like:


[(start 1 , 10), (add 1 , 12), (add 1 , 13),(add 2 , 15),(add 2, 17), (start 1 ,18)]


My code then loops through this array looking for where it can see the same instance of a function start and stop next to each other and then concatenates them into a time adding on the (end time - start time) onto the total time spent inside that function e.g.


after first pass array would look like:

{% highlight python %}
[(start 1 , 10), 1,(add 2 , 15),(add 2, 17), (start 1 ,18)]
{% endhighlight %}

{% highlight python %}
TimeSpentInAdd = 1
{% endhighlight %}
It would then pass again looking where either start-stop next to each other or solely separated by times. If times in between it would calculate (start time - stop time) - sum of times in between e.g.

after second pass:

{% highlight python %}
[(start 1 , 10), 1,2, (start 1 ,18)]
{% endhighlight %}
{% highlight python %}
TimeSpentInAdd = 1 + 2 = 3
{% endhighlight %}
After third pass:
{% highlight python %}
TimeSpentInStart = (18-10)-(1+2) = 5
{% endhighlight %}



Concluding that 3 seconds was spent inside the add function and 5 seconds inside the start function. However, this is a very slow algorithm basically of order O(n^2) which takes way too long analyzing code that has millions of function calls such as code using lots of recursion such as the Fibonacci Recursive code shown in the Project Euler Blog. I am now coming up with a faster algorithm for doing this and I believe the best way is to somehow calculate the times inside the decorator functions while the code is running as soon as timestamps are returned instead of having to unwind the whole array at the end.


I am also now deciding what algorithms can be run on the graphs created to help the user e.g. maybe longest way through the network to show what paths need optimization and ideas like that.