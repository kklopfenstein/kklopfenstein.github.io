---
layout: post
title:  "My first foray into Node.js"
date:   2014-05-12 09:50:00
categories: node.js twitter
---

I've been following Node.js for a couple years with some interest. JavaScript on the server side is an intriguing concept, and I've always had a love of JavaScript but Android has kept me so busy the past two years that I haven't had time for much else.

I started into the world of Node by writing a small twitter bot I've named [simpletweet][simple]. It searches Twitter for a keyword and periodically replies to tweets using that keyword with a few random phrases. It also favorites retweets. I'm hoping to add some following functionality in the near future.

One thing that takes some getting used to when writing Node, coming from a Java background is the constant use of nesting callbacks. Regardless of what you think about this pattern, it's hard to write much Node code without it. It takes some getting used to at first. Although these kinds of patterns are almost possible in Java with anonymous classes, the syntax is so unwieldy that it isn't a whole lot of fun to use. For example:

{% highlight javascript %}

selectTweet(tweet_id, screen_name, tweet_text, function(rows) { 
  insertTweet(tweet_id, screen_name, tweet_text, function() {
    tweetReply(tweet_id, screen_name);
  });
});

{% endhighlight %}

It takes a bit of getting used to but overall I've enjoyed working with Node an am excited to keep hacking with it.

You can follow me on twitter at [@klopkev][klopkev].

[klopkev]: http://twitter.com/klopkev
[simple]: http://github.com/kklopfenstein/simpletweet
