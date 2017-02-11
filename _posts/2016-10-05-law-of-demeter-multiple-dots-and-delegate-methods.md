---
layout: post
title: "Law of Demeter: Multiple dots and delegate methods"
date:   2016-10-05 00:00:00 -0300
categories: best practices
---
This post is an extract from [Ruby Science book][ruby-science-book]

The law of Demeter was developed at Northeastern University. This principles states that
a method of an object should invoke only the methods of the following kind objects:

1. Itself
2. Its parameter
3. Any object it creates/instantiates
4. Its direct component object

Like a many principles, the Law of Demeter is an attempt to help developers manage dependencies. The law restricts how deeply a method can reach into another object's dependency graph, preventing any one method from becoming tightly coupled to another object's structure.

## Multiples dots

The most obvious violation of the law of Demeter is multiple dots. This meaning a chain of methods being invoked on each others returns values.

Example:

{% highlight ruby %}
class User
  def discounted_plan_price(discount_price)
    coupon = Coupon.new(discount_price)
    coupon.discount(account.plan.price)
  end
end
{% endhighlight %}

The call account.plan.price violates the Law of Demeter by invoking price on
return value of plan. The price method is not a method on User, its parameter
discount_code, its instantiated object coupon or its direct component account.

The quickest way to avoid violations of this nature is to delegate the method:

Example:

{% highlight ruby %}
  class User
    delegate :discount_plan_price, to: :account
  end
{% endhighlight %}

If you find yourself writing lot of delegators, consider changing the consumer
class to take a different object. For example if you need to delegate numerous
User methods to Account.


[ruby-science-book]: https://thoughtbot.com/books
