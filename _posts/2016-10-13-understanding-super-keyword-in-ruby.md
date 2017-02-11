---
layout: post
title: "Understanding super keyword in Ruby"
date:   2016-10-13 00:00:00 -0300
categories: ruby
---
After read "super" keyword in many pieces of code in rails I just decide to share the meaning for this.

> Called from a method, searches along the method lookup path (the classes and modules available to the current object) for the next method of the same name as the one being executed. Such method, if present, may be defined in the superclass of the object‘s class, but may also be defined in the superclass‘s
superclass or any class on the upward path, as well as any module mixed in to any of those classes.

In the others words

> super calls a parents methods for the same name with the same arguments

Example:

{% highlight ruby %}
class People
  def name
    puts "Nelson"
  end
end
{% endhighlight %}

{% highlight ruby %}
class Entrepreneur < People  
   def name
    puts "Mario"
    super
   end
 end
{% endhighlight %}

When I create an object for entrepreneur and call the method for this:

{% highlight ruby %}
entrepreneur = new Entrepreneur()  
entpreneur.new.name()
{% endhighlight %}

I got this results:

{% highlight ruby %}
Nelson  
Mario
{% endhighlight %}
