---
layout: post
title:  "Clojure - Luminus - Enabling basic auth for specific routes"
date:   2015-08-15 06:50:00
categories: clojure luminus ring-basic-authentication 
---

The [ring-basic-authentication][ring] library makes it easy to add http auth to your Luminus web app; however, I wanted auth to only apply to certain routes. I ended up wrapping the HTTP auth wrapper with a simple check to enable this. I added the following to middleware.clj:


Require: 

{% highlight clojure %}
[ring.middleware.basic-authentication :refer [wrap-basic-authentication]]
{% endhighlight %}



{% highlight clojure %}

(defn authenticated? [name pass]
  (and (= name "foo")
       (= pass "bar")))

(defn wrap-bauth [handler]
  (fn [req]
    (if (boolean (re-find #"admin" (get req :path-info)))
      ((wrap-basic-authentication 
          handler
          authenticated?) 
       req) (handler req))))
{% endhighlight %}


Once the wrapper function is defined, the function can be added to the wrap-base chain.

{% highlight clojure %}
(defn wrap-base [handler]
  (-> handler
      wrap-dev
      wrap-formats
      wrap-webjars
      wrap-bauth
      (wrap-defaults
        (-> site-defaults
            (assoc-in [:security :anti-forgery] false)
            (assoc-in  [:session :store] (ttl-memory-store (* 60 30)))))
      wrap-context
      wrap-internal-error))
{% endhighlight %}

Now the basic auth wrapper will only run on routes that match the condition. Obviously, you can customize this to whatever criteria you want.

You can follow me on twitter at [@klopkev][klopkev].

[klopkev]: http://twitter.com/klopkev
[ring]: https://github.com/remvee/ring-basic-authentication 
