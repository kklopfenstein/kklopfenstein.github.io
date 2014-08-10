---
layout: post
title:  "Creating a Twitter bot with Node.js"
date:   2014-08-10 11:50:00
categories: node.js twitter
---

This tutorial will show you how to create a simple twitter bot that tweets at users that have tweeted public tweets with certain keywords. It will also tweet normal tweets randomly at configurable intervals.

NOTE: This tutorial assumes you have node, npm, and git installed. If you don't have these tools install them first.

Open a terminal window and enter the following command:

{% highlight bash %}
git clone git@github.com:kklopfenstein/simpletweet.git
{% endhighlight %}

Install the dependencies:

{% highlight bash %}
npm install twit
npm install datejs
npm install sqlite3
npm install moment
npm install node-rest-client
{% endhighlight %}

Now open the twit_config.json in your favorite editor:

{% highlight bash %}
cd simpletweet
vim twit_config.json
{% endhighlight %}

Set the twit_data information to your twitter information (consumer key, consumer secret, access token, access token secret). If you don't know this info visit https://dev.twitter.com/apps/new.

Set the phrases array to the random phrases you want your bot to tweet. For example:
{% highlight javascript %}
"phrases": [
   "phrase1",
   "phrase2",
   "phrase3"
]
{% endhighlight %}

The twitter bot script will search public tweets for a specific phrase. Enter this phrase under search_phrase.

Enter your bot's screen name under bot_screen_name.

Now you're all set! Run the twitter bot with:

{% highlight bash %}
node simpletweet.js
{% endhighlight %}

[simpletweet][simple]



You can follow me on twitter at [@klopkev][klopkev].

[klopkev]: http://twitter.com/klopkev
[simple]: http://github.com/kklopfenstein/simpletweet
