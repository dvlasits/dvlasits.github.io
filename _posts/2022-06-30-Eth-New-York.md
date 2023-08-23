---
layout: post
title: "Eth New York"
date: 2022-06-30 14:48:44 +0100
categories: Blockchain
image: files/EthNewYork/skyscraper.jpg
comments: false

---

I had the incredible opportunity to attend the Ethereum New York Hackathon in June.


I was hoping to lay down here briefly the project I came up with developed in a team that went on to win several first place prizes.


[Here is a link to our project on the Eth Global site: ](https://ethglobal.com/showcase/messageinabottle-y6o6k){:target="_blank"}


I went into this hackathon with very little knowledge of Blockchain and Cryptocurrencies. However, I spent two days in advance initially watching a lecture course by Gary Gensler at MIT open course ware. It is an amazing series that really helps get the fundamentals across. I then watched most of this video https://www.youtube.com/watch?v=gyMwXuJrbJQ&t=59725s. Which is an incredibly long video but teaches you everything you need to know about developing blockchain applications.

**There was a very important lesson I leant here about the incredible power of delving into a topic learning before you start coding. It only took me two days, and it was an absolute game changer for the hackathon.**

The problem I wanted to solve was a Decentralised Messenger app. However, what always bugged me was the irony that whilst Blockchain claims to be privacy centric (The technical term being pseudo-anonymous) all transactions are visible and therefore even with encrypted messages you could form a graph of who is sending messages to whom, which is powerful data that current messenger based apps capitalise off of. So my goal was coming up with a solution that was not only decentralised but **anonymised** too.

This was what we came up with!

We facilitate it by setting up this protocol: If you want to send the message to someone, you have to know their public key. Then, you encrypt a message “I want to talk to you, talk to me at this IPNS address XXX”. Then, you wait for the receiver to decrypt your message, and once that’s done, you both move to the IPNS to continue your communication. One might wonder how that could possibly scale?- The network potentially has ~1 trillion edges. We resolved this by making everyone's public keys hash to a number between 1-1000. This way, the receiver of the messages has to attempt to decrypt only one of the 1000 arrays of messages that were sent, which cuts the time to identify a sender to a few seconds (and subsequent communication) is fast, as it happens through IPFS.

And we won the:

WalletConnect — Best Social

Gnosis Chain — Best Use

Here is a photo of the finished app:

![Eth New York]({{ site.baseurl }}/files/EthNewYork/app_photo.png)

Here is a gallery of some other photos:

![Eth New York]({{ site.baseurl }}/files/EthNewYork/asleep.jpg)
![Eth New York]({{ site.baseurl }}/files/EthNewYork/closeup.jpg)
![Eth New York]({{ site.baseurl }}/files/EthNewYork/group.jpg)
![Eth New York]({{ site.baseurl }}/files/EthNewYork/skyscraper.jpg)




