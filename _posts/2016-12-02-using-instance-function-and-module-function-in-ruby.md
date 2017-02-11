---
layout: post
title: "Using instance function and module function in Ruby"
date:   2016-12-02 00:00:00 -0300
categories: ruby, rails
---
### Instance function
Module function can be mixed in different classes and these are invoked as instance method
for the object of that classes:

{% highlight ruby %}
module Library  
  def welcome
    puts 'Welcome!'
  end
end  
{% endhighlight %}

{% highlight ruby %}
class Account  
  include Library
end  
{% endhighlight %}

{% highlight ruby %}
a = Account.new  
a.welcome #this return: Welcome!   
{% endhighlight %}

### Module functions

A module functions is a function invoked from a module

{% highlight ruby %}
module Library  
  def welcome
    puts 'Welcome!'
  end
end   
{% endhighlight %}

{% highlight ruby %}
Library.welcome
{% endhighlight %}

### Using module function in a class

If you want to use [module function][module-function-url] with a class you need to use module_function, here an example:

{% highlight ruby %}
module Library  
  def welcome
    puts 'Welcome!'
  end
  module_function :welcome
end  
{% endhighlight %}

{% highlight ruby %}
class Account  
  include Library
end  
{% endhighlight %}

{% highlight ruby %}
Library.new.welcome #=> Welcome!  
Account.welcome #=> Welcome!  
{% endhighlight %}

[module-function-url]: http://ruby-doc.org/core-2.2.0/Module.html#method-i-module_function
