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

While writing this project, particularly in the final week or two, I was constantly dealing with issues relating to how I had written previous code and blocked myself in. I mentioned that the FX system was scattered throughout the project and because of this, tweaking it to get it the way I wanted it was extremely time consuming. 

Bugs were also very hard to chase down because a certain global variable may pass through 5 different functions before one of them throws an error because it's suddenly undefined. But now I couldn't easily just move that variable out of the global scope because 5 different functions were still relying on it to be there and were each expecting to recieve it in a certain order and in a certain shape.

I think there are a few things I keep in mind now while I write code now that really helps with this:
- Could I pull this code into a separate module if I needed to? Would it make sense to?
- Is this function/class going to be easy/fun to use in the future?
- Am I able to group abstractions into concise, logical public-facing APIs?
- What abstractions am I coupling together, intentionally or not? Does it make sense?
- Am I seeing functions/classes bleeding knowledge into each other in a way that seems inappropriate or may cause things to get messy?

I think it was difficult to understand when I was at this point but even the very simple ideas of avoiding global variables and keeping functions short can get you really far in writing code that is extensible.

### How to read documentation

For all the faults of this project and the mistakes I made making it, I am very grateful I made it for one reason especially: I have never experienced Tutorial Hell. I am very sympathetic to people who have and do but I think entering into this project knowing absolutely nothing about the technologies I would need to build it or the architecture it might require made me figure it out and build confidence in my ability to figure it out.

To this day I do not get intimidated by big, dangerous sounding programming concepts. Maybe a little. But having experience overcoming my own ignorance over and over again, I just don't believe that there are many ideas I can't wrap my head around or problems I can't solve.

But you have to read the documentation. I do believe reading documentation is not like reading other things and my style has evolved a lot over time. I don't read documentation once and move on. I don't think most people do. Sometimes I skim it, other times I read it very deeply, reading the same paragraph over and over and many times I use it as a reference. 

But I had to learn all of this the hard way and I didn't know to do any of that when I started this project. So I would skim when I should have read deeply and would get the very common programmer syndrome of spending many hours trying to solve a problem only to find the answer very obviously placed in the docs. I would also do the opposite, reading deeply when I should have skimmed and wasting a lot of time and mental energy coming to grips with concepts that were completely irrelevant to the problem I was trying to solve.

I think learning to read documentation is actually much more of a personal process than it is often described as being. We all take in and process information differently. I generally scan the Ikea directions and arrange the parts before putting them together, using the directions as a reference when I get stuck. Trying to grasp the high-level abstraction and whittling it down works for me. Other people might follow the directions step-by-step and that works best for them.

### JavaScript can run server side?

## Challenges and Solutions

### Sound/Visual Synchronization

### Performance optimizations
