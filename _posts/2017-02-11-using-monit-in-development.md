---
layout: post
title: "Using monit in development (OS X)"
date:   2017-02-11 19:22:30 -0300
categories: tools
---
I've been working for many time with Rails apps. I've spent hours working with [Monolithics][monolithic-url] and micro services apps. (Yep in the last time I've worked with [RabbitMQ][rabbitmq-url])

When the application grow up and has many clients, is really important to maintain highly available. [Monit][monit-url] is a tool that help to ensure that all essential services and applications are up and running. (Also it helps to restart when we have troubles with our applications)

This post explains how to configure Monit for monotoring Rails apps in development enviroment (OS X)

### Install Monit in Mac OS X

1. Enter to terminal
2. Write in terminal: `brew update`
3. Write in terminal: `brew install monit`
4. Create a ~/.monitrc or copy from `cp /usr/local/Cellar/monit/5.20.0/share/monit/monitrc ~/.monitrc` (In my case I have to copy from this directory)
5. Run monit with this command: `monit`
![image-monit-start](http://i.imgur.com/tCjwCTN.png)
6. After that you can enter in this url (by default user/password are admin/monit): `http://127.0.0.1:2812/`
7. When you enter to user and password you can watch a panel similar to:
![image-monit-enter-user-password](http://i68.tinypic.com/b3sw3r.png)

### Configurate Monit for Rails apps

After you can setting up Monit in your enviroment is time to setting up Rails for them. For this particular case I'll setup Puma, SQLite and Nginx for my test.

### Setting up Puma services

The first step


[rabbitmq-url]: https://www.rabbitmq.com/
[monolithic-url]:https://en.wikipedia.org/wiki/Monolithic_application
[monit-url]: https://mmonit.com/monit/
