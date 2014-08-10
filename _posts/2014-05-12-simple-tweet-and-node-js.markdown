---
layout: post
title:  "Creating a Twitter bot with Node.js"
date:   2014-05-12 09:50:00
categories: node.js twitter
---

Open a terminal window and enter the following command:

{% highlight bash %}
git clone git@github.com:kklopfenstein/simpletweet.git
{% endhighlight %}

Now open the twit_config.json in your favorite editor:

{% highlight bash %}
cd simpletweet
vim twit_config.json
{% endhighlight %}

[simpletweet][simple]

{% highlight javascript %}

selectTweet(tweet_id, screen_name, tweet_text, function(rows) { 
  insertTweet(tweet_id, screen_name, tweet_text, function() {
    tweetReply(tweet_id, screen_name);
  });
});

{% endhighlight %}


You can follow me on twitter at [@klopkev][klopkev].

[klopkev]: http://twitter.com/klopkev
[simple]: http://github.com/kklopfenstein/simpletweet
