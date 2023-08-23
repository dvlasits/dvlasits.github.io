---
layout: post
title: "Final Piece of the Haskell Puzzle"
date: 2022-12-14 14:48:44 +0100
categories: haskell
---

I would like to preface this by saying Haskell is a never ending hole but still.


So I was back at it this year with Advent of Code and Haskell.


GitHub: https://github.com/dvlasits/AoC-Haskell

I happened to stumble across Lens' and decided to do some reading into what they were and what they were about. I read most of this amazing book called "Optics By Example Functional Lenses in Haskell" and discovered they were an absolute game changer.


I would now consider them almost vital to being able to write Haskell in a useable way. Simple examples are lets say you want to set the middle item of a tuple:


Is a function which takes (in fact any tuple of size 2 or greater) and will update the 2nd and will set the second element to 5.

{% highlight haskell %}
_2 .~ 5 
{% endhighlight %}

The power from them really comes from being able to compose them for example:

{% highlight haskell %}
_2 . _3 %~ (\x -> 2*x+3)
{% endhighlight %}

Will take the 2nd element and then the 3rd element of that, and set it to 2*x+3.


So that's composability and then you get onto incredible power with folding and traversing to update "lists" and other objects.


For example lets say you want to update every element in the 3rd column of a list

{% highlight haskell %}
traversed . ix 2 %~ (\x -> x^2 + 2)
{% endhighlight %}

And the final crazy thing I wanted to show in this is the partsOf combinator:

Lets say you want a function that does this:

{% highlight haskell %}
[('a', 5), ('b', 3), ('c', 10)] -> [('b', 5), ('c', 3), ('a', 10)]
{% endhighlight %}

i.e. it cycles the letters around the tuples can be done like this:

{% highlight haskell %}
partsOf (traversed . _1) %~ (drop 1 . cycle)
{% endhighlight %}

And then you get onto incredibly powerful features about being able to traverse almost anything not just classically traversable type classes.

For example in one example I wanted all the cells around a coordinate i.e. 

{% highlight haskell %}
(10,11) -> [(10,12),(10,10),(11,11),(11,12),(11,10),(9,11),(9,12),(9,10)]
{% endhighlight %}

I can now do this as follows:

{% highlight haskell %}
(delete <*> (both %%~ (\x -> [x, x+1, x-1])))
{% endhighlight %}

Which I thought was pretty neat using the list monad non deterministically as both allows you to traverse both parts of the tuple.

So! I highly recommend you check Lens out and the incredible "Optics By Example" book. 

Having even just a basic understanding of _1, ix and at. Is an absolute game changer (may have said that already). 