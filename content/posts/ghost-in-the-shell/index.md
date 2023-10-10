+++
title = 'Ghost in the S̶h̶e̶l̶l̶ internet connection?'
date = 2022-11-19T13:30:42+02:00
draft = false
tags = [ "internet", "linux" ]
author = "jmchor"
ShowReadingTime = true
ShowBreadCrumbs = true
ShowPostNavLinks = true
ShowWordCount = true
ShowRssButtonInSectionTermList = true
UseHugoToc = true

[cover]
image = "img/cover.png"
alt = "<alt text>"
caption = "<text>"
relative = false
hidden = false
linkFullImages = true
+++


## Why I wished I knew more about the inner workings of computers

For the last three years, I have gotten increasingly interested in how computers actually work. Sure, this comes years to late (from my current standpoint) but in the past I was perfectly happy to play games and cheat my way through them (the first of which was Age of Empires with little photon laser shooting soldiers.)

But nowadays, I want to KNOW how stuff works. More often than not it's something like "Hey, how could I keep my monitors from going to sleep?" and after 10 minutes I'm down a rabbithole on Linux messageboards, sifting through information on systemd and symlinked services and whatnot. And while that is super interesting - it is also beyond me.

I had - at the beginning of my coding journey - the goal to become a sysadmin, understanding Linux as well as being able to code. But: the code took up my brain and that's whats happening now.
Thankfully, I got so far in my studies of Linux that I now can actually operate a Unix-based computer in a manner that for me I find pretty satisfactory. I like the commandline. For me, it's much faster than any other means of doing anything with the system. But some things just very much escape me. Like my Ghost in the connection.

For two weeks now, our internet system at home suddenly dropped out. My phone silently switches to mobile data, and I get an email alert from my Synology, that services are suspended cause there's no internet connection.
So I go over to our Fritzbox, and lo and behold! The LED for _Internet_ is nice and dead. And that is where the panic rises **- EVERY - DARN - TIME**.

It's nine pm, or 10, or 22:55, who cares - I don't really need the internet connection any more because I'm on my way to bed. But why is there no internet? I turn the Fritbox off and on again - oldest trick in the book, ought to work. But **nothing**.

I log into the Fritzbox home network interface and restart it - and **nothing** again!

So no I **really** start to panic - if the internet is broken, maybe something with the ISP is wrong? What if there's a problem that is SO BIG that it won't be resolved by month's end, and I won't be able to reliably attain my bootcamp?\*

Then, just for the fun of it all, I turn my laptop back on. The laptop is shut off from Wifi and connected via Ethernet (cause much much faster), and from there I try and reset the Fritzbox. And, oh sweet miracle - the internet is back.

And now, from time to time I forget to disconnect the Ethernet adapter from my laptop before shutting it down - and the internet goes down with it, like a ship that's gathered too much water. But when I turn it back on and restart the Box - et voila, it's back!

And I don't understand why - but I'd kinda like to, but then I also rather use my time to code.

Let's just hope it's a friendly ghost.

<span style="font-size:12px;">*There will be posts on that: from November 29th, I will participate in an Ironhack parttime bootcamp for fullstack web development.</span>
