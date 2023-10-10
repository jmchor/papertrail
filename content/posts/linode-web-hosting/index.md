+++
title = 'Linode Web Hosting'
date = 2022-11-25T13:25:26+02:00
draft = false
tags = [ "coding", "ghost" ]
author = "jmchor"
ShowReadingTime = true
ShowBreadCrumbs = true
ShowPostNavLinks = true
ShowWordCount = true
ShowRssButtonInSectionTermList = true
UseHugoToc = true
TocOpen = false

[cover]
image = "img/cover.png"
alt = "<alt text>"
caption = "<text>"
relative = false
hidden = false
linkFullImages = true
+++

I don't know exactly when I decided to switch to Linode for Web Hosting - I can't pinpoint the day or anything, but certainly I remember WHY I did it. But let's back up a bit.

Since I started coding (which seems AGES ago, but arguably for real that was in the last nine months) I wanted a webpage or website that I made accessible for the public - either via my Synology or a proper domain. Now, as you could read [here](https://blog.jmchor.dev/move-and-confusion/), our ISP does not have public IPs available (and is currently still working on providing IPv6 addresses) which makes a pbulicly accessible solution for web hosting via the Synology no possible. So what I instead did was just tinker with web page building on localhost (I first installed XAMPP after reading about it in Paul McFedries' book and ran simple index.html files there), basically just exercising clunky html writing, early style sheet stuff etc.

Later on, I wanted to actually have a website available to the public (I since had gotten better at making a web page, thankfully - I didn't think that flexbox was something optional, for example). Since there are SO MANY web hosting companies, I decided to go with the one that was [hosting](https://all-inkl.com/) the WordPress website for the NGO I was working with. And for a surprisingly cheap fee of about eight Euros a month you got file hosting, three domains and 250 subdomains, SSL and email included. They even provide a software pack for easy installation - like WordPress or Drupal, or NextCloud. So I just went with it, uploading the first coherent website to the web using FileZilla - and hopefully I will have some time in the future to present a snippet of what that website looked like, cause it was seriously *so full* of stuff that I recently had learned or wanted to have on there that it was a super sensory **overload**.

### No Ghost? No thanks.

I say was, because only recently I deleted everything from that hosting provider. Why?

Well, one of the reason why was: *they couldn't host a Ghost blog*. Not that this is the thing that every action should be measured against, but for some reason I was very set on having a Ghost blog. For a while there I used the second of the three free domains that came with the hosting subscription and had a WordPress blog at **ghostnotes.org**, but the whole WordPress thing was not what I wanted. It offered too much in a sense (like in too many choices, maybe?), and I just wanted - a blog. And I wanted it to be Ghost - I mean, one of my favorite bands is called [Ghost](https://ghost-official.com/), so why not? But the provider couldn't provide cause 1st: I only had the web hosting solution, and for something like that I needed to get a server (cheapest option at 99 bucks, so no thank you) and 2nd: Ghost runs on Node, and they don't do Node. Weird, but that kinda decided it.

But where to go? Get a **DigitalOcean** droplet for five bucks a month? That's almost as much as I would have paid for oh-so-many subdomains. So no. And then I think something clicked, and I remembered that one of the frequent sponsors of [my favorite podcast](https://syntax.fm/) is **Linode - Linux Cloud Computing**. And Linode offers a free trial thing of 2 Months / $100 so you could check it out. And so I did.

### The machine in the machine

And *OH* was I happy. I mean, you basically get a whole different "computer" - you pick and choose the specs (for website hosting you don't need the best of the best) and can switch them up or down or however you please. Sure, you have to get a domain from a separate registrar, but if you're not too crazy you get that for 11 Euros a year, which is less than a buck a month (I'm GREAT at math).

I picked a Linode that costs me 10 bucks a month, plus a domain name, so 11 bucks a month - a bit more than what I paid at the other provider. Plus, nobody installed nothing for me there. What I now had was a domain name and a GNU-Linux system (I picked Ubuntu cause reasons) and TONS of Linode documents. And so I tinkered my way through setting up a web server (**nginx**), learning about A records and name servers at a rapid pace, deleting and editing nginx.conf-files over and over until I had it just right and had set up a web page. And after some more reading and tinkering, even a subdomain that cost me nothing but some more work. Thankfully I had picked up quite a few tricks on the CLI since I had switched fully to Linux about a year ago and had come to love manipulating the system via the command line. And so setting up a web server and pages was not a big problem (the issue was just the "which config goes where" type thing, cause the docs were a bit conflicting) - but in the end everything worked out well and I just hope that I saved the right docs to be able to replicate it.

That was that. But I also wanted a Ghost blog - which is the "reasons" cited earlier for picking the Ubuntu 22.04.01 LTS OS, since the docs on deploying Ghost on Linode recommended that. And those docs were extremely helpful - up until the point that the mysql database threw an error. Or, I should say, that's what turned out to be the error - I deleted the Ghost install and even the whole Linode before picking up on that. But in the end I also found a solution for the database error (spoiler: for some reason it just would recognize the logins I gave it at Ghost setup). So I changed the logins, saved the docs I found the solution in and voila! - here we are.

This blog is running on the Linode so inventively named **dev-01-prod **and I am very happy with how everything is running - smoothly, that is. I get to work on my CLI skills as well as web hosting, and by moving from a provided service to a provided server with supplying my own work, it just feels great, too.

Currently, I am working on a new version of my website - or a whole new revamp, basically. That is to say - I had already written a revamp of the original-original, which was already less cluttered and cleaner, but I ran to far in the direction of trying to implement "cool" features (like a slider that completely ripped my screen ratio apart). So, the new-new revamp is a very early work-in-progress, where I am using a mixed **Grid-Flexbox** layout, a more complex folder structure, oh - and [TypeScript](https://www.totaltypescript.com/). We'll see how far I can get before I start all over again (again - again).

jmc

