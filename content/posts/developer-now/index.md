+++
title = "I'm the Developer Now"
date = 2023-07-01T11:16:07+02:00
draft = true
tags = [ "React", "Javascript", "coding" ]
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


### Or: how we finished bootcamp with a React social media platform

So, this is it! Bootcamp over, certification in the mail - you are now a full-stack web developer. And to be honest - that is really, really cool.

I think most of us who have built their last projects are happy that the 24 weeks are over - it took a lot of time and effort from us that we spent coding and studying and worrying about coding and studying - it is nice to do something else for a change in our freetime other than that. But by no means do I want to suggest that I did not enjoy it - because I really, really did.

Learning about React was a really great experience. And putting that knowledge to use, which essentially meant REALLY learning it, was an even better one.

### The three amigos

Everything leading up to project week didn't feel as tense (at least to me) as the last time, because I kind of already knew who I wanted to work with - so I asked my class mates from the M2 project if they wanted to work together again. And if there was ever a resounding positive answer to anything, this was it. So we informed our TAs about it, talked briefly, an idea was approved and then we basically just got to it. We discussed a concept (which was revised, or, refined, over and over again), wireframes and a basic and advanced model, and then sat down and coded. We drew up kanban cards and just went back to the same workflow as the last time - Trello cards with color codes, GitHub repos with Pull Request and Issue management, pinned Slack messages and bookmarks on Excalidraw, and that was the organisation! We gave out certain "responsibilities" without being to set in our ways - everything was a discussion.

### And once again with React

How different using React made things this time became apparent to us fairly quickly. We set up routes in the backend just like last time - but in no way did it get as complicated there as with Taskmeister. No Handlebars, no views, no nothing. Everything frontend was React - but to assume it was just rainbows and unicorns there is also quite off the mark.

The cool thing about React for me was that setting up a new page (with a Single Page Application) is incredibly easy. We used React Router, so you just - write down a route, come up with a path, and that is it. No need to do all that AND write a route on the server. Of course there is a ton more, but that is what impressed me a lot.

Getting stuff from A to B to C is another cool thing in React, since you get a few possibilities to do it. The downside is, it also makes things quite complicated if you have never dealt with it. If someone asked me now to build a React app, I'd definitely plan FIRST what kind of information I have and what needs to be put where from where, and THEN design the structure. With our project - since the objective was to learn and demonstrate our proficiency with React at the same time - we did it the other way round, or at least at the same time. Thus, passing data around happened in various forms - lifting state, context wrapper, using params, using location, prop drilling, and maybe even more. Eventually we always got there, but sometimes it proved to be quite a battle.

What I also really liked to do was the challenge to create reusable components. It worked with one out of three - I created an Image Uploader component which, according to it's props, could be used for multiple images in the same form. I modified a Select component from MUI (which freaking rocks, by the way), but it wasn't really reusable - it only did it's one thing, but I got it to be controlled. The last thing that I created to be reusable was a form which created one of two things - a collection or an item (since our project was about creating collections of items, I thought that a good thing). After two weeks of using it, style choices and UX dictated that form to be ripped in two distinct components - which was fine, since I got the practice to write something reusable AND someone else got the practice of refactoring code into something else. I can only recommend doing both.

### Getting into the Groove

The point of this project was to learn React - thus, we really only developed a concept of our app while we were writing it. This way, everything got a bit chaotic - for example, who to get data from one point to another. In the end, we used different techniques - using the Context API, Prop Drilling or Lifting State, just to name some of the possibilities. And all of it works, obviously, but it makes for a very erratic developer experience, when anyone would look at our code. We just got into the groove of doing whatever was necessary to get to the goal we wanted. *This needs to show the name of the person clicking on it, not the person clicked on? No problem, let me just rewrite the whole thing.*

In the end, we had a pretty neat product. But right there at the end, as we sat down to present our project to all of our classmates, we were still running into one major issue: CORS.

### The last hurdle

You could put a timer on - open Dev Tools, and visit our website. Sooner rather then later, the CORS errors would start popping up; everything went red, warnings galore, and no way to fix it. Or so it seemed.

In the end, it was a hint from our instructor that got us to fix it. One of my teammates texted me a link while I was in the car (back seat, no worries), and I looked into it. "I'll look at it when I'm home, maybe I can fix it quick" is what I wrote back.

Sat down at the computer, checked it out - and voila! no more CORS errors.

The problem was this: the error message claimed that a CORS policy violation was going on, even though we checked and checked again that the IP for the Origin was definitely freed up for the back end. We installed Chrome extension to override it, we used different ways of coding the same thing, but it didn't work. It turned out to be something very different: the Models in the back end which handled all the User and Document makeups for our CRUD operations.

Here's a code example of what saved us:

```javascript
const User = model("User", userSchema);

const MONGO_URI =
   process.env.MONGODB_URI

async function run() {
  await mongoose.connect(MONGO_URI);
  await User.findOne();
  console.log("Found the User Model")
}

run()

module.exports = User;
```

The important piece of code here is the *async function*. We had run our code without any the first times, and sometimes it worked, sometimes it threw CORS errors at you. When the latter happend, what actually happened was the Frontend trying to connect to the Backend with a request for a User or a Collection or whatnot, which was just not there - because the database connection hadn't been established yet. Async to the rescue: with a few lines, every request is preceded by a check "hey, do I actually see a User model?" *churning* "Yup, there it is, okay, next move!" And bam! done. It was very misleading to yell "CORS ISSUE" when it was actually "sry no database here man."

Working on this project was absolutely amazing. It took a lot of effort and focus, sometimes too much, and definitely took away too much sleep. But I think it gave us many tools, concepts of how to form ideas of data flow BEFORE writing it down, and a first-hand experience of what it means to build a fullstack application from the ground up.

If you want to check out the app - here's the [website](https://useum.netlify.app/), and here's the repo.

Have Fun!