(Write-up still in progress)

# Hyporeal Spotify Visualizer

Total Development Time: 212 hours 58 minutes

## Technologies

- Three.js
- Spotify Web API
- Node.js/Express
- CSS
- HTML

## Process

For some context this was my final project for Harvard's deservingly famous
online CS50 course
and my first project ever of any substantial scale. Because of this there are
many points in this post-mortem that may seem obvious but to me at the time this project was
incredibly formative. This is the spaghetti that set me on my way to becoming a
chef.

This project really started with a simple idea: make a reactive music visualizer integrated with Spotify which used 3D visuals. It took me about a week of research just to figure out what packages I would need. 

I was really diving in the deep end. I had never worked with a 3rd party library of any size. I had never interacted with a web API. I had never used npm. I had never written any back end code. In fact I don't even think that while I was writing it I was fully aware the difference between my front end and back end. I just understood that Spotify says I need to authenticate with their API with Node.js so that's what I did.

But slowly things started coming together. It took me another week start getting data flowing from the Spotify API. I really learned how to google like a programmer and read documentation during this period. 

What I loved about this project was how free form it was. I would write code until I hit a roadblock. A problem. And my problem was generally unique enough to not have a StackOverflow thread about it somewhere so I would have to think outside the box. It did not result in the cleanest code but it did result in a lot of creative/hacky solutions which were very fun. 

My very first 'prototype' was a series of console logs that would fire on every beat of a song being played through the browser. From there I started on the actual 3D visuals which would read data from some embarassingly globally scoped variables which were set from data from the API. At a certain point all the main visual elements (four separate visual panes, each which respond differently to the music) were in place and I decided to implement what I'll generously call an event-based FX system. 

This FX system is the most complex and messy part of the project and, in my attempts to refactor this project more recently, has given me the most trouble. It is a bit like a bomb exploded in the code base, scattering bits of the FX system all over the place. Two of the biggest functions in the project: getSectionEffect and handleEvents are related to this system. I may be able to tame it at some point but at the moment I think it is more valuable as a case study in how to tightly couple everything together, ambiguously name variables and completely ignore the principle of encapsulation and still make a program that works. But I wouldn't recommend it.

## Takeaways and Lessons

### Painting yourself into a corner

I think I have a bit of PTSD from this project which made me into a better developer in some ways. One of the ways is that I became allergic to painting myself into a corner. It still happens but more often I can sense the walls closing in on me and I get the sudden intense urge to refactor the code into something more encapsulated and extensible. 

I think there are a few things I keep in mind while I write code now that really helps with this:
- Could I pull this code into a separate module if I needed to? Would it make sense to?
- Is this function/class going to be easy/fun to use in the future?
- Am I able to group abstractions into concise, logical public-facing APIs?
- What abstractions am I coupling together, intentionally or not? Does it make sense?
- Am I seeing functions/classes bleeding knowledge into each other in a way that seems inappropriate or may cause things to get messy?

I think it was difficult to understand when I was at this point but even the very simple ideas of avoiding global variables and keeping functions short can get you really far in writing code that is extensible.

### How to read documentation

### JavaScript can run server side?

## Challenges and Solutions

### Sound/Visual Synchronization

### Performance optimizations
