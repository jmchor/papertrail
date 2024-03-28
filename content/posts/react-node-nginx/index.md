+++
title = 'Deploying a React / Node app on Linode with Nginx'
date = 2024-03-27T13:33:20+02:00
draft = false
tags = [ "blog", "react", "node", "nginx", "graphql", "linode" ]
author = "jmchor"
ShowReadingTime = true
ShowBreadCrumbs = true
ShowPostNavLinks = true
ShowWordCount = true
ShowRssButtonInSectionTermList = true
UseHugoToc = true

[cover]
image = "img/cover.jpg"
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

For previous apps I had relied solely on third party services - Netlify, Heroku, Cyclic and Render (once on Fly.io) - but this time I wanted to have the app running on my own web server. Well, shared CPU and all, but on my own domain. I had a [video](https://www.youtube.com/watch?v=svEs1TafR7E&t=7s) all lined up that showed how to deploy a MERN stack app to a Linode no problem. The video by CodingInFlow went over every important aspect of deployment to a webserver - setting up the Linode and securing access, setting up a firewall using ufw and restricting access from the outside, all the good stuff.

Getting the code onto the webserver was conceivable easy - I created a directory and just git pulled all the code in (actually, I did that numerous times, but whatever). Then the setup works just with any other project code:

```bash
npm install //for all the cool dependecies!
```

and depending on the scripts you set up in the package.json

```bash
npm run build //which is just "vite build" for the frontend, and "tsc" for the backend
```

for compiling the TypeScript code.

Then we had to split ways.

### Backend

The backend is written Node.js, with GraphQL and everything (which was kind of a problem later on but also not). So, after compiling the TS code into the /dist folder, I had to make the code run consistently as I did while developing - but I can't log into the console every time when something is going run and run 'npm run dev', now can I. Thankfully I already new about a service used for that, and the whole setup was also talked about in the video - using the process manager **pm2**.
Setting it up is fairly easy - just install it using npm, and run it!

```bash
cd *your_repo*/dist
pm2 start server.js //or whatever your main file is called
pm2 save
pm2 list
```

That last command will output a list of all the pm2 processes running currently:

```bash
┌────┬───────────┬─────────────┬─────────┬─────────┬──────────┬────────┬──────┬───────────┬──────────┬──────────┬──────────┬──────────┐
│ id │ name      │ namespace   │ version │ mode    │ pid      │ uptime │ ↺    │ status    │ cpu      │ mem      │ user     │ watching │
├────┼───────────┼─────────────┼─────────┼─────────┼──────────┼────────┼──────┼───────────┼──────────┼──────────┼──────────┼──────────┤
│ 0  │ index     │ default     │ 1.0.0   │ fork    │ 0        │ 0      │ 0    │ stopped   │ 0%       │ 0b       │ jc       │ disabled │
│ 1  │ server    │ default     │ 1.0.0   │ fork    │ 12559    │ 40h    │ 3    │ online    │ 0%       │ 67.6mb   │ jc       │ disabled │
└────┴───────────┴─────────────┴─────────┴─────────┴──────────┴────────┴──────┴───────────┴──────────┴──────────┴──────────┴──────────┘
```

The name will be set after the file name you're running with pm2 - which is why I renamed my main server file "server.js" (creative, I know). Whenever you need to make changes in the code, don't forget to compile and then run the new code with pm2 using

```bash
pm2 restart server.js
```

So that process is running - on to the front end.

### Frontend

Fairly easy here as well - just build the code into the /dist directory. Then, following the next steps of the video, I copied all contents of the dist folder to the directory "/var/www/boilerplate.jmchor.dev" - the root directory for my React application. And that was basically it.

### NGINX config

This is where nginx and the web server configuration comes in - and this is basically also where things went awry. The basic server config looks like this:

```bash
server {
        listen 80;
        listen [::]:80;
        root /var/www/testing.jmchor.dev;
        index index.html index.htm;
        server_name testing.jmchor.dev;

   location / {
       try_files $uri /index.html;
            }

   location /graphql {
    proxy_pass https://localhost:4000/graphql;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection 'upgrade';
    proxy_set_header Host $host;
    proxy_cache_bypass $http_upgrade;
        }
    }
```

which is almost the same code that I took from the video. It basically specifies which port to listen on (80, which is http, which should also be made available in your firewall), the root directory where the html-files can be accessed, what does files are called, and what the server is called.
Now, in the video (a MERN stack application), the server has REST API endpoints specified to run at _/api_, which is why for the backend the location is specified at /api, and to run on the port specified in the code.
In my case, I have a GraphQL server running on port 4000, and GraphQL servers are specified by a single endpoint, _/graphl_.

After writing the server conf, you need to check that the nginx confugrations are written up to specs, and then restart the whole service:

```bash
sudo nginx -t
sudo systemctl reload nginx
```

And tadaa - absolutely no connection to the backend. The React app itself was running (almost) smoothly - aside from a weird 404 error I got every time I refreshed. But we'll get to that in a bit.

Opening my console I saw a ton of connection errors - refused, or CORS error or whatnot. And: I could not get to the GraphQL server playground at the specified address (which should just have been 'boilerplate.jmchor.dev/graphql'). I experimented with changing the localhost port (enabling that port in the ufw), changing the "proxy_pass" in the server conf to omit the /graphql - all to no avail whatsoever. I also ended up fiddling a ton with the sites-available and sites-enabled stuff (which you should NOT do) - but nothing worked.

I obiously got a bit upset by that, and decided to try the old way - using Render.

### Render

Render is cool service to showcase React/Node apps, because it allows you to run both backend and frontend on the same service. Maybe I'll write about how to set that up some time, but not now.
I set up the backend as a web service and the frontend as a static site - and now I could finally get both to communicate to each other! Articles where found in the database and displayed, all was well - until it wasn't.
After a bunch of trial & error I learned that because Render uses a public suffix for all deployed pages ('.onrender.com'), cookie authentication does not work. And tbh - I spent a lot of effort making httpOnly cookie authentication a thing.
But more so I wanted to see that app deployed.
I tried running the app on custom domains (had to set up CNAME records in my Linode), but that also didn't do anything.

### A Quick Rewrite

I resolved to - well, solve that problem later, and just make it work. In an hour I had a short rewrite done - replacing all the cookie setup and authentication with local storage. Not particularily secure, but it works. And it worked! I had my app deployed to Render and was thus able to see some of the blatant holes in my code, that I fixed quickly (stuff you won't even see in a localhost environment).

I'm so glad I decided to deploy using Render, cause it gave me an idea - if the backend is running on Render, why not try and hook it up to the React app on my web server? Said, done - and it worked! Which gave rise to the next idea - why don't I use TWO subdomains, one for back, one for front, to deploy my app? I mean, essentially running a static site and a web service is similar, so why not?

I went through the whole spiel (`git pull`ing code, building, restarting `pm2`, copying the React code to the root directory) and - it worked! My app was indeed running - but it was still "just" the localStorage version. I wanted those cookies - and now that I was able to use my own web server, why not try it?

By looking up how to just run a Node process on it's own subdomain I came across a ton of articles that were very outspoken against configuring an nginx web server using the "sites-available" folder and symlinking. Really, the easiest way was also the most prevalent - just set up a server conf in the '/etc/nginx/conf.d' directory and be done with it:

```bash
server {
    server_name boilerplate-backend.jmchor.dev www.boilerplate-backend.jmchor.dev;
    location / {
        proxy_pass http://localhost:4444/graphql;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
    listen 80;

}
```

Since the process for the backend was already running using pm2, and running on port 4444 on the localhost (that is to say, just on the web hosting), I only needed to specify a location for the server to be available - the root location pointing to ` :4444/graphql`. And the server was thus available at "boilerplate-backend.jmchor.dev", easy as that.

To make it all nice, I left the "sites-available" stuff where it was, and set up another server conf for the React code as well:

```bash
server {
    server_name    boilerplate.jmchor.dev www.boilerplate.jmchor.dev;
    listen 80;

location / {
    root           /var/www/boilerplate.jmchor.dev;
            }
}
```

And then everything was running smoothly, even with the cookies (though I had to make adjustments in the code's env variables to no point to the correct URLs).

## At the finish, ready to start

### 404 Route Errors with React and nginx

Aside from some things not working as expected (fetching only half the data, or not fetching any profile data at all - which were fixes in the code), the most annoying one were constant 404 errors when refreshing a page in the React app. Every time I did that, I just conjured up the white screen proclaiming the dreaded "404 Not Found. nginx/"

What was up with that? I thought that's maybe just how that is now - but then I remembered that, back at Ironhack, we had a similar problem with pages rendering wrongly. For that, we had to include a `_redirects`directory in the code which would redirect any route requests to /index.html with a code of 200 (since ALL React pages are rendered on the index.html root div) - but that did not help. So, internet to the rescue - in the form of [this blog post](https://www.frontendundefined.com/posts/tutorials/nginx-react-router-404/).

I was very, very happy to read this, and even happier when the fix was easy, and worked right away. Read the article, but tl;dr:

I'm using TanStack Router, which works like React Router - which means, Client Side Routing. Which means, the browser is serving those routes using JavaScript, which confuses nginx a lot - the web server is used to serving web pages from the disk (e.g. from files like 'about.html'). Since we are running an SPA (single page application) which presents as if it had many pages (which is a lie)

<div class="post-image">
    <img src="img/legend.gif" alt="image">
</div>

we have to get nginx to serve the only file we have (index.html) for EVERY path and route we might be navigating. This is done by adding `try_files $uri $uri/ /index.html;`to the server configuration - and that is it.

A finishing touch to any web app is of course to enable HTTPS with an SSL certificate. I can highly recommend the Linode docs on installing [Certbot](https://certbot.eff.org/) right here from their [document hub](https://www.linode.com/docs/guides/enabling-https-using-certbot-with-nginx-on-ubuntu/), all fairly easy to set up. When you are ready, all you have to do is run `sudo certbot --nginx`(AFTER setting up all the server configurations of course), and then you just have to pick out the subdomains you'd like the letsencrypt certificate applied to. All done automatically, and then your server configurations will look like this:

#### React app

```bash
server {
    server_name    boilerplate.jmchor.dev www.boilerplate.jmchor.dev;

location / {

    root           /var/www/boilerplate.jmchor.dev;
    try_files      $uri $uri/ /index.html;

        }

    listen 443 ssl; # managed by Certbot
    ssl_certificate /etc/letsencrypt/live/boilerplate.jmchor.dev/fullchain.pem; # managed by Certbot
    ssl_certificate_key /etc/letsencrypt/live/boilerplate.jmchor.dev/privkey.pem; # managed by Certbot
    include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot

        }
server {
    if ($host = www.boilerplate.jmchor.dev) {
        return 301 https://$host$request_uri;
    } # managed by Certbot

    if ($host = boilerplate.jmchor.dev) {
        return 301 https://$host$request_uri;
    } # managed by Certbot

    server_name    boilerplate.jmchor.dev www.boilerplate.jmchor.dev;
    listen 80;
    return 404; # managed by Certbot

}
```

#### Node

```bash
server {
    server_name boilerplate-backend.jmchor.dev www.boilerplate-backend.jmchor.dev;

    location / {
        proxy_pass http://localhost:4444/graphql;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }

    listen 443 ssl; # managed by Certbot
    ssl_certificate /etc/letsencrypt/live/www.boilerplate-backend.jmchor.dev/fullchain.pem; # managed by Certbot
    ssl_certificate_key /etc/letsencrypt/live/www.boilerplate-backend.jmchor.dev/privkey.pem; # managed by Certbot
    include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot


}
server {
    if ($host = boilerplate-backend.jmchor.dev) {
        return 301 https://$host$request_uri;
    } # managed by Certbot

    if ($host = www.boilerplate-backend.jmchor.dev) {
        return 301 https://$host$request_uri;
    } # managed by Certbot

    server_name boilerplate-backend.jmchor.dev www.boilerplate-backend.jmchor.dev;
    listen 80;
    return 404; # managed by Certbot

}
```

Now the web app is running as smoothly as I currently have the capacity to make it run. I laid "siege" to it (using [Siege](https://www.joedog.org/siege-home/), to see how many requests it could withstand) and was happy with the result. Everything is going well so far, but I am sure bugs will show their faces soon enough. Be that as it may - now I can say that I was able to deploy a React/Node app using GraphQL to my very own (well, shared) web server on a Linode. And so can you.
