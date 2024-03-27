+++
title = 'Deploying a React / Node app on Linode with Nginx'
date = 2024-03-27T13:33:20+02:00
draft = false
tags = [ "blog", "react", "node", "nginx" ]
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

I wrote a new project - but this isn't the blog post about the project. If and When I write it, you'll be able to see it here.

No, this is the blog post about how I got the new project up and running on Linode. Let's go.

## Starting at the "finish"

Web apps are never really finished, I think they're at some point good enough to try deployment - like, good enough, but with room to grow. So it also came to be for my latest project, a React/Node.js app where I tried my hand at GraphQL data fetching. So the app was sort of finished enough (and during deploy it showed that it really wasn't), so I went ahead to get it deployed.

For previous apps I had relied solely on third party services - Netlify, Heroku, Cyclic and Render (once on Fly.io) - but this time I wanted to have the app running on my own web server. Well, shared CPU and all, but on my own domain. I had a [video](https://www.youtube.com/watch?v=svEs1TafR7E&t=7s) all lined up that showed how to deploy a MERN stack app to a Linode no problem

- no connection to backend
- frantically changing local host adresses
- fiddling with sites-available
- abandoning for Render
- not getting it to work
- setting up CNAME
- still nothing
- Render wont play nice with cookies
- Write a version with local storage
- Render works
- Hooking web server frontend to Render backend - works
- Why not make another subdomain for the backend?
- Set it up - works
- Double check the cookie version and set it up again
- use nginx conf.d
- works
- fix code
- include location / in server conf
- perfect
