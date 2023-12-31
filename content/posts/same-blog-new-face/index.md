+++
title = 'Same Blog, New Face (and Bones)'
date = 2023-10-12T06:32:20+02:00
draft = true
tags = [ "blog", "ghost", "hugo" ]
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

I can't even tell exactly why I did it this week of all times, or why Hugo, or a rewrite - it was just at the end of last week, I sat at my desk and was like: "Hey, wasn't there this one framework to do stuff with - what was it called, Hugo?" And Bam! - a few days later I have my new old blog deployed. On the same Linode, probably a different server, and definitely using a different framework. And I gotta say, I'm really happy with my decision.

### Why change?

I found that my motivations run in phases - and I have the strong suspicion that almost everyone can corroborate this experience at one point or another in their life. What I mean is that we have things that we love to do but we don't love to do them _all the time_; and that's also totally fine. For me, all things seem to go that way. And it's much easier to accept for me when I accepted the fact that we are not in control of our feelings but our feelings are basically in control of us (I'd like to write more in depth about that, the context here is just not quite right).
So, as I was saying - feelings control us; that is seen easiest when we sit down and try to think of nothing, and if we don't pay attention - suddenly we find ourselves in a frame of reference that had nothing to do with why we sat down in the first place. Thoughts and feelings yank us this way and that - and I think the same is the case with our hobbies, passions and obsessions. For me, those passions are currently

- Buddhist practice
- drumming
- tech projects
- self help

Not necessarily in order, or case in point: the order always changes. Two weeks ago I was very occupied with learning to play the drum line for thirteen songs, cause my band got a pretty last-minute gig. Three months before that, I was also very much into drumming, but more from a technical point of view. Two and a half months ago, I was very much into happiness research, which over time made a transformation into interest in Buddhist teachings. About a month ago, I started a new job and really got into tech things again - that came along with starting a course in Java, getting back into Bash scripting more, looking into a rewrite of my portfolio page using Gatsby - which ultimately resulted in "hey, actually, I want to write some more blog stuff. But kinda new. So how?". And from the back of my mind, somewhere, I unearthed a memory that had to do with Hugo. And so I googled, and probably I had learned a lot in the meantime, because setting everything up using Hugo was just as easy as pie, if you consider pie to be easy.

### Like Ghost, but much more configurable

The more choices we have, the easier we are disconcerted - we get choice fatigue. Unless! unless we have to discover the choices ourselves.

I studied the Hugo homepage a bit and decided to just give it a try - from the first time I used HTML I really fell in love with localhost, and to deploy something on a test server running on yor local machine just gives me a lot of contentment and pleasure. So I followed the basic usage guidelines, pulled up a Hugo page with the recommended Theme, and voila! I had created a new page. Then I went ahead and looked at other themes you can use in Hugo - and that is always something slightly overwhelming. They all look good, they probably all have cool features and so on and so forth. I don't exactly remember how, but I decided on Papermod fairly quickly, because the name "Papertrail" suddenly came into my head, and the similarity of the words seemed fortunate to me.

Then I just wanted to alter one thing: have a little thumbnail image of the post on the landing pages' post list. I did a quick internet search, and someone on a Hugo board just wrote "then put it into the CSS". And I was like "CSS, what?!", and lo and behold! there was indeed a CSS file in the Hugo site folder! Multiple, in fact, but now I understood what was going on. Hugo basically created an index.html from files and templates - a static site generator, as it were. And by and large: I know how to manipulate **that**.

I went ahead and took this very cool theme and adjusted it to my needs. I created the thumbnail list view that you can see now, and adjusted the whole structure to look a bit wider, to display different icons at the top that lead to different things. I learned about the Hugo folder structure that catches tags and whatnot to display, and learned how to write Go templates (instead of Handlebars, but the idea is the same). And step by step, I create the blog that I wanted. It looks similar to the Ghost template that I used, but with a few twists and turns here and there. And now, whenever I see something that makes me think "hm, do I really want it to look that way?" I can delve into the code and just change it. Or realize how intricately it is done, or how deep into the structure I would need to dig, and decide to live with a minor "flaw" - such is the world of developing stuff.

### Import and banish the Ghost

Thankfully, Ghost comes with an export function. And thankfully, somebody wrote a [GhostToHugo](https://github.com/jbarone/ghostToHugo) program - which I didn't end up using. But what I used was the Copy-Pasta-Function of my keyboard as well as [Paste To Markdown](https://euangoddard.github.io/clipboard2markdown/) to pour all my blog posts into md syntax to put it into the Hugo files. I also finally got around to collect all of my entries on my Ironhack web development bootcamp experience and put it into [one big blog post](https://papertrail.jmchor.dev/posts/ironhack-experience/).
The switch from Ghost to Hugo also came with another perk - since I'm hosting this on a Linode, and Hugo bare uses any resources, I felt safe enough to downgrade my linode to a Nanode - much cheaper, and more than enough space and power to run this blog, my portfolio website, and whatever fun shenanigans I might come up with (such as checking out Gatsby, or rewriting my home page in React). So - as another failsafe - I created a locally hosted copy of the Ghost blog on my machine, and then I went and

```bash
ghost stop
```
-ed the blog and discontinued the DNS record. I might spin it up again, I might not.

I learned how to set up Ghost on a machine, I learned how to update and delete it. I learned how to use Hugo, and Markdown much more efficiently. I learned a ton, and on top - it looks cool.