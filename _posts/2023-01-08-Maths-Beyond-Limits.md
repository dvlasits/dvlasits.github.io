---
layout: post
title: "Maths Beyond Limits"
categories: ["teaching"]
date: 2023-01-08 14:48:44 +0100
description: "I taught at an amazing maths camp in Poland!"
featured: false
image: files/MathsBeyondLimits/group_photo.jpg
categories: teaching
---

Maths Beyond Limits is an incredible Mathematical Camp hosted in Poland for high school students around the world.


I had an amazing time, and the participants were awesome. Really could not recommend applying enough if you can, either to be a participant or a tutor.


I taught two courses:


Lambda Calculus:

I love lambda calculus, and showing the power it has considering how basic it seems. I came up with this handout attached. The aim of all the lessons was to get the students to come up with everything themselves. The aim was to code up an infinite list of primes, in lambda calculus using python. Which was hilarious at times and gave code looking like this:

{% highlight python %}
equal = lambda n1 : lambda n2 : negation(orOp(greater(n1)(n2))(lessThan(n1)(n2)))


doFact = lambda h : lambda n : \
ifte(isZero(pred(n)))(lambda : one)(lambda : mult(n)(h(h)(pred(n))()))
{% endhighlight %}

[Here is the lambda pdf](/files/MathsBeyondLimits/Lambda.pdf){:target="_blank"}

If you're interested in trying the exercises they are all in here.


Complexity Theory:

The second course I taught was complexity theory. Which has a lot of very interesting exercises within it revolving around translating problems into other problems which you know how to solve.

[Here is the complexity pdf](/files/MathsBeyondLimits/Complexity.pdf){:target="_blank"}

My handout is a very compressed version of the great notes written by Prof . Anuj Duwar at the University of Cambridge.


I discovered a love of teaching and hope to pursue it more often in the future. In the meantime, I plan to look into some of the theory behind teaching well. 