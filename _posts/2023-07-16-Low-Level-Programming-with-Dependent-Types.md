---
layout: post
title: "Low Level Programming with Dependent Types"
date: 2023-07-16 14:48:44 +0100
categories: Programming Idris Types
image: files/LowLevelIdris/code.png
featured: true
comments: false

---

This is the first library to guarantee the elimination of pointer bugs and array bounds bugs at runtime whilst allowing for low-level operations. It also allows for duplicating pointers without resorting to reference counting, like Rust has to. Allowing for a type of compile time reference counting.

[The full writeup is here](/files/LowLevelIdris/Low_level_programming_in_Idris.pdf){:target="_blank"}

An article by google said that half of the known exploitable bugs in chrome are use
after free bugs. This is when a pointer is accessed after the data it was pointing to
had been freed.

This can lead to undefined behaviour and worse security bugs.
Double free bug is when a buffer is free’d twice in memory. It can lead to memory
leaks, and can also lead to heap exploitation by a hacker, where they could control
memory at a location only the process should have access to.

To protect against indexing out of bounds most programming languages must
check on each index to the array that it does not index out of bounds, crashing with
an error if it does not occur. This incurs an overhead that systems languages such
as C avoid but leads to undefined behaviour if you index out of bounds. There is
therefore a cost to using either of these solutions.

The tradeoff that is made in most languages concerning these is either you can
do what you would like which can lead to undefined behaviour or you use a higher
level language that protects against this but leads to slower runtime.
These are the problems I would like to address using the incredibly powerful type system available in Idris 2.

Idris 2 is an absolutely crazy language which combines both Dependent Types and Linear Types into something called Quantitative Type Theory.

So ... What are Linear Types:

We can define a function with the type signature

{% highlight haskell %}
f : (1 _ : Int) -> Int
{% endhighlight %}

The intuition behind this is that if the output i.e. (f 5) is "consumed exactly once" then we guarantee that the inputted argument is "consumed exactly once" in total.

Where we can think of "something being consumed once" as:

for a base type: evaluate x

for a function: apply x once and consume the result once

for a pair pattern match on x, and consume each component once

What this allows us to do is control how much something is used (e.g. an expensive resource) what it also means is we guarantee that it is only ever in one place. Which is very useful when working with pointers.

In my project I have used this to eliminate (at compile time) all possible pointer errors.

This can be done with 3 simple functions:

{% highlight haskell %}
alloc : ((1 mem : Ptr) -> IO a) -> IO a
write : Int -> ((1 mem : Ptr) -> IO a) -> (1 mem : Ptr) -> IO a
read : (Int -> (1 mem : Ptr) -> IO a) -> (1 mem : Ptr) -> IO a
free : (1 mem : Ptr) -> IO a
{% endhighlight %}

These functions never allow the pointer to escape, and as the ptr can only be consumed with free guarantee it is created in one place, then used, and then free'd.

Dependent types allow the type of a functions output to depend on the value of its input.

For example:

{% highlight haskell %}
getType : Int -> Type
getType 0 = String
getType _ = Int

doSomething : (x : Int) -> (getType x)
doSomething 0 = "Zero"
doSomething x = 7*x
{% endhighlight %}

And this type checks and compiles. Which I think is absolutely incredible.

The absolute classic example given for dependent types is a vector:

{% highlight haskell %}
data Vect : Nat -> Type -> Type where
Nil : Vect Z a
(::) : a -> Vect k a -> Vect (S k) a
{% endhighlight %}

So, here we define Nil to have the type Vector 0 a.

And whenever you get given an value of type Vector x a you can construct a value of type Vector (x+1) a by putting an element in front.

This then allows us to do something like:

{% highlight haskell %}
append : Vect m a -> Vect n a -> Vect (n + m) a
{% endhighlight %}

Where at the type level we can specify that append must return a vector of the correct size.

We then get into crazy things like you can carry around proofs such as

(LT = Less Than)

{% highlight haskell %}
index : (index : Nat) -> LT m size -> Vect size a -> a
{% endhighlight %}

This then guarantees at the type level that you can only pass Natural numbers when you can prove that the number is less than the size of the array.

So that is a way too quick overview of these ideas. But I am using them to write a completely safe pointer library in Idris 2 to handle lists structs and anything else:

Using some other things such as linear monad my library then allows you to write code like this:

{% highlight haskell %}
main = do
arr <- createArr 100
val # arr <- readArr 1 arr
arr <- writeArr 20 5 arr
freeArr arr
{% endhighlight %}

Where createArr creates the array. ReadArr reads the array and returns the value and a new pointer to the array, where you have unrestricted usage of the val but still linear in the arr.
Any of the following code would result in an error:

{% highlight haskell %}
main = do
main = do
arr <- createArr 100
{% endhighlight %}

Would give an error saying arr isn't freed

{% highlight haskell %}
main = do
arr <- createArr 100
writer 2000 2000 arr
{% endhighlight %}

Would give an error saying cannot write to position 2000 in an array of size arr. This is therefore very powerful and allows for low-level programming without compromising safety of code.

It gets even more crazy when you get into trying to do all of this polymorphically and leads to ridiculous type signatures such as:

{% highlight haskell %}
update : {t : Type2} -> {s : Nat} ->

(MyVectL (S s) t parent my) -> (Fin (S s)) -> (case t of

     TInt => Int -> Int
     TChar => Char -> Char
     TStruct l => {m : Maybe AnyPtr} -> {p : AnyPtr} -> (1 _ :
            MyStructL l m p) -> L IO {use=1} (MyStructL l m p)
     TArr s2 l => {m : Maybe AnyPtr} -> {p : AnyPtr} -> (1 _ :
                       MyVectL (S s2) l m p) -> L IO {use=1}
                                 (MyVectL (S s2) l m p))

-> L IO {use=1} (MyVectL (S s) t parent my)
{% endhighlight %}

Where basically you have to case split on what is contained within a list to decide whether you can treat it unrestricted or have to return the pointer you got to respect the constraints.

But yeah, that's just to show off how crazy idris can get, I will link to a full writeup of my project when it is done.
