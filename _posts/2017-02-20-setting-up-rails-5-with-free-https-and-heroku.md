---
layout: post
title: "Setting Up Rails 5 with free HTTPS and Custom Domain in Heroku"
date:   2017-02-20 08:01:30 -0300
categories: rails
---
I've working in a personal project and I needed an SSL certificate, so I used it as an excuse to try (Let's Encrypt)[https://letsencrypt.org/].
This website provide a free certificate for SSL.
After read many articles and many information about how to setting up Rails 5 + Custom Domain + SSL + Heroku, I prefered to write this post.

For this case I'm using a (Free DNS Provider)[http://freedns.afraid.org/]. This said, I'll go to enumerate steps for this configuration.

### 1. Setting Up SSL certificate

For to do this configuration, It necessaries to install (certbot)[https://certbot.eff.org/] that allow to install the easy way a https certificate in your website.
As I'm using Mac Os X 😏, I just to install through Hombrew.

I just simply run:

{% highlight bash %}
$ brew install certbot
{% endhighlight %}

Let's Encrypt's ideal workflow involves running it on your server. Since we're not on the Heroku server, we have to do it locally and in a few steps.

{% highlight bash %}
$ sudo certbot certonly --manual
{% endhighlight %}

You’ll be prompted to enter the domain you want a certificate for:

![image-promp](http://i.imgur.com/ZBjnEhig.png)

Stop in this place, Now is necessary to setting up your Aplication for validate this code. (Don't press: "Pres Enter to Continue", Press enter before setting up the app)

### 2. Preparing your Rails application for validate certificate

In the first place we need to prepare the application to serve the code provided for certbot

![url-validation-code](http://i.imgur.com/bAX1wyh.png)

In our Rails app you must to add a view for read the code provided for certificate, so you need to add a controller, a view and a router configuration.

config/routes.rb
{% highlight ruby %}
  get '/.well-known/acme-challenge/:id' => 'pages#letsencrypt'
{% endhighlight %}

app/controllers/pages__controller.rb
{% highlight ruby %}
  def letsencrypt
    render text: "CYpdpYsU-PUT-YOUR-TEXT-CODE-FOR-CERTIFICATE"
  end
{% endhighlight %}

If you are using devise for all controllers, remember exclude this method.
app/controllers/pages__controller.rb
{% highlight ruby %}
  skip_before_action :authenticate_account!
{% endhighlight %}

After that you can to continue the validation for your certificate, when this certificate is created,
certbot will create to directory for your domain with your certificates.
Normally this directory are: /etc/letsencrypt/live/yourdomain.com/. In this directory you can found the certiticates that I will upload to heroku server.

### 3. Uploading certificates to Heroku


