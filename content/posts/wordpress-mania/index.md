+++
title = 'Wordpress Mania'
date = 2022-11-03T07:14:57+02:00
draft = false
tags = [ "wordpress", "coding" ]
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

Can you relate with this weird state of mind, where you fixate on an idea and stress yourself out over nothing in particular? No deadlines, just your own drive? I'm guessing, everyone had that at some point in their lives.

For a week at the end of October I almost did nothing else on the computer other than WordPress. Sure, I checked mails and such, but I didn't do any exercises, tutorials, I didn't code on a website project - I only went to the WordPress site of an NGO I am part of, and fired up the staging website.

It was entirely my idea - nobody "commissioned" me to do it - but there had been discussion about revamping the website - restructuring the knowledge base, creating different access points for users with different interests and backgrounds. To me, the website was too "full" - all of the content was kind of sprawled over it. Not in a 1996-HTML-Only-Webpage type of design, but in "there is too much text here for me to take in" way. The design, colors, shapes and presentation did it's job well, but still - I felt the UX could be improved.

So I took it on myself to do exactly that. Since I did not want the original website to be impeded at any cost, I quickly familiarized myself with the Staging Plugin Wordpress provides, and cloned the page.

Up until that point what I mostly did for the NGO was set up Matomo Analytics and keep the website updated. Nothing too in-depth, so I saw this entirely voluntary project as a way for me to "practice" Wordpress. And a good thing, too - if you have to first set up everything and write a ton of content AND THEN you get to play around with plugins and styling and whatnot - it just, it takes too long. So I counted myself lucky that I could just play with it.

The person who originally had set up the Wordpress site used a blankslate child theme and wrote the rest themselves, using [Bootstrap](https://getbootstrap.com/docs/3.4/css/) and  - that was about it. Which is also where the problems came in: I don't know PHP and I have never worked with Bootstrap (which will change) - so what I instead opted for was: a full-on switch to a completely new theme.

Which was a major undertaking by itself. What do I want out of a theme? Do I need a sticky nav menu? What does this and that themes search page look like? Which plugins are supported?

I checked out I think six different themes until I settled for one - it didn't have a sticky nav, but it supported [conditional menus](https://wordpress.org/plugins/conditional-menus/) and the search page was coded into the theme in a way that was not terrible (not that I could judge the code).

And then the fun part started. I tried to clean up the mess that the switch to the new theme created - putting the right menus at the right place, moving things around, rounding corners, adjusting background images etc. - most of which I accomplished by extensively writing additional CSS. Other things that I liked - like a sticky nav - I was able to put in with a nice plugin that allowed me to [add my on JavaScript code](https://wordpress.org/plugins/insert-headers-and-footers/) (of course you can stick a script in the header - but this is WordPress! It's plugins held together by faith and spit!)

I also added pop-ups (for info boxes) and was able to work around some things the theme lacked by using [shortcode](https://getshortcodes.com/) in the HTML editor of the plugin - basically, the whole thing was an exercise in finding creative workarounds to make up for my lack of PHP knowledge.

After coding and tweaking and uploading images and coding some more, after about six days I was done, and I felt done. Not that the website was done, but it was done in a way that I could show it to the people responsible.

They didn't exactly shoot it down (most of them were pretty impressed by what I had done) - but thankfully at that meeting, an actual designer familiar with Wordpress and web design was there and told me, that the effort I put in, the work and what I was able to show for it, was great - conceptually, none of it made sense. And the fun part is: I agreed. I didn't set out to create the best user experience one could ever have - to say it bluntly: I took a copy of a website and crammed it full of gimmicks, tools and little code snippets just to see if I could do it.

And I could, and it was worth it, just for the work and the experience.

Oh, and people took my effort to heart. We basically created a "task force" to write up a new website from scratch. And I got better at WordPress. Everybody wins.

jmc