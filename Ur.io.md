# Ur.io Write Up in Markdown

## Technologies

- Socket.io
- TypeScript
- SCSS/Sass
- React
- Node.js/Express

## Process

This project was created as an improvement on a previous project I had done
which implemented the same game in just vanilla JavaScript. That was actually my
first JS project I ever made. It has since been refactored and is relatively
clean but digging through the git history you would find vast amounts of global
variables, massive complex functions, poor variable naming technique and
hardcoded constants left and right.

My intention with this new iteration was to leverage my existing knowledge of
the game logic and build upon it. The primary goals for this version were

- To write a cleaner version
- To make it capable of online multiplayer
- To use this project as an opportunity to learn two new topics which fascinated
  me: TypeScript and Socket.io.
- To implement this version in React, using what I had learned from the mistakes
  of my previous React projects

The project was built client side first which forced me to encapsulate server
side code well so it would be easy to pull out when it was time to work on the
server. This method worked well, transferring the game’s data structures and
converting client side events into Socket.io API requests was a relatively
simple process.

## Takeaways

### Sometimes code splitting can get excessive

I was an am pretty happy with how my code is organized in this project.
Especially in terms of encapsulation and writing modular code and React
components with relatively simple APIs I think I was successful.

However there is a moment that I still think about which I think has been really
formative. Toward then end of writing the server side Socket.io code I decided
to extract all the socket event handlers to a new ‘controller’ file. I had seen
this done before in other projects and I personally favor smaller files as a
general rule so I thought I would try out the pattern. But as soon as it was
done I realized I had made the code more difficult to work with. Sure it
_looked_ cleaner but now all these event listeners which had a closure on the
data passed to the Socket.io server had to accept one or even two additional
parameters.

Since then I have been introduced to a new one of those punchy three-letter
acronyms programmers love so much which fits the circumstance perfectly: AHA.
"Avoid Hasty Abstractions." Just because an abstraction _can_ be created doesn't
mean it should. Abstractions should meet certain criteria and in particular they
should be _useful_ and _appropriate_. Although one could argue that this
specific abstraction was appropriate, it wasn't worth much because it made the
code harder to grok.

### React is not meant for everything

I have been using React for a bit over a year now and have misused it left and
right. I know this because with every new project I understand it a little
better and in particular understand what it is good at and what it is not. React
is presented as "A JavaScript library for building user interfaces" and this is
what it does best. JSX, components, state, lifecycle all good stuff in my very
humble opinion. Especially when you are building a medium to large complex app
with a large amount of reuseable components.

However I was really able to compare and contrast my experience in building it
in React with the experience of building the original version in vanilla JS. I
will admit that the comparision isn't exactly apples to apples, there was
certain non-trivial functionality added to this version. However the beginning
stages of this project were very similar to the other. Server side and client
side code were originally written together and extracted from each other later
meaning that implementing the core functionality of the game itself was
comparable, just Reactified.

All that being said, this implementation took a good amount more time to
implement in comparision to the version I had made a few years ago with
significantly less experience. The code quality was certainly higher but there is
just a certain level of boilerplate and prop wrangling involved in using React that
only really starts to pay off when a project is of a bit larger scale.

In this project I had very few components that were actually reused which really
meant that there wasn't much payoff.

I still love React, it's changed the way I think about my code. However I think
the moral here is the same as the one above: "Avoid Hasty Abstractions". Just
because you can introduce an abstraction doesn't mean you should. Abstractions
need to be both appropriate and useful. React
is full of opinionated abstractions which are generally useful for guiding larger, more
complex projects. But if you don't need them, they will probably just end up getting in
your way.

### React ❤️ TypeScript

From my experience the TypeScript support in React was excellent. I loved being
able to add type checking to things like state and props. There is such a peace
of mind that comes from declaring a interface for a component. But also, at
least for me I think it helps to mentally model a component and how it should
interact with its neighbors.

While I was
working on this project I was also starting to make my way through _Head First
Design Patterns_ which was written primarily with Java developers in mind and
other than an _Intro to Computer Science_ course I had taken which predominately
used C, TypeScript is the only other statically typed language I had used to
this point. But working on this project gave me an appreciation for statically
typed language I didn't have before. It revolutionized my idea of Object
Oriented Programming. It made me want to write every new project in TypeScript
because TypeScript made me feeling like I had been writing essays without
punctuation my whole life.

TypeScript works so well with React because TypeScript lets you reify what React
essentially implies. React is a framework with opinions but when you apply
TypeScript to it, it gives things like components a life of their own. You can
make components that aren't just theoretically reusable but actually reuseable
because the guard rails are on. You can say explicitly and exactly how you want a
component to behave and TypeScript will enforce that.

So yes, React loves TypeScript not only in the fact that it supports it will but
I think also from a recognition that TypeScript loves React back. It likes the
encapsulation of components. It likes that React tunnels all this data around as
props. And it wants to protect that and make it better, more reliable and
easier.

### Socket.io is awesome but was maybe unnecessary

Essentially I used Socket.io as a glorified event handler on the server side. I
could imagine a version of this project where things like player movements were
just passed to different express API endpoints which would update the state on
the server and pass back the result to both players. And that probably would
have been fine.

Socket.io is more or less a wrapper around the Web Sockets API which allows for
low-latency, persistent, two-way communication between client and server.
What excited me
about using this library was this idea of rapid, low-latency communication which
I thought would allow for seamless and exciting gameplay. But
in retrospect, I made a board game. Board games just don't need low-latency to the
level which Web Sockets offer. Delays of even a full second or two would have
been acceptable in a game where someone may spent a minute or two pondering
their next move.

All that being said I am actually glad I used it. It made creating events and
event handlers a real pleasure and actually allowed for some nice quality of
life features for players such as a near instant notification system for
important things like if your opponent has connected/disconnected.

Although including Socket.io added some knowledge overhead and in strict terms
was unnecessary, I believe it's low-latency offered headroom to build out a
higher quality product.

### TypeScript is awesome but not stupid simple

### Challenges/Solutions

### Organizing SCSS Getting used to compiling TS Sharing types between server and client

## Lessons

### @types is your friend npm scripts are your friend

### Environment variables early and often
