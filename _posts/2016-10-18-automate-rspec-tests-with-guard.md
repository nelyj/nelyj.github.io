---
layout: post
title: "Automate RSpec tests with Guard"
date:   2016-10-18 00:00:00 -0300
categories: testing
---
![image-guard](http://i1382.photobucket.com/albums/ah245/nelsonpatojimenez/Guard-setting_zpsyfsqvu2p.gif)

After some time using RSpec for test in Rails Apps I discovered that I can use [Guard][guard-url] for automate tests.

> Guard::RSpec allows to automatically & intelligently launch specs when files are modified.

Guard is a command line tool that watches a file structures when changes are in those files.

## Installing Guard

Before install guard, you need to install RSpec in your rails application. When you have installed RSpec you're done for install Guard. Add this in your Gemfile

{% highlight ruby %}
group :development, :test do  
  gem 'rspec-rails'
  gem 'guard-rspec'
end  
{% endhighlight %}

in the other hand you need to add growl and rb-fsevent for manage notifies and FSEvents in Mac OS . Added this lines in your Gemfile

{% highlight ruby %}
group :test do  
  gem 'rb-fsevent'
  gem 'growl
end  
{% endhighlight %}

Before concluding this installation you need to run `bundle install` and, after that, `guard init spec` for setting up Guard in your app.


[guard-url]: https://github.com/guard/guard-rspec
