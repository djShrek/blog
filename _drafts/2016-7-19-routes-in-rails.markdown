---
layout:     post
title:      "Naming Routes in Rails"
date:       2016-07-19 12:00:00
author:     "bobby"
---

<p>Other than typing my standard resources :posts to routes, mapping routes to
controllers in Rails has always been one of the most annoying things to do. For starters,
you have to remember to either use nested routing, or wrap the route in a scope block, or wrap the route in a namespace block or 10 other things that I can't remember right now. But alas, I was assigned to an API project and needed to figure out how to write proper routes in a DRY way. When I first started writing the code, I was lazy and just added: </p>

{% highlight ruby %}
def show
  @widget = Widget(params[:id])
  respond_to do |format|
    format.html # show.html.erb
    format.json { render json: @widget }
  end
end
{% endhighlight %}